# Phase 4 — 스케줄링 + 알림

**목표**: 마감 임박 판정 루프와 OS 네이티브 알림 발송을 구현한다 ([notification 요구사항](../../requirements/notification/rooster-req-notification) 참조).

---

## 작업 항목

1. 스케줄 체크 루프 — 주기적 tick, "마지막 스케줄 체크 시각" 갱신(`status`에 반영)
2. `notify-before` 임박 판정 로직
3. OS 네이티브 알림 발송 연동 — 크레이트 조사 후 개발 머신(macOS) 우선 구현
4. Windows/Ubuntu 알림 API 분기 확장

---

## 완료 기준

- 실제 마감 임박 시점에 OS 알림이 화면에 뜨는 것을 확인 — 자동화 스크립트로 짧은 주기를 설정해 등록부터 알림 발송까지 전체 흐름을 구동해서 관찰(개별 컴포넌트 단위 검증만으로 완료 처리하지 않음)
- 최근 알림 발송 이력이 `status` 출력에 반영됨
