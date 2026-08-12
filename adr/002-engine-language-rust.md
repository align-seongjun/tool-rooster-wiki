# ADR-002: 엔진 언어 Rust 선택

- **상태**: Accepted
- **일자**: 2026-08-13

## 배경

CLI/GUI가 엔진에 동시 요청을 보내는 구조라 동시성 안전성이 중요하고, 불특정 다수 배포 가능성도 있어 안정성이 개발 속도보다 중요할 수 있다.

## 결정

엔진 언어로 Rust를 채택한다.

## 검토한 대안

- **Go**: 개발 속도는 더 빠르다. 하지만 GC가 버퍼 오버플로우/댕글링 포인터는 막아줘도 goroutine 간 data race는 컴파일 타임에 잡지 못한다(`-race` 플래그로 런타임에만 탐지 가능). Rust의 borrow checker는 data race를 컴파일 타임에 원천 차단한다는 점이 이 프로젝트(다중 클라이언트의 동시 요청)에 실질적 이점.

## 결과

- 개발 속도는 Go 대비 느릴 수 있으나, 동시성 버그를 컴파일 타임에 잡을 수 있음
- 크로스 컴파일(Windows/macOS/Ubuntu) 툴체인 관리가 필요 ([platform 요구사항](../requirements/platform/rooster-req-platform) 참조)
