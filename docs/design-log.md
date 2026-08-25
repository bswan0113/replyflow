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

**추가 확인** (1단계 작업 중): 이후 세션에서 `harness-reviewer`를 실제로 Agent 툴에서 호출해 정상 동작을 확인함. 2번 항목의 조건부 사유 해소.

---

## 1단계 — 아이디어 구축

**제안된 작업방식**: 사용자가 떠올린 장면/소재 하나를 자유형식으로 전달 → 1차평가 → 시놉시스 단계까지 기획 진행 → 플랫폼 선정·작품 길이(연재/중단편)·사업성(취미용/게임화용/유료판매용)까지 진행 → 사용자 컨펌 → 최종평가 → 다음 단계.

**평가 결과 (1차, `harness-reviewer` 호출)**:

1. 목적적합성: 반려 — 기존 1단계 산출물(로그라인 5~8개 발산) 정의와 어긋나고, 2단계(평가)·5단계(플랫폼선정) 산출물까지 한 번에 흡수함.
2. 실행가능성: 통과 — 전 과정이 대화형 텍스트 작업이라 API 키/브라우저 없이 로컬에서 재현 가능.
3. 생산성: 반려 — 세계관·캐릭터 확정 전에 플랫폼·사업성을 완전히 확정하면, 이후 결과에 따라 번복해야 할 재작업 위험이 큼.
4. 일관성: 반려 — `CLAUDE.md` 표, `00-foundation.md` 폴더 매핑, `project.yaml` 주석(플랫폼은 5단계에서 확정)과 충돌. `business_model` 필드가 스키마에 없음.

**종합 판정**: 반려.

**개선 제안 (리뷰어)**: (A) 플랫폼·사업성 판단을 5단계로 완전히 미룬다 / (B) 1단계에서는 "가결정"만 하고 5단계에서 재검토해 확정한다.

**사용자 선택**: B.

**최종 승인안**: 사용자가 원한 흐름(소재→1차평가→시놉시스→플랫폼/분량/사업성 논의→컨펌→최종평가)을 그대로 유지하되, 1단계에서 나온 플랫폼/분량/사업성은 모두 가결정(provisional)으로 표시하고 5단계에서 재검토해 확정한다. 옛 2단계(평가)는 별도 진입점 없이 1단계의 1차평가·최종평가로 흡수 — 파이프라인 번호(0~10) 자체는 재배치하지 않는다. 생성 파일: `docs/phases/01-idea.md`, `.claude/agents/idea-evaluator.md`, `.claude/skills/novel-idea/SKILL.md`, `CLAUDE.md` 표 갱신, `project.yaml`(`business_model`/`length_type`/`platform.provisional` 필드 추가), `docs/phases/00-foundation.md` 스키마 설명 동기화.

**완성도 재평가** (`harness-reviewer` 실호출):

**종합 판정**: 통과. 4항목 모두 통과 — 승인된 산출물이 빠짐없이 생성됐고, 옛 2단계용 별도 진입점이 남아있지 않으며, `idea-evaluator`/`harness-reviewer` 역할 구분이 명확하고, 이전 반려 사유 4가지가 모두 해소됨을 확인.

사소한 개선 제안 반영: `stage_history`의 `stage`는 완료한 단계, `status`는 다음 단계를 가리킬 수 있다는 점을 `00-foundation.md`에 명시.

---

## 3단계 — 세계관·플롯

**제안된 작업방식**: 한 번에 완벽한 설계를 기대하지 않음. 초기설계는 Claude/Codex 중 성과 좋은 쪽이 자유롭게 진행하거나 사용자가 뼈대를 직접 던지는 등 형식 제약 없이 진행. 세계관은 특히 보완·수정이 잦을 것으로 예상되므로 초기설계용과 확장(보충/수정)용 진입점을 분리해, 집필 등 다른 단계 세션에서도 확장 쪽을 자유롭게 호출 가능하게 함. 단, 실제 변경 반영에는 항상 사용자 승인 전제. 후속 확인에서 플롯(전체아크·회차별비트)에도 동일한 이원화를 적용하기로 함.

**평가 결과 (1차, `harness-reviewer` 호출)**:

