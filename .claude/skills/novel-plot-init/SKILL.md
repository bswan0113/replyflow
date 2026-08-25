---
name: novel-plot-init
description: 3단계(플롯) 초기설계 진입점. 형식 제약 없이 전체 아크와 초반 회차 비트를 만들어 plot.md 최소요건을 채운다.
---

이 스킬은 `docs/phases/03-plot.md`의 초기설계 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/03-plot.md` 참고):

1. `projects/<slug>/01-idea/synopsis.md`와 `projects/<slug>/02-world/worldbuilding.md`(있는 만큼)를 참고한다.
2. 진행 방식은 자유 — 사용자가 아크/비트를 먼저 던지든, 이 세션이 제안을 먼저 하든 상관없다.
3. `projects/<slug>/04-outline/plot.md`에 최소요건(전체 아크 요약, 최소 초반 10화 비트)을 채운다.

이후 플롯을 추가로 보완·수정할 때는 이 스킬을 다시 쓰지 않고 `plot-architect-update` 서브에이전트를 호출한다 (`docs/phases/03-plot.md`의 "확장" 절차 참고).
