---
name: novel-publish-assets
description: 7단계(게시 필수요소) 진입점. 소개글/태그/표지문구 초안을 자동 생성하고 단일 go/no-go로 확정한다. platform.verified가 false면 진입 전 별도 동의를 구한다.
---

이 스킬은 `docs/phases/07-publish-assets.md`의 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/07-publish-assets.md` 참고):

1. 시놉시스·세계관·캐릭터·플롯·`platform-notes.md`(있으면 회차 요약도)를 읽는다.
2. `project.yaml`의 `platform.verified`를 확인한다. `false`면 가능하면 재조사하고, 안 되면 **미검증 예외 진행에 대한 별도 동의**를 먼저 구한다(초안 승인과는 다른 질문).
3. `publish-assistant` 서브에이전트를 호출해 제목 후보·소개글·태그·표지문구 초안과 `docs/style/ai-smell.md` 기준 자가점검 결과를 받는다.
4. 자가점검에 반려 항목이 있으면 사용자에게 보여주고 재작성 여부를 묻는다 — 원하면 `publish-assistant`를 다시 호출한다(최대 3회, `docs/style/ai-smell.md` 기준). 3회를 넘겨도 반려면 사용자에게 진행 여부를 명시적으로 묻는다.
5. 사용자에게 단일 go/no-go로 확정 여부만 묻는다.
6. 승인되면 `06-publish/essentials.md`에 저장하고, `platform.verified` 상태에 따라 `project.yaml`의 `status`를 8로 올리거나(검증됨) 7에 유지한다(미검증 예외 진행).
