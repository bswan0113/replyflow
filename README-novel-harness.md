# 소설 작업 통합 하네스

웹소설 창작의 전 과정(아이디어→평가→세계관/플롯→캐릭터→플랫폼 선정→집필→게시 필수요소→게시→관리→피드백)을 지원하는 개인용 로컬 하네스입니다. Claude Code와 Codex CLI를 API 키 없이, 단계별로 자유롭게 번갈아 사용합니다.

> 이 파일은 새 저장소(`novel-harness`)를 만드셨을 때 `README.md`로 옮겨 쓰시라고 미리 준비해둔 초안입니다.

## 파이프라인

| # | 단계 | 진입 스킬 | 상태 |
|---|------|-----------|------|
| 0 | 하네스 기반구조 | - | 완료 |
| 1 | 아이디어 구축 | `/novel-idea` | 완료 |
| 2 | 평가 | (1단계에 통합) | - |
| 3 | 세계관·플롯 | `/novel-world-init`, `/novel-plot-init` | 완료 |
| 4 | 캐릭터 생성 | `/novel-characters-init` | 완료 |
| 5 | 플랫폼 선정 | `/novel-platform` | 완료 |
| 6 | 집필 | `/novel-write` | 완료 |
| 7 | 게시 필수요소 | `/novel-publish-assets` | 완료 |
| 8 | 게시 | `/novel-publish` | 완료 |
| 9 | 관리·피드백 | `/novel-feedback` | 완료 |
| 10 | 피드백 | (9단계에 통합) | - |

각 단계의 상세 절차는 `docs/phases/NN-*.md`에 있습니다. 스킬은 얇은 진입점이고, 실제 절차는 전부 `docs/phases/`에 있어서 Claude Code든 Codex든(사람이 절차 문서를 프롬프트로 넘겨) 동일하게 재현할 수 있습니다.

## 시작하기 (신규 소설 프로젝트)

1. `projects/_TEMPLATE/`을 `projects/<작품-slug>/`로 복제
2. `project.yaml`을 채운다 (제목, 장르, 문체 등)
3. `/novel-idea`부터 순서대로 진행

여러 작품을 동시에 진행해도 됩니다 — 하네스 본체(`CLAUDE.md`, `.claude/`, `docs/`)는 모든 프로젝트가 공유하고, 작품별 데이터만 `projects/<slug>/`로 나뉩니다.

## 서브에이전트

| 이름 | 역할 |
|------|------|
| `harness-reviewer` | 하네스 자체를 확장/수정할 때 설계·완성도를 평가 (실제 창작에는 쓰지 않음) |
| `idea-evaluator` | 소재/시놉시스 1차평가·최종평가 |
| `worldbuilder-update` | 세계관 보완·수정 제안 (언제든 호출 가능, 제안만 함) |
| `plot-architect-update` | 플롯 보완·수정 제안 |
| `character-designer-update` | 캐릭터 보완·수정 제안 |
| `platform-scout` | 플랫폼 확정 여부 판단 (웹조사는 호출 세션이 담당) |
| `publish-assistant` | 소개글/태그/표지문구 초안 생성 |
| `feedback-analyst` | 독자 댓글을 칭찬/비판/떡밥예측/오류지적으로 분류·요약 |

`worldbuilder-update`/`plot-architect-update`/`character-designer-update`는 읽기 전용이며, 실제 문서 반영은 항상 사용자 승인을 거친 뒤 호출한 세션이 직접 수행합니다.

## 설계 원칙

- 하네스 자체를 확장할 때는 "제안 → `harness-reviewer` 평가 → 사용자 승인 → 구현 → 완성도 재평가"라는 메타 빌드 루프를 거칩니다. 모든 결정은 `docs/design-log.md`에 기록돼 있습니다.
- 게시 관련 최종 클릭(게시 버튼, 약관 동의)은 항상 사용자가 직접 합니다.
- 플랫폼 연재규칙처럼 실시간 확인이 필요한 정보는 로컬 세션(브라우저 접근 가능)에서만 검증되며, 미검증 상태로는 게시 단계에 진입하지 않도록 게이트가 걸려 있습니다(`project.yaml`의 `platform.verified`).

## 문서

- `CLAUDE.md` — 하네스 전체 개요 + 메타 빌드 루프
- `docs/phases/*.md` — 단계별 상세 절차 (도구 중립)
- `docs/design-log.md` — 단계별 설계 결정 기록
