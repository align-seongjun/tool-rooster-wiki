# 지원 플랫폼 범위

## 개요

데스크톱 전용(Windows/macOS/Ubuntu). 모바일(iOS/Android)은 스코프 제외한다.

## 기능 요구사항

### FR-PLATFORM-001: 3개 데스크톱 OS 지원
- **우선순위**: P0
- **설명**: 엔진/CLI/(후순위)GUI가 Windows, macOS, Ubuntu에서 동일하게 동작한다.
- **수용 기준**: 동일 코드베이스가 3개 OS에서 빌드되고, 로컬 HTTP API·SQLite·알림 기능이 플랫폼별 분기 없이(또는 최소 분기로) 동작한다.

## 제약사항

- 모바일 제외 이유: "엔진 상주 + API 제공" 구조가 iOS/Android의 백그라운드 프로세스 제약(배터리/리소스 정책상 OS의 강한 상주 제한)과 근본적으로 충돌. 포괄하려면 플랫폼별로 스케줄링/알림 방식을 이원화해야 해서 기술부채가 커짐
- 엔진 자동시작/재시작은 OS 네이티브 서비스 매니저(macOS: launchd, Ubuntu: systemd, Windows: Task Scheduler/Windows Service)에 위임 ([lifecycle](../../architecture/lifecycle/rooster-arch-lifecycle) 참조)
