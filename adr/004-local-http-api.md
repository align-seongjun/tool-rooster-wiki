# ADR-004: 엔진-클라이언트 통신 로컬 HTTP API 채택

- **상태**: Accepted
- **일자**: 2026-08-13

## 배경

상주 엔진과 CLI/GUI 클라이언트 간 통신 방식을 결정해야 했다. 3개 OS(Windows/macOS/Ubuntu)를 동일 코드로 지원해야 한다.

## 결정

로컬 HTTP API(127.0.0.1 loopback)를 채택한다. 포트는 고정 기본값 + 충돌 시 설정 파일/환경변수로 오버라이드한다.

## 검토한 대안

- **Unix 소켓 / Windows named pipe**: OS별로 구현이 다르므로 플랫폼 분기가 필요하다.
- **동적 포트 할당**: 개인용 유틸리티 규모에 비해 과한 복잡도라 채택하지 않음.

## 결과

- axum 등 경량 Rust 프레임워크로 3개 OS 동일 코드 처리 가능
- `curl` 등으로 수동 테스트 용이
- 루프백 바인딩이라 외부 네트워크 노출 없음
- GUI 스파이크를 포함한 세 번째 클라이언트도 동일 API 재사용 가능 ([api](../architecture/api/rooster-arch-api), [gui-spike](../architecture/gui-spike/rooster-arch-gui-spike) 참조)
