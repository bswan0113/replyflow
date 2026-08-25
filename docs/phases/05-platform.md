# 5단계 — 플랫폼 선정

## 목표

1단계에서 가결정(provisional)했던 플랫폼 후보/분량 유형/사업성을, 세계관(3단계)·캐릭터(4단계)·플롯(3단계)이 갖춰진 지금 시점에서 재검토해 확정한다. 플랫폼 선정은 세계관·플롯·캐릭터와 달리 한 번 확정하고 넘어가는 성격이므로, init/update 이원구조를 적용하지 않고 단일 패스로 진행한다. 항목별 재협상 대신, 재검토 결과를 요약해 사용자에게는 "이대로 확정하고 진행할지" 하나의 go/no-go만 묻는다.

## 진입

`.claude/skills/novel-platform/SKILL.md`를 호출한다. 4단계가 끝난 김에 같은 세션에서 이어서 불러도 되고, 세션이 끊긴 뒤 나중에 다시 불러도 된다 — 어느 쪽이든 이 스킬이 유일한 진입점이다.

## 절차

1. `projects/<slug>/01-idea/synopsis.md`(가결정 내용), `02-world/worldbuilding.md`, `03-characters/characters.md`, `04-outline/plot.md`를 읽는다.
2. **가능하다면** (로컬 세션이고 Claude 데스크톱/Codex의 브라우저 접근이 있다면) 가결정 플랫폼의 최신 연재규칙을 호출 세션이 직접 조사한다. 조사 결과를 텍스트로 정리해둔다. 브라우저 접근이 없는 세션(예: 이 클라우드 빌드 세션)이라면 조사를 생략하고, 생략했다는 사실을 그대로 다음 단계에 넘긴다.
3. `platform-scout` 서브에이전트를 호출한다. 1~2에서 모은 자료(조사 결과가 있다면 그것도 프롬프트에 포함)를 전달하면, 이 서브에이전트는 "가결정을 그대로 확정할지, 다른 후보로 조정할지"를 판단해 근거와 함께 돌려준다. 이 서브에이전트는 웹 조사를 하지 않는다 — 순수하게 이미 모인 자료를 바탕으로 판단만 한다.
4. 호출 세션이 이 판단을 요약해 사용자에게 보여주고, **"이대로 확정하고 진행할지"** 하나만 묻는다. 항목(플랫폼/분량/사업성)별로 따로 재협상하지 않는다. 연재규칙 조사를 생략했다면 이 요약에 반드시 "미검증(unverified)" 표시를 포함한다.
5. 사용자가 승인하면 6번으로. 사용자가 "아니오"라고 하면, 이 지점부터는 예외적으로 세부 항목별 논의로 들어간다(플랫폼/분량/사업성 중 무엇이 걸리는지 확인하고 조정).
6. `project.yaml`을 갱신한다:
   ```yaml
   platform:
     confirmed: "..."      # 최종 확정 플랫폼
     verified: true/false  # 연재규칙을 실제로 조사했으면 true, 생략했으면 false
   business_model: "..."   # 최종 확정
   length_type: "..."      # 최종 확정
   status: 6
   stage_history:
     - stage: 5
       entered_at: "..."
       note: "플랫폼 확정. verified=<true/false>"
   ```
7. `projects/<slug>/04-outline/platform-notes.md`에 확정 사유와 (조사했다면) 연재규칙 메모를 기록한다. `verified: false`인 경우, "미검증 상태로 확정됨 — 실제 게시(7·8단계) 전 반드시 최신 연재규칙을 재확인할 것"이라고 명시한다.

## 산출물

- `project.yaml`의 `platform.confirmed`/`platform.verified`/`business_model`/`length_type`
- `projects/<slug>/04-outline/platform-notes.md`

## 주의

`platform.verified`가 `false`인 채로 7·8단계(게시 관련)에 진입해서는 안 된다 — 실제 게시 전에는 반드시 연재규칙을 재확인해 `verified: true`로 갱신해야 한다.
