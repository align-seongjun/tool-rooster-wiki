# 언어/저장소 스택 (Rust, SQLite)

## 개요

엔진 언어는 Rust, 데이터 저장소는 SQLite로 확정했다.

## 결정 사항

### 엔진 언어: Rust

- 대안(Go)과의 진짜 차이는 "메모리 안전성"보다 **동시성 안전성**에 있음: Go의 GC는 버퍼 오버플로우/댕글링 포인터는 막아주지만 goroutine 간 data race는 컴파일 타임에 잡지 못한다(`-race` 플래그로 런타임에만 탐지). Rust의 borrow checker는 data race를 컴파일 타임에 원천 차단한다.
- CLI/GUI가 엔진에 동시 요청을 보내는 이 프로젝트 구조와 맞물려 실질적 이점이 있고, 불특정 다수 배포 가능성까지 고려하면 안정성 이점이 개발 속도보다 우선 → Rust로 확정.

### 데이터 저장소: SQLite

대안(JSON/TOML 평문 파일) 대비 이점:
- 벌크 인서트를 트랜잭션으로 원자적 처리(중간 실패 시 롤백, 파일 손상 위험 없음)
- "마감 임박 숙제만" 같은 필터링을 SQL 쿼리로 위임 가능
- WAL 모드 등으로 CLI/GUI의 동시 읽기·쓰기를 안전하게 처리
- 컬럼 타입/제약 조건으로 데이터 무결성 보장, 필드 추가 시 마이그레이션으로 관리
- rusqlite/sqlx 등 Rust 생태계 성숙, 별도 서버 없이 파일 하나로 임베디드 동작

데이터 규모가 커질수록(다중 게임/캐릭터, 완료 이력 등) SQLite 쪽이 유리하다고 판단해 확정.

## 제약사항

- Rust 크레이트: 스캐폴드 단계에서 `clap`(CLI), `axum`+`tokio`(HTTP API), `rusqlite`(bundled feature, 임베디드 SQLite), `serde`/`serde_json`(JSON I/O), `chrono`(시간 처리)를 초기 의존성으로 선정 ([tool-rooster-engine/Cargo.toml] 참조, 실제 구현 중 조정 가능)

## 관련 ADR

- [ADR-002: 엔진 언어 Rust 선택](../../adr/002-engine-language-rust)
- [ADR-003: 데이터 저장소 SQLite 선택](../../adr/003-storage-sqlite)
