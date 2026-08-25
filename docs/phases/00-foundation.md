# 0단계 — 하네스 기반구조

## 목표

이후 모든 단계(1~10)가 따를 공통 구조를 확립한다: 디렉토리 스켈레톤, 프로젝트 상태 스키마(`project.yaml`), 문서/파일 컨벤션, 그리고 메타 빌드 루프를 실행할 `harness-reviewer` 서브에이전트.

## 디렉토리 구조

```
CLAUDE.md                          # 하네스 전체 개요 + 메타 루프 요약 + 단계 목차
docs/
  design-log.md                    # 결정 로그
  phases/
    00-foundation.md               # 이 문서
    NN-<slug>.md                   # 단계별 상세 스펙 (승인될 때마다 추가)
.claude/
  agents/
    harness-reviewer.md            # 루브릭 기반 평가 서브에이전트
    (이후 단계별 서브에이전트 추가)
  skills/
    (이후 단계별 SKILL.md 추가, 예: novel-new/SKILL.md)
projects/
  _TEMPLATE/                       # 신규 프로젝트 복제용 템플릿
    project.yaml
    01-idea/
    02-world/
    03-characters/
    04-outline/
    05-manuscript/
    06-publish/
    07-feedback/
  <slug>/                          # 실제 소설 프로젝트 (템플릿 복제 후 생성)
```

`projects/<slug>/NN-*` 폴더 번호는 `project.yaml`의 파이프라인 단계(1~10)와 대응한다. 단, 폴더는 7개뿐이므로 다음과 같이 매핑한다:

| 폴더 | 대응 단계 |
|------|-----------|
| `01-idea/` | 1(아이디어) + 2(평가) 결과 |
| `02-world/` | 3(세계관) |
| `03-characters/` | 4(캐릭터) |
| `04-outline/` | 3(플롯): 전체 아크 요약 + 회차별 비트, 5(플랫폼)의 선정 결과 메모 |
| `05-manuscript/` | 6(집필) 회차 원고 |
| `06-publish/` | 7(게시 필수요소) + 8(게시) 기록 |
| `07-feedback/` | 9(관리 통계) + 10(피드백) |

## `project.yaml` 스키마

```yaml
title: ""              # 작품 제목 (가제 가능)
slug: ""                # 디렉토리명과 동일, kebab-case
genre: ""                # 예: 현대판타지, 로맨스판타지 등
platform:
  target: []              # 후보 플랫폼 목록 (1단계에서 초안, 5단계에서 재확인)
  provisional: null        # 1단계 가결정 플랫폼 (5단계에서 재검토 대상)
  confirmed: null          # 최종 선정 플랫폼 (5단계 완료 시 확정)
business_model: null       # hobby | game_adaptation | paid_serial — 1단계 가결정, 5단계 확정
length_type: null          # serial | novella — 1단계 가결정, 5단계 확정
status: 0                 # 현재 진행 중인 파이프라인 단계 번호 (0~10)
stage_history:            # 단계 전환 로그
  - stage: 0
    entered_at: ""        # ISO 8601
    note: ""
style_guide:
  pov: ""                  # 시점 (1인칭/3인칭 등)
  tone: ""                 # 문체 톤
  chapter_length_chars: null  # 회차 목표 분량(자수)
created_at: ""
updated_at: ""
```

- `status`는 항상 파이프라인 표(CLAUDE.md)의 단계 번호와 일치시킨다.
- 단계를 넘어갈 때마다 `stage_history`에 항목을 추가하고 `status`를 갱신한다.
- `stage_history`의 각 항목은 **완료한 단계 번호**를 기록한다. 그 시점의 `status`는 이미 **다음 단계 번호**로 갱신돼 있을 수 있다 (예: 1단계를 완료하면 `stage_history`에 `stage: 1` 항목이 추가되고, `status`는 3으로 넘어간다). 즉 `status`와 `stage_history` 마지막 항목의 `stage` 값이 다른 것은 정상이다.
- `platform.confirmed`가 정해지기 전까지 7·8단계(게시 관련) 작업은 시작하지 않는다.
- 세계관/플롯 변경 제안은 어느 단계의 세션에서 호출되든, 파일 수정 전 반드시 사용자 승인을 거친다.

## 컨벤션

- **언어**: 모든 하네스 문서와 소설 프로젝트 산출물은 한국어를 기본으로 작성한다.
- **도구 중립성**: `docs/phases/*.md`는 Claude Code 전용 문법(예: 서브에이전트 frontmatter)이나 Codex 전용 문법을 쓰지 않는다. 사람이 읽고 그대로 실행할 수 있는 절차형 지침으로 작성해서, Claude Code에서는 서브에이전트/스킬이 이를 읽어 수행하고 Codex에서는 사용자가 이 문서를 프롬프트로 넘겨 동일하게 재현할 수 있게 한다.
- **서브에이전트 vs 스킬**: `.claude/agents/*.md`는 특정 역할(발산적 아이디어 생성, 평가 등)을 맡는 Claude Code 전용 서브에이전트 정의다. `.claude/skills/*/SKILL.md`는 사용자가 슬래시 커맨드로 부르는 단계 진입점이며, 내부적으로 해당 서브에이전트를 호출하거나 `docs/phases/*.md` 절차를 따른다. 스킬 파일 자체는 얇게 유지하고 실질 지침은 `docs/phases/`에 둔다.
- **네이밍**: 프로젝트 슬러그·파일명은 kebab-case. 단계 스펙 문서는 `NN-<slug>.md` (NN은 두 자리 단계 번호).
- **커밋 단위**: 하네스 구축 커밋과 실제 소설 프로젝트 산출물 커밋을 섞지 않는다.

## `harness-reviewer` 서브에이전트

메타 빌드 루프의 3단계(작업방식 평가)와 7단계(완성도 재평가)에서 호출된다.

**입력**: (a) 평가 대상 — 제안된 작업방식 설명, 또는 완성된 산출물(파일 경로 목록); (b) 어느 단계에 대한 평가인지.

**루브릭** (4항목, 항목별 통과/반려 + 사유):

1. 목적적합성 — 해당 단계의 목표에 실제로 부합하는가
2. 실행가능성 — 로컬 Claude Code/Codex 환경에서 API 키 없이 실제로 동작 가능한가
3. 생산성 — 사용자의 반복 노동을 실제로 줄이는가
4. 일관성 — 이미 승인된 다른 단계 설계(`docs/design-log.md`에 기록된 것들)와 충돌하지 않는가

**출력 형식**: 항목별 통과/반려와 사유, 종합 판정(통과/반려), 반려 시 구체적 개선 제안.

정의 파일: `.claude/agents/harness-reviewer.md`.

## 0단계 자체의 평가 (부트스트랩)

`harness-reviewer`가 아직 존재하지 않으므로, 0단계에 한해 위 루브릭을 Claude가 직접 적용해 자체 점검한다. 결과는 `docs/design-log.md`에 기록한다. 1단계부터는 실제 서브에이전트를 호출한다.
