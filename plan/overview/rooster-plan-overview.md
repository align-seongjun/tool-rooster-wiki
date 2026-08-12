# rooster 개발 계획 — Overview

## 컨텍스트

게임 특화 일정 관리 유틸리티. MVP 범위는 엔진 + CLI로 한정하고, 본격 GUI(상호작용형/오버레이형)는 후순위로 미룬다 — 핵심 가치("등록 → 마감 임박 알림")가 CLI만으로 완전히 검증 가능하기 때문. GUI 프레임워크 선정 같은 본격 설계 없이, 엔진 API 계약만 조기 검증하는 최소 스파이크(정적 HTML+JS)는 엔진/CLI와 병렬로 진행한다 ([gui-spike 아키텍처](../../architecture/gui-spike/rooster-arch-gui-spike) 참조).

바이너리 이름은 `rooster`로 가배정(추후 변경 가능, [게임/반복 숙제 요구사항](../../requirements/game-task/rooster-req-game-task) 및 프로젝트 레포 `tool-rooster-engine`에서 빌드).

---

## 패키지 목록

| 패키지 | 용도 | 도입 시점 |
|--------|------|----------|
| clap (derive) | CLI 서브커맨드 파싱 | Phase 0 |
| axum | 로컬 HTTP API 서버 | Phase 0 (의존성만), Phase 2 (실제 라우팅) |
| tokio (rt-multi-thread, macros) | axum 실행에 필요한 비동기 런타임 | Phase 0 (의존성만), Phase 2 |
| rusqlite (bundled) | 임베디드 SQLite, 시스템 SQLite 설치 불필요 | Phase 0 (의존성만), Phase 1 |
| serde / serde_json (derive) | JSON 직렬화 (import/export, API body) | Phase 0 (의존성만), Phase 1 |
| chrono (serde) | 시간대/일정 계산 | Phase 0 (의존성만), Phase 1 |

---

## 디렉토리 구조

```
tool-rooster-engine/
├── Cargo.toml
└── src/
    ├── main.rs       # 엔트리포인트, clap 서브커맨드 정의 및 디스패치
    ├── cli.rs         # CLI 서브커맨드 → 로컬 API 호출 (Phase 3)
    ├── db/            # SQLite 스키마·쿼리 (Phase 1)
    ├── engine/         # 스케줄러 루프, 알림 발송 (Phase 4)
    └── api/            # axum 라우터/핸들러 (Phase 2)
```

Phase 0에서는 `main.rs` 하나에 서브커맨드 스텁만 존재. 위 모듈 분할은 초기 제안이며 Phase 1 착수 시 실제 구현 편의에 맞게 조정 가능.

---

## 주요 기술 리스크

| 리스크 | 내용 | 대응 |
|--------|------|------|
| OS 네이티브 알림 API 차이 | Windows/macOS/Ubuntu 각각 토스트 알림 구현 방식이 다름 | Phase 4에서 크레이트 조사 후 플랫폼별 분기 최소화 시도, 안 되면 OS별 모듈 분리 |
| OS 서비스 매니저 등록 차이 | launchd/systemd/Task Scheduler 각각 설정 방식이 다름 ([ADR-005](../../adr/005-lifecycle-os-native)) | Phase 5에서 OS별 등록 스크립트/설정 파일 작성, 개발 머신(macOS) 우선 검증 |
| rusqlite bundled 크로스 컴파일 | `bundled` feature는 C 컴파일러 필요 — 크로스 컴파일 시 툴체인 이슈 가능 | Phase 1~5 진행하며 3개 OS 각각에서 실제 빌드 확인 |

---

## 단계별 요약

| Phase | 내용 | 플랫폼 |
|-------|------|--------|
| 0 | 프로젝트 셋업 | 개발 머신(macOS) |
| 1 | 데이터 모델 + 엔진 코어 | 개발 머신(macOS) |
| 2 | 로컬 HTTP API | 개발 머신(macOS) |
| 3 | CLI 클라이언트 | 개발 머신(macOS) |
| 4 | 스케줄링 + 알림 | 3개 OS (알림 API 분기) |
| 5 | 엔진 생명주기 (OS 서비스 등록) | 3개 OS (서비스 매니저 분기) |
| 6 | GUI 스파이크 | 개발 머신(macOS), 브라우저 |
