---
name: novel-characters-init
description: 4단계(캐릭터 생성) 초기설계 진입점. 형식 제약 없이 주인공·조연·빌런 프로필과 관계도를 만들어 characters.md 최소요건을 채운다.
---

이 스킬은 `docs/phases/04-characters.md`의 초기설계 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/04-characters.md` 참고):

1. `projects/<slug>/01-idea/synopsis.md`, `02-world/worldbuilding.md`, `04-outline/plot.md`(있는 만큼)를 참고한다.
2. 진행 방식은 자유 — 사용자가 캐릭터를 먼저 던지든, 이 세션이 제안을 먼저 하든 상관없다.
3. `projects/<slug>/03-characters/characters.md`에 최소요건(주인공/조연·빌런 프로필, 관계도)을 채운다.

이후 캐릭터를 추가로 보완·수정할 때는 이 스킬을 다시 쓰지 않고 `character-designer-update` 서브에이전트를 호출한다 (`docs/phases/04-characters.md`의 "확장" 절차 참고).
