# Phase 5 — 엔진 생명주기 (OS 서비스 등록)

**목표**: 자동시작 + 크래시 재시작을 OS 네이티브 서비스 매니저에 위임한다 ([lifecycle 아키텍처](../../architecture/lifecycle/rooster-arch-lifecycle), [ADR-005](../../adr/005-lifecycle-os-native) 참조).

---

## 작업 항목

1. macOS launchd plist 작성 + 등록/해제 절차
2. Ubuntu systemd unit 작성 + 등록/해제 절차
3. Windows 서비스 등록 (Task Scheduler 또는 Windows Service)
4. `status` 커맨드에 "마지막 스케줄 체크 시각" 기반 이상 탐지 반영 확인 (프로세스는 떠 있으나 루프가 멈춘 상태 구분)

---

## 완료 기준

- 3개 OS 각각에서 엔진 프로세스를 강제 종료한 뒤 OS 서비스 매니저가 자동으로 재시작하는 것을 확인
- 재부팅 시 엔진이 자동으로 기동하는 것을 확인
