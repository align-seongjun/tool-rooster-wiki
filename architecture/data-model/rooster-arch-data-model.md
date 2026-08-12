# DB 스키마

## 개요

SQLite 스키마는 `games` / `tasks` / `completions` 3개 테이블로 구성한다.

## 테이블

### `games` — 게임 등록

- `name` (고유 식별자)
- 숙제 등록 전 게임을 먼저 등록해야 함 — 자유 텍스트로 두면 오타/표기 불일치로 게임별 그룹화가 깨지므로 사전 등록을 강제
- 삭제(`game rm`) 시 연관 숙제 처리: 기본은 인터랙티브 확인("N개 숙제도 같이 삭제할까요?"), `--cascade` 플래그를 주면 확인 없이 게임+숙제 일괄 삭제(스크립트/자동화 용도)

### `tasks` — 숙제 정의

- `game_ref` (`games.name` 참조)
- `task_name`
- `period_type` (`daily` / `weekly` / `monthly` / `once`)
- `reset_rule` — periodic 타입 전용. daily는 시:분, weekly는 요일+시각, monthly는 일자+시각
- `notify_before_minutes` — 마감 몇 분 전에 알림을 보낼지
- `enabled` — 잠시 중단(삭제 없이 비활성화)

**일회성 일정(`period_type = once`)**: `reset_rule` 대신 특정 날짜·시각(`deadline_at`) 하나만 가짐. 완료 처리는 `completions` 로그 구조를 그대로 재사용(한 번 기록되면 끝, "다음 주기" 없음). 마감 경과 후 미완료 시 자동 숨김/삭제하지 않고 "지남(overdue)" 상태로 계속 표시 — 사용자가 직접 삭제.

### `completions` — 완료 이력 로그

- `task_id`, `cycle_start`, `completed_at`
- "현재 주기 완료 여부"는 플래그를 따로 관리하지 않고 현재 주기 윈도우 안에 로그가 존재하는지로 판단
- 리셋 시점마다 초기화 로직이 필요 없고, 완료 이력이 자연스럽게 쌓여 나중에 통계 기능에도 활용 가능

## 시간대

- 태스크별 `reset_timezone` 오버라이드는 넣지 않고 **시스템 로컬 시간대 하나로 통일**
- 리셋 시각(자정/새벽5시/오전9시 등)은 게임마다 다르지만 전부 로컬 기준으로 보면 되고, 실제로 사용자가 다른 시간대에서 접속해도 "현재 컴퓨터 기준"으로 보는 게 자연스러움

## 제약사항

- `tasks.game_ref`는 반드시 존재하는 `games.name`을 참조(참조 무결성) — [game-task 요구사항](../../requirements/game-task/rooster-req-game-task) 참조
