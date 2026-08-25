---
name: novel-write
description: 6단계(집필) 진입점. 회차 단위로 원고를 쓴다. 집필·자기교정은 현재 세션이 직접 수행하며 서브에이전트에 위임하지 않는다.
---

이 스킬은 `docs/phases/06-writing.md`의 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/06-writing.md` 참고):

1. `05-manuscript/summaries.md`(있으면) 또는 시놉시스·세계관·캐릭터·플롯을 읽어 맥락을 복원한다.
2. `04-outline/plot.md`에서 이번 회차 비트를 확인한다.
3. 이 세션이 직접 초고를 쓰고, 직접 자기교정한다(문체/모순/분량/훅, 그리고 AI 냄새 판정 — 전부 최소요건). AI 냄새 판정은 `docs/style/ai-smell.md` 기준으로 최대 3회까지 반려·재작성을 반복하는 게이트다 — 통과(또는 3회 상한 후 사용자 승인) 없이는 5번(저장)으로 진행하지 않는다.
4. 세계관·플롯·캐릭터 보완이 필요하면 해당 update 서브에이전트를 예외적으로 호출해 제안받고, 사용자 승인 후 반영한다.
5. `05-manuscript/ch<NNN>.md`로 저장하고, `summaries.md`에 회차 섹션 + 떡밥 추적 표를 갱신한다.
6. `summaries.md`가 40화를 넘으면 `docs/phases/06-writing.md`의 확장성 규칙(아카이빙)을 따른다.
