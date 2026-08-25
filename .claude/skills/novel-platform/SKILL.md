---
name: novel-platform
description: 5단계(플랫폼 선정) 진입점. 1단계의 가결정(플랫폼/분량/사업성)을 세계관·캐릭터·플롯이 갖춰진 지금 재검토해 확정한다. 항목별 재협상 없이 단일 go/no-go로 진행한다.
---

이 스킬은 `docs/phases/05-platform.md`의 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/05-platform.md` 참고):

1. 시놉시스·세계관·캐릭터·플롯을 모두 읽는다.
2. 가능하면(로컬 세션, 브라우저 접근 있음) 가결정 플랫폼의 최신 연재규칙을 직접 조사한다. 안 되면 생략하고 그 사실을 남긴다.
3. `platform-scout` 서브에이전트를 호출해 확정할지 조정할지 판단을 받는다.
4. 사용자에게 세부 재협상 없이 "이대로 확정하고 진행할지" 하나만 묻는다 (조사를 생략했다면 "미검증" 표시 포함).
5. 승인되면 `project.yaml`(`platform.confirmed`/`platform.verified`/`business_model`/`length_type`/`status: 6`)과 `04-outline/platform-notes.md`를 갱신한다. 거절되면 세부 항목별 논의로 들어간다.
