---
name: novel-world-init
description: 3단계(세계관) 초기설계 진입점. 형식 제약 없이 세계관 초안을 만들어 worldbuilding.md 최소요건을 채운다.
---

이 스킬은 `docs/phases/03-world.md`의 초기설계 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/03-world.md` 참고):

1. 사용자가 던진 뼈대(있다면)와 `projects/<slug>/01-idea/synopsis.md`를 참고한다.
2. 진행 방식은 자유 — 사용자가 초안을 먼저 던지든, 이 세션이 제안을 먼저 하든 상관없다.
3. `projects/<slug>/02-world/worldbuilding.md`에 최소요건(핵심 설정, 시스템 규칙, 시놉시스와의 모순 점검)을 채운다.

이후 세계관을 추가로 보완·수정할 때는 이 스킬을 다시 쓰지 않고 `worldbuilder-update` 서브에이전트를 호출한다 (`docs/phases/03-world.md`의 "확장" 절차 참고).
