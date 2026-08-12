# 전체 구조 (엔진/CLI/GUI 분리)

## 개요

Rust 스케줄러 엔진을 백그라운드 프로세스로 상주시키고 로컬 API를 제공한다. CLI와 GUI는 둘 다 그 API를 호출하는 클라이언트로 분리한다.

## 결정 사항

- **엔진/클라이언트 분리**: 평소엔 GUI를 띄우지 않고 엔진만 상주 — 메모리 절약의 핵심은 "연산 분리" 자체가 아니라 **무거운 GUI를 상시 띄워둘 필요가 없다는 점**(엔진 자체 연산 비용은 미미함). 이전 시도(Flutter 단일 앱)는 실행이 무거워 기각.
- **단일 바이너리 + 서브커맨드**: `docker`/`dockerd` 패턴(엔진/CLI 바이너리 분리)을 검토했으나, 바이너리를 둘로 나누면 빌드/서명/배포 부담이 배가되므로 하나로 통합 — `rooster serve`가 엔진 모드, 나머지 서브커맨드가 CLI 모드. 커맨드 목록은 요구사항 문서(예: [game-task](../../requirements/game-task/rooster-req-game-task)) 참조.
- **GUI는 세 번째 클라이언트**: 엔진 API를 재사용하는 구조라 상호작용형/오버레이형 GUI 추가 시에도 엔진 자체는 변경 불필요 ([gui-spike](../gui-spike/rooster-arch-gui-spike) 참조).

## 관련 ADR

- [ADR-001: 엔진/CLI 단일 바이너리 통합](../../adr/001-single-binary)
