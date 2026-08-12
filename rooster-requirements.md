# rooster — requirements

> 통합 스냅샷: 세분화 원본은 해당 영역의 index를 참조하세요.

## 전체 개요

게임 특화 일정 관리 유틸리티. 반복 숙제(일일/주간/월간)와 일회성 이벤트를 등록·관리하고, 마감 임박 시 OS 네이티브 알림으로 알린다. 데스크톱 전용, 로컬 알림만 사용. 핵심 가치("등록 → 마감 임박 알림")는 CLI만으로 완전히 검증 가능해야 한다. → [상세](requirements/overview/rooster-req-overview)

## 게임/반복 숙제 등록 및 관리

게임 등록이 숙제 등록보다 선행(참조 무결성). 반복 숙제는 일일/주간/월간 주기, 완료 처리 후 다음 주기에 재등장. `game add/list/rm`, `add`, `list`, `done`, `rm` 커맨드로 관리. → [상세](requirements/game-task/rooster-req-game-task)

## 기간 한정 일회성 이벤트

`--period once --deadline`으로 등록하는 일회성 일정. 반복 숙제와 동일한 커맨드 체계를 공유하되 완료 후 다음 주기가 생성되지 않고, 마감 경과 후 미완료 시 자동 삭제 없이 overdue 상태로 계속 표시된다. → [상세](requirements/once-event/rooster-req-once-event)

## 마감 임박 알림

엔진이 백그라운드 스케줄 체크 루프로 `notify-before` 시점에 도달한 숙제를 OS 네이티브 토스트로 알린다. 순간 이벤트 알림이며, 상시 열람용 오버레이 GUI(후순위)와는 목적이 다르다. → [상세](requirements/notification/rooster-req-notification)

## CLI 파일 입출력 (import/export)

JSON 기반 벌크 export/import. `games` 섹션 존재 여부로 백업 복원과 신규 벌크 등록이 플래그 없이 자연히 구분된다. → [상세](requirements/cli-io/rooster-req-cli-io)

## 엔진 상태 확인

트레이 아이콘만으로는 놓치기 쉬운 "엔진이 조용히 죽어있는" 최악의 실패 모드를 `status` 커맨드로 능동 확인. 프로세스 생존과 스케줄러 루프 동작을 분리해서 판단(마지막 스케줄 체크 시각). → [상세](requirements/status/rooster-req-status)

## 지원 플랫폼 범위

Windows/macOS/Ubuntu만 지원. 모바일은 백그라운드 상주 제약 충돌로 스코프 제외. → [상세](requirements/platform/rooster-req-platform)

## 배포 방식

주 사용자는 본인이지만 불특정 다수 배포 가능성을 염두에 두고 안정성 우선 기술 선택. 배포 채널 자체는 미정(후순위). → [상세](requirements/distribution/rooster-req-distribution)
