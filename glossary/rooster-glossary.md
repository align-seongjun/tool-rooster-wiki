# rooster 용어 사전

## 도메인 용어

| 용어 | 설명 |
|------|------|
| 엔진(engine) | 백그라운드 상주 프로세스. 스케줄러 + 로컬 HTTP API 제공. CLI/GUI는 이 엔진의 클라이언트 |
| 게임(game) | 숙제가 소속되는 상위 단위. 등록은 자유 텍스트가 아니라 사전 등록 필수(오타/표기 불일치 방지) |
| 숙제(task) | 게임에 속한 반복 또는 일회성 일정. `period_type`으로 반복/일회성을 구분 |
| 반복 숙제 | `period_type`이 `daily`/`weekly`/`monthly`인 숙제. 완료 처리 후 다음 주기에 다시 나타남 |
| 일회성 이벤트(once) | `period_type=once`. 특정 마감 시각(`deadline_at`) 하나만 갖고, 완료 후 다음 주기가 없음 |
| 마감 경과(overdue) | 마감이 지났는데 완료되지 않은 상태. 자동 삭제하지 않고 계속 표시, 사용자가 직접 삭제 |
| 완료 이력(completions) | `task_id`/`cycle_start`/`completed_at` 로그. "현재 주기 완료 여부"를 별도 플래그 없이 로그 존재 여부로 판단 |
| 리셋 규칙(reset_rule) | 반복 숙제의 주기 리셋 시각 정의 (daily=시:분, weekly=요일+시각, monthly=일자+시각) |
| notify-before | 마감 몇 분 전에 알림을 보낼지 지정하는 값(분 단위) |
| 오버레이 GUI | 읽기 전용, 화면 위에 항상 떠 있는 GUI 형태(MVP 이후). 즐겨찾기한 일정을 상시 열람하는 용도 — 알림 수단 아님 |
| 즐겨찾기(오버레이) | 마감 임박 여부와 무관하게 사용자가 오버레이 GUI에 상시 띄워두고 싶어하는 일정 |

## 기술 용어

| 용어 | 설명 |
|------|------|
| loopback (127.0.0.1) | 엔진의 로컬 HTTP API가 바인딩되는 주소 — 외부 네트워크에 노출되지 않음 |
| WAL 모드 | SQLite의 Write-Ahead Logging. CLI/GUI의 동시 읽기·쓰기를 안전하게 처리 |
| rusqlite (bundled) | 시스템에 SQLite 설치 없이 C 소스를 함께 빌드하는 임베디드 SQLite 크레이트 feature |
| axum | 로컬 HTTP API 서버 구현에 쓰는 경량 Rust 웹 프레임워크 |
| launchd / systemd / Task Scheduler | macOS / Ubuntu / Windows의 OS 네이티브 서비스 매니저. 엔진 자동시작·크래시 재시작을 위임하는 대상 |
| ADR | Architecture Decision Record. 결정당 1파일, 불변 — [adr/index](../adr/index) 참조 |