1. 목적적합성: 통과 — 세계관/플롯 모두 초안 확립 + 지속적 보완이라는 실제 요구에 부합.
2. 실행가능성: 통과 — "쓰기 권한 없는 제안 전용 서브에이전트 + 승인 후 호출 세션이 직접 반영" 구조는 `idea-evaluator`에서 이미 검증된 패턴 재사용.
3. 생산성: 통과 — 제안 전용 서브에이전트가 사용자의 문서 재검토 수고를 줄이고, `project.yaml` 스키마 확장 없이 `changelog.md`만 두어 과설계를 억제.
4. 일관성: 반려 — 최초 구체화안이 실질 절차를 `SKILL.md`에 직접 담으려 해서 "스킬은 얇게, 실제 지침은 `docs/phases/*.md`에" 컨벤션 및 `novel-idea/SKILL.md` 선례와 충돌. `docs/phases/03-*.md` 신설 계획이 누락돼 있었음.

**종합 판정**: 반려 (일관성 항목만).

**개선 반영**: `docs/phases/03-world.md`, `docs/phases/03-plot.md`를 신설해 초기설계 최소요건과 확장 절차(트리거·제안 형식·승인·changelog 기록)를 담고, `SKILL.md`는 `novel-idea`와 같은 형식으로 얇게 재작성.

**최종 승인안**: 세계관·플롯 각각 초기설계(Init, 자유형식)와 확장(Update, 쓰기권한 없는 제안 전용 서브에이전트)을 분리. 생성 파일: `docs/phases/03-world.md`, `docs/phases/03-plot.md`, `.claude/skills/novel-world-init/SKILL.md`, `.claude/skills/novel-plot-init/SKILL.md`, `.claude/agents/worldbuilder-update.md`, `.claude/agents/plot-architect-update.md`, `docs/phases/00-foundation.md`에 세계관/플롯 변경 승인원칙 한 줄 추가(단계 번호 지칭 없는 일반형), `CLAUDE.md` 3행 갱신.

**완성도 재평가** (`harness-reviewer` 실호출, 1차):

**종합 판정**: 반려 (일관성 항목만). 목적적합성/실행가능성/생산성 모두 통과, 이전 반려 사유(SKILL.md 비대화, 03-*.md 누락)도 완전히 해소 확인. 다만 **새 일관성 문제**를 발견: `00-foundation.md`의 "폴더↔단계" 매핑 표(0단계 때 작성된 초안)가 이번 3단계 최종 설계와 어긋남 — `02-world/` 행이 "3(세계관·플롯)"으로 돼 있어 플롯도 이 폴더에 있는 것처럼 읽히지만 실제로는 `worldbuilding.md`만 여기 있고, `04-outline/` 행은 "회차별 비트 세부화"만 언급해 실제로 `plot.md`에 함께 들어가는 "전체 아크 요약"이 빠져 있었음.

**개선 반영**: `00-foundation.md` 폴더 매핑 표를 `02-world/` → "3(세계관)", `04-outline/` → "3(플롯): 전체 아크 요약 + 회차별 비트, 5(플랫폼)의 선정 결과 메모"로 수정.

**완성도 재평가 (2차, `harness-reviewer` 실호출)**: 통과. 4항목 모두 통과 — 폴더 매핑 표 수정이 제안대로 정확히 반영됐고, `03-world.md`/`03-plot.md`의 최소요건·산출물 절과 완전히 일치함을 확인. 수정 과정에서 다른 행이나 `CLAUDE.md`와 새로운 충돌도 없음. 3단계 완성도 재평가 종합 판정: 통과.

---

## 4단계 — 캐릭터 생성

**제안된 작업방식**: "3단계랑 동일하게 가면 될듯" — 3단계에서 승인된 초기설계(Init, 자유형식)+확장(Update, 쓰기권한 없는 제안 전용 서브에이전트, 언제든 호출 가능, 승인 후에만 반영) 이원 구조를 캐릭터 생성에도 그대로 적용.

**평가 결과 (`harness-reviewer` 호출)**:

