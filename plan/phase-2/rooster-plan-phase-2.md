# Phase 2 — 로컬 HTTP API

**목표**: axum 기반 로컬 HTTP API(127.0.0.1 loopback)로 Phase 1의 엔진 코어 기능을 노출한다 ([api 아키텍처](../../architecture/api/rooster-arch-api) 참조).

---

## 작업 항목

1. axum 서버 부트스트랩 — `rooster serve`에서 기동, 포트 고정 기본값 + 설정파일/환경변수 오버라이드
2. 게임 CRUD 엔드포인트
3. 숙제 CRUD 엔드포인트 (반복 + once)
4. `status` 엔드포인트 — 엔진 상태/가동시간/마지막 스케줄 체크 시각/등록 수/DB 경로/API 포트

---

## 완료 기준

- `curl`로 각 엔드포인트를 왕복 호출해 정상 응답 확인
- axum 테스트 클라이언트(`oneshot` 등)로 라우팅/핸들러 자동화 테스트 통과
