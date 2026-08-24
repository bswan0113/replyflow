# 결정 로그

하네스를 확장할 때마다(메타 빌드 루프 적용 시) 단계별로 기록한다.

---

## 0단계 — 하네스 기반구조

**제안된 작업방식**: Claude가 표준 초안을 제시 → 사용자가 검토/수정.

**평가 결과** (부트스트랩 — `harness-reviewer`가 아직 없어 Claude가 직접 루브릭 적용):

1. 목적적합성: 통과 — 기반구조는 표준적인 스캐폴딩 작업이라 Claude가 초안을 제시하고 사용자가 검토하는 방식이 목표(공통 구조 확립)에 부합함.
2. 실행가능성: 통과 — 마크다운/YAML 파일 생성뿐이라 로컬 Claude Code/Codex 어디서든 그대로 재현 가능.
3. 생산성: 통과 — 사용자가 매 항목을 처음부터 나열할 필요 없이 초안만 검토하면 되어 반복 노동이 적음.
4. 일관성: 통과 — 최초 단계라 비교 대상 없음.

**종합 판정**: 통과.

**최종 승인안**: 아래 구조를 그대로 생성.
- `CLAUDE.md`, `docs/design-log.md`, `docs/phases/00-foundation.md`
- `.claude/agents/harness-reviewer.md`
- `projects/_TEMPLATE/` (project.yaml + 7개 하위 폴더)

**완성도 재평가** (부트스트랩 — `harness-reviewer`를 Agent 툴로 호출 시도했으나, 이번 세션은 파일 생성 이전에 시작되어 서브에이전트가 핫리로드되지 않음 `Agent type 'harness-reviewer' not found`. 정의 파일 자체는 표준 Claude Code 서브에이전트 frontmatter 형식을 따르므로, 다음 로컬 세션(재시작 후)에서 실제 호출 테스트가 필요. 그 전까지 Claude가 직접 루브릭 적용):

1. 목적적합성: 통과 — CLAUDE.md/design-log.md/00-foundation.md/harness-reviewer.md/project.yaml/7개 하위 폴더가 모두 실제로 생성되었고, 0단계 목표(공통 구조 확립)를 그대로 충족.
2. 실행가능성: 조건부 통과 — 모든 파일이 순수 마크다운/YAML이라 로컬에서 그대로 재현 가능. 다만 `harness-reviewer` 서브에이전트는 이번 세션에서 인식되지 않았으므로, 실제 호출 가능 여부는 다음 로컬 세션에서 재확인 필요.
3. 생산성: 통과 — 이후 모든 단계가 이 스켈레톤/스키마/컨벤션을 그대로 재사용하므로 반복 설계 비용을 없앰.
4. 일관성: 통과 — 위 "최종 승인안"과 실제 생성 결과가 일치. 기존 index.html/README.md는 변경하지 않음(`git status`로 확인).

**종합 판정**: 조건부 통과 (harness-reviewer 실동작은 다음 세션에서 확인).
