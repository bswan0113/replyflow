---
name: novel-publish
description: 8단계(게시) 진입점. essentials.md 내용을 확정 플랫폼에 실제로 게시한다. 브라우저 조작 도구가 있으면 직접 채우고, 없으면 체크리스트로 대체한다. 최종 게시/약관동의는 항상 사용자가 직접 클릭한다.
---

이 스킬은 `docs/phases/08-publish.md`의 절차를 그대로 따른다.

절차 요약(자세한 내용은 `docs/phases/08-publish.md` 참고):

1. `project.yaml`의 `platform.verified`를 확인한다. `false`면 7단계(`novel-publish-assets`)로 돌아가 재검증하도록 안내하고 중단한다.
2. `06-publish/essentials.md`, `04-outline/platform-notes.md`를 읽는다.
3. 확정 플랫폼에 접속한다.
4. 브라우저 조작 도구가 있으면 직접 필드를 채우고, 없으면 체크리스트를 출력해 사용자가 복사/붙여넣기 하도록 한다.
5. 최종 게시 버튼·약관동의는 항상 사용자가 직접 클릭 — 세션은 그 직전에서 멈춘다.
6. 사용자가 게시 완료를 확인하면 `project.yaml`(`stage_history`/`status: 9`)과 `06-publish/publish-record.md`를 갱신한다.
