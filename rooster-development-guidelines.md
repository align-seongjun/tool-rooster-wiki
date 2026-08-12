# rooster — development-guidelines

> 통합 스냅샷: 세분화 원본은 해당 영역의 index를 참조하세요.

## Rust 코드 컨벤션

`cargo build`/`clippy`/`fmt` 경고 0개 목표. 엔진/CLI 로직은 단일 바이너리 안에서 분리. 에러 처리는 외부 경계(입력/파일/DB/HTTP)에서만, `unwrap()`은 지양. → [상세](guidelines/rust-conventions/rooster-guide-rust-conventions)

## 테스트 전략

커밋 단위는 `cargo test`로 검증(DB는 인메모리/임시 파일 사용). API는 실제 HTTP 요청으로 검증. 여러 상태 전이가 필요한 기능(등록→알림 발송 등)은 골든 패스 전체를 자동화 스크립트로 구동해 확인. → [상세](guidelines/testing/rooster-guide-testing)

## 커밋 규칙

영어로 작성, `Co-Authored-By: Claude`는 사용자 요청 시에만 포함. 최소 커밋 단위 + 파일 그룹별 사유 명시. GitHub Flow 브랜치 전략. → [상세](guidelines/commit/rooster-guide-commit)

## 참고 자료

원본 기획 논의는 위키 밖 별도 노트 폴더에 있으나 이 위키에는 경로를 하드링크하지 않는다 — 위키 문서가 항상 최신 확정 스펙. → [상세](guidelines/references/rooster-guide-references)
