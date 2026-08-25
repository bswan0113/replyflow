---
name: novel-idea
description: 1단계(아이디어 구축) 진입점. 사용자가 소재/장면을 던지면 시놉시스+플랫폼/분량/사업성 가결정까지 진행한다.
---

이 스킬은 `docs/phases/01-idea.md`의 절차를 그대로 따른다. 신규 프로젝트라면 먼저 `projects/_TEMPLATE/`을 `projects/<slug>/`로 복제하고 `project.yaml`을 채운 뒤 시작한다.

절차 요약(자세한 내용은 `docs/phases/01-idea.md` 참고):

1. 사용자가 전달한 소재를 그대로 기록한다.
2. `idea-evaluator` 서브에이전트를 **1차평가** 모드로 호출한다. 보완요청이면 사용자에게 더 생각해볼 지점을 전달하고 다시 소재를 받는다.
3. 통과하면 시놉시스 템플릿을 채워 발전시킨다.
4. 플랫폼 후보·분량 유형·사업성을 사용자와 논의해 가결정한다.
5. 시놉시스+가결정을 정리해 사용자 컨펌을 받는다.
6. `idea-evaluator`를 **최종평가** 모드로 호출한다. "재검토"면 지적된 지점(시놉시스 또는 가결정 논의)으로 돌아간다.
7. "진행" 판정을 받으면 `projects/<slug>/01-idea/synopsis.md`와 `evaluation.md`를 저장하고, `project.yaml`을 `docs/phases/01-idea.md`의 "project.yaml 갱신" 절에 따라 갱신한다.
