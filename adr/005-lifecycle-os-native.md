# ADR-005: 엔진 생명주기 OS 네이티브 서비스 매니저 위임

- **상태**: Accepted
- **일자**: 2026-08-13

## 배경

엔진의 자동시작과 크래시 재시작을 어떻게 보장할지 결정해야 했다.

## 결정

커스텀 워치독을 직접 구현하지 않고 OS 네이티브 서비스 매니저에 위임한다 — macOS: launchd, Ubuntu: systemd, Windows: Task Scheduler/Windows Service.

## 검토한 대안

- **자체 워치독 구현**: 3개 OS 각각의 프로세스 감시/재시작 로직을 직접 구현·검증해야 해서 기술부채가 크고, 이미 각 OS가 제공하는 검증된 재시작 정책보다 신뢰성이 낮을 가능성이 높다.

## 결과

- OS별 서비스 등록 절차(launchd plist, systemd unit, Windows 서비스 등록)를 각각 구현해야 함
- 트레이 아이콘만으로는 "죽어있는 엔진"을 놓치기 쉬우므로, 보완 수단으로 `status` CLI 커맨드를 둠 ([lifecycle](../architecture/lifecycle/rooster-arch-lifecycle) 참조)
