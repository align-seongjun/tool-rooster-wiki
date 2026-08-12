# Phase 0 — 프로젝트 셋업

**목표**: 개발 착수를 위한 레포/디렉토리/문서/툴체인 기반을 갖춘다.

---

## 작업 항목

- [x] 위키(`tool-rooster-wiki`) 스캐폴드 + 콘텐츠 작성(requirements/architecture/guidelines/plan)
- [x] Rust 툴체인 설치(rustup)
- [x] `tool-rooster-engine` cargo 프로젝트 생성, 초기 의존성(clap/axum/tokio/rusqlite/serde/chrono) 추가, CLI 서브커맨드 스텁 작성
- [x] `tool-rooster-engine` git 초기 커밋 (`030f5ac`)
- [x] 프로젝트 CLAUDE.md 작성 (primary working directory, 섹션 0에 위키 허브 링크)
- [x] `tool-rooster-wiki` git 초기 커밋 (`a173178`)

---

## 완료 기준

- `cargo build`가 `tool-rooster-engine`에서 경고 없이 성공
- `tool-rooster-engine`, `tool-rooster-wiki` 각각 git 초기 커밋 존재
- 프로젝트 CLAUDE.md의 섹션 0이 위키 허브(`Home.md`)를 가리킴
