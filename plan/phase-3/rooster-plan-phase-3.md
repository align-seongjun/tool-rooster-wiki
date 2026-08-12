# Phase 3 — CLI 클라이언트

**목표**: `main.rs`의 CLI 서브커맨드 스텁이 실제로 Phase 2의 로컬 API를 호출해 동작하도록 구현한다.

---

## 작업 항목

1. HTTP 클라이언트 연동(reqwest 등)을 각 서브커맨드(`game add/list/rm`, `add`, `list`, `done`, `rm`, `status`)에 연결
2. `import`/`export` — JSON 벌크 인서트/덤프 ([cli-io 요구사항](../../requirements/cli-io/rooster-req-cli-io) 참조)
3. `list --overdue` 필터링 — once 이벤트의 overdue 상태 포함

---

## 완료 기준

- 엔진을 `serve`로 기동한 상태에서, CLI로 "게임 등록 → 숙제 등록 → 조회 → 완료 처리 → 삭제" 전체 흐름이 실제로 동작
- `export` → `import` 왕복 시 데이터가 손실 없이 복원됨
