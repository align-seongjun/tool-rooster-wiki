# rooster — architecture

> 통합 스냅샷: 세분화 원본은 해당 영역의 index를 참조하세요.

## 전체 구조 (엔진/CLI/GUI 분리)

Rust 스케줄러 엔진을 백그라운드 프로세스로 상주시키고 로컬 API를 제공, CLI와 GUI는 그 API를 호출하는 클라이언트로 분리. 단일 바이너리 + 서브커맨드(`rooster serve`가 엔진 모드) 구조로 `docker`/`dockerd` 패턴은 기각([ADR-001](adr/001-single-binary)). → [상세](architecture/overview/rooster-arch-overview)

## 언어/저장소 스택 (Rust, SQLite)

엔진 언어는 Rust(동시성 안전성이 Go 대비 결정 요인, [ADR-002](adr/002-engine-language-rust)), 저장소는 SQLite(트랜잭션/WAL/무결성이 평문 파일 대비 결정 요인, [ADR-003](adr/003-storage-sqlite)). 초기 의존성: clap, axum+tokio, rusqlite(bundled), serde/serde_json, chrono. → [상세](architecture/tech-stack/rooster-arch-tech-stack)

## 로컬 HTTP API

엔진 ↔ CLI/GUI 통신은 127.0.0.1 loopback HTTP API. Unix 소켓/named pipe 대비 플랫폼 분기가 없다는 게 결정 요인([ADR-004](adr/004-local-http-api)). 포트는 고정 기본값 + 오버라이드, 동적 할당은 미채택. → [상세](architecture/api/rooster-arch-api)

## DB 스키마

`games`(게임, 참조 무결성의 기준) / `tasks`(숙제, `daily`/`weekly`/`monthly`/`once`) / `completions`(완료 이력 로그, 플래그 대신 로그 존재 여부로 현재 주기 완료 판정) 3테이블. 시간대는 태스크별 오버라이드 없이 시스템 로컬 시간대로 통일. → [상세](architecture/data-model/rooster-arch-data-model)

## 엔진 생명주기

자동시작/크래시 재시작은 OS 네이티브 서비스 매니저(launchd/systemd/Task Scheduler)에 위임([ADR-005](adr/005-lifecycle-os-native)). "죽어있는 엔진"을 놓치지 않도록 `status` 커맨드로 마지막 스케줄 체크 시각을 능동 확인. → [상세](architecture/lifecycle/rooster-arch-lifecycle)

## GUI 스파이크

엔진/CLI와 병렬로 진행하는 최소 스파이크 — 정적 HTML+JS에서 `fetch()`로 로컬 API 직접 호출. 목적은 "API 설계가 실제로 동작하는가" 조기 검증이며 완성된 GUI 제공이 아님. 본격 상호작용형/오버레이형 GUI는 후순위. → [상세](architecture/gui-spike/rooster-arch-gui-spike)
