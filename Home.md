# 게임 숙제 관리 유틸리티 — 문서 허브

---

## rooster

### 읽기 순서

처음 접하는 개발자는 아래 순서를 따르세요:

1. **[용어 사전](glossary/rooster-glossary)** — 도메인·기술 용어 파악
2. **[요구사항 명세](rooster-requirements)** — 무엇을 만드는지 이해
3. **[아키텍처](rooster-architecture)** — 어떻게 설계했는지 이해
4. **[ADR](adr/index)** — 왜 이렇게 결정했는지 이해
5. **[개발 가이드라인](rooster-development-guidelines)** — 코딩 규칙 숙지
6. **[개발 계획](plan/index)** — 구현 순서와 Phase별 범위 파악
7. **[진행 상태](progress)** — 현재 어디까지 됐는지 확인

---

### 핵심 문서 (통합 스냅샷)

전체 내용을 한 파일에서 볼 수 있는 통합 문서입니다.

| 문서 | 설명 |
|------|------|
| [요구사항 명세](rooster-requirements) | 기능 요구사항 전체 |
| [아키텍처](rooster-architecture) | 기술 설계 전체 |
| [개발 가이드라인](rooster-development-guidelines) | 코딩 규칙 전체 |

### 세분화 문서 (영역별 버전 관리)

영역별로 독립 변경 이력을 추적합니다. 파일명은 날짜 없이 안정적으로 유지하고, 실제로 개정이 일어날 때만 기존 파일을 `_archive/`로 옮깁니다(아래 갱신 규칙 참고).

| 인덱스 | 영역 수 | 프리픽스 |
|--------|--------|---------|
| [requirements/index](requirements/index) | 8개 | `rooster-req-` |
| [architecture/index](architecture/index) | 6개 | `rooster-arch-` |
| [guidelines/index](guidelines/index) | 4개 | `rooster-guide-` |
| [plan/index](plan/index) | 8개 | `rooster-plan-` |

> **통합 vs 세분화**: 통합 문서는 전체를 빠르게 파악할 때, 세분화 문서는 특정 영역의 변경 이력을 추적할 때 사용합니다. **세분화 문서가 원본**이며, 통합 문서는 스냅샷입니다. 세분화 문서 변경 후 통합 문서도 갱신해야 합니다.

### 보조 문서

| 문서 | 설명 | 관리 방식 |
|------|------|----------|
| [개발 계획](plan/index) | Phase별 구현 계획 | 세분화 (Phase별 독립 파일) |
| [진행 상태](progress) | 현재 Phase, 다음 작업, 변경 로그 | **가변 문서** (직접 갱신) |
| [ADR 인덱스](adr/index) | 아키텍처 결정 기록 | 결정당 1파일 (불변) |
| [용어 사전](glossary/rooster-glossary) | 도메인·기술 용어 정의 | 버전 관리 (개정 시 구버전 아카이빙) |
| 환경 설정 가이드 | 빌드 도구, 실행 명령어 등 | Phase 0 완료 후 작성 |

---

### 문서 갱신 규칙

1. **세분화 영역 변경**: 기존 파일을 같은 폴더의 `_archive/{파일명}-{YYYY-MM-DD-HHmm}.md`로 이동(개정 시점 타임스탬프) → 같은 경로에 원래 파일명 그대로 새 내용 생성 → 인덱스 설명 갱신(경로 자체는 안정적이라 보통 안 바뀜) → 통합 스냅샷 갱신
2. **ADR 추가**: `adr/` 폴더에 새 파일 생성 → `adr/index.md` 목록 추가
3. **진행 상태 갱신**: `progress.md` 직접 수정 (유일한 가변 문서)
4. **개발 계획 변경**: `plan/` 해당 Phase 폴더의 파일을 1번 규칙대로 아카이빙 후 재생성 → `plan/index.md` 갱신
5. **용어 추가/수정**: `glossary/` 폴더의 파일을 1번 규칙대로 아카이빙 후 재생성
