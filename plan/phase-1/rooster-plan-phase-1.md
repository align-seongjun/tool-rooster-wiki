# Phase 1 — 데이터 모델 + 엔진 코어

**목표**: SQLite 스키마(`games`/`tasks`/`completions`)를 구현하고, 게임/숙제 CRUD 로직을 엔진 코어에 갖춘다 ([data-model 아키텍처](../../architecture/data-model/rooster-arch-data-model) 참조).

---

## 작업 항목

1. SQLite 연결/마이그레이션 초기화 — DB 파일 경로 결정, 스키마 생성
2. `games` CRUD — 등록/조회/삭제, 삭제 시 하위 숙제 인터랙티브 확인 + `--cascade` 로직
3. `tasks` CRUD — 반복(`daily`/`weekly`/`monthly`) + `once` 등록/조회/삭제, `games` 참조 무결성 검증
4. `completions` 로그 기반 "현재 주기 완료 여부" 판정 로직 — 별도 플래그 없이 로그 존재 여부로 판단

---

## 완료 기준

- 각 CRUD 로직에 대한 유닛 테스트(`cargo test`)가 인메모리 또는 임시 파일 DB로 통과
- 존재하지 않는 게임을 참조하는 숙제 등록 시도가 에러로 막힘
