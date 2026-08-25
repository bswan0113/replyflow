# 에세이 하네스

짧은 블로그 포스팅용 에세이를 쓰기 위한 가벼운 작업 폴더.
클로드 코드, Codex 등 어떤 에이전트로도 쓸 수 있도록, 실제 진행 방식은 툴에 종속되지 않는
[`GUIDE.md`](./GUIDE.md) 하나에 정의되어 있다.

## 사용법

- 클로드 코드: `/essay`
- 다른 에이전트(Codex 등): `essay-harness/GUIDE.md`를 읽고 따르도록 지시하면 된다. 루트의 `AGENTS.md`가 진입점 역할을 한다.

## 구조

- `GUIDE.md` — 전체 진행 방식 (소재구상 → 집필 → 후작업 → 게시). 툴 무관, 실제 내용은 여기에만 있음.
- `.claude/skills/essay/SKILL.md` — 클로드 코드용 `/essay` 진입점. GUIDE.md를 가리키기만 함.
- `AGENTS.md` — 다른 에이전트용 진입점. GUIDE.md를 가리키기만 함.
- `essays/<slug>.md` — 에세이 한 편. frontmatter의 `status`(idea/draft/post/ready)로 진행 상태 추적.
- `essays/_log.md` — 후작업이 끝난 에세이의 기록. 소재구상 단계의 중복 확인과 후작업 단계의 카테고리·태그 정리가 이 파일 하나를 함께 쓴다.
- `EVAL_RUBRIC.md` — 집필 단계에서 초안을 통과/재작성 판정하는 고정 채점 기준. 평가자가 개선을 제안할 수 있지만 사용자 승인 없이는 스스로 고치지 않는다.

집필 단계의 평가 게이트 외에는 상태머신 파일, 서브에이전트 자동 호출, changelog를 두지 않는다.