1. 목적적합성: 통과 — 초기설계+확장 구조가 4단계 목표(캐릭터 프로필·관계도 확립 + 지속적 보완)에 부합.
2. 실행가능성: 통과 — `worldbuilder-update`/`plot-architect-update`와 동일한 읽기전용 제안형 패턴, 3단계에서 이미 실호출 검증됨.
3. 생산성: 통과 — 제안 전용 서브에이전트 + `changelog.md`만 추가하는 구조로 과설계 억제. 관계도를 텍스트로 충분하다고 명시해 불필요한 포맷 도입 방지.
4. 일관성: 통과 — 폴더 매핑(`03-characters/` 행)은 이미 정확해 추가 수정 불필요. 스킬은 얇게, 실질 절차는 `docs/phases/`에 두는 패턴과 네이밍 규칙(`character-designer-update`, `novel-characters-init`) 모두 3단계 선례와 일치. 세계관/플롯과 달리 캐릭터는 단일 파일·단일 Init/Update로 처리한 것도 불필요한 분할을 피한 적절한 단순화로 확인.

**종합 판정**: 통과 (1차에 바로 통과, 재설계 불필요).

**최종 승인안**: `docs/phases/04-characters.md`, `.claude/skills/novel-characters-init/SKILL.md`, `.claude/agents/character-designer-update.md` 신규 생성. `CLAUDE.md` 4행을 3행과 동일한 서술 형식으로 갱신.

**완성도 재평가** (`harness-reviewer` 실호출): 통과. 4항목 모두 통과 — `04-characters.md`가 `03-world.md`/`03-plot.md`와 문단 구조 1:1 대응, `character-designer-update.md`가 `worldbuilder-update.md`와 frontmatter·출력형식·승인문구까지 동일 패턴, `novel-characters-init/SKILL.md`도 `novel-world-init`과 동형, `CLAUDE.md` 4행이 3행과 서술 형식 일치, `design-log.md` 최종승인안과 실제 생성 파일 목록 정확히 일치. 새로운 충돌 없음.

---

## 5단계 — 플랫폼 선정

**제안된 작업방식**: "여긴 내가 개입할 부분이 없을 듯. 4단계까지 끝나면 기초 기획은 나온 거니까, 자동으로 진입해서 프로젝트 진행 여부만 결정해주면 될 것 같은데?" — 세부 항목(플랫폼/분량/사업성)을 재협상하지 않고, 기존 자료 기반 자동 재검토 후 사용자에게는 단일 go/no-go만 요청.

**평가 결과 (1차, `harness-reviewer` 호출)**:

1. 목적적합성: 통과 — 자동 재검토+단일 go/no-go 구조가 1단계에서 합의한 "5단계에서 재검토해 확정"의 취지를 형식적으로 흘려보내지 않음.
2. 실행가능성: 반려 — (a) `platform-scout`의 tools(Read/Grep/Glob)로는 웹 조사가 불가능한데 절차는 "실제로 조사한다"고 명시해 모순. (b) "자동 진입" 메커니즘이 불명확 — 세션이 끊긴 뒤 재진입할 경로(전용 스킬 등)가 없음.
3. 생산성: 통과 — 항목별 재협상을 단일 go/no-go로 압축하면 승인 부담이 실제로 줄어듦 (단, 2번 결함 해소가 전제).
4. 일관성: 반려 — 1~4단계 모두 예외 없이 전용 `SKILL.md` 진입점을 뒀는데 이번만 빠뜨림. (참고: init/update 이원구조를 적용하지 않은 판단 자체는 "한 번 확정하는 성격"이라는 근거가 있어 통과로 인정됨.)

**종합 판정**: 반려 (실행가능성·일관성).

**개선 반영**: 웹 조사는 호출 세션이 직접 수행(가능한 경우)하고, `platform-scout`은 조사 결과+기존 문서를 입력받아 "확정/조정 필요"만 판단하는 순수 읽기전용 역할로 재조정(tools는 Read/Grep/Glob 유지). `.claude/skills/novel-platform/SKILL.md` 신설로 기존 4단계와 동일한 진입 패턴 확보. 조사를 생략한 경우 `platform.verified: false` 플래그를 남기고, 7·8단계(게시) 진입 전 재검증을 요구하는 문구를 `05-platform.md`에 명시.

**최종 승인안**: `docs/phases/05-platform.md`, `.claude/skills/novel-platform/SKILL.md`, `.claude/agents/platform-scout.md` 신규 생성. `project.yaml`/`00-foundation.md`에 `platform.verified` 필드 추가. `CLAUDE.md` 5행 갱신.

**완성도 재평가**: (구현 완료 후 이어서 기록)
