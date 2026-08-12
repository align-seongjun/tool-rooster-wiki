# 로컬 HTTP API

## 개요

엔진 ↔ CLI/GUI 통신은 로컬 HTTP API(127.0.0.1 loopback)로 처리한다.

## 결정 사항

- **Unix 소켓/Windows named pipe 대신 로컬 HTTP API 채택**: 3개 OS에서 플랫폼별 분기 없이 동일 코드로 처리 가능(axum 등 경량 Rust 프레임워크), `curl` 등으로 테스트도 용이.
- **루프백 바인딩**: 외부 네트워크 노출 없음.
- **GUI도 동일 API 재사용**: GUI가 세 번째 클라이언트로 붙을 때도 별도 API를 만들지 않는다.
- **포트**: 고정 기본값 + 충돌 시 설정 파일/환경변수로 오버라이드. 동적 포트 할당은 개인용 유틸리티 규모에 비해 과한 복잡도라 채택하지 않음.

## 제약사항

- 엔드포인트 상세 스펙(경로, 요청/응답 스키마)은 Phase 2(로컬 HTTP API) 구현 시 확정 — 현재는 CLI 서브커맨드가 호출할 기능 단위만 결정된 상태 ([game-task](../../requirements/game-task/rooster-req-game-task), [cli-io](../../requirements/cli-io/rooster-req-cli-io) 요구사항 참조)

## 관련 ADR

- [ADR-004: 엔진-클라이언트 통신 로컬 HTTP API 채택](../../adr/004-local-http-api)
