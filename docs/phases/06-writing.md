# 6단계 — 집필

## 목표

회차(화) 단위로 원고를 완성한다. 집필과 자기교정은 전부 지금 활성화된 세션이 직접 수행하며, 별도 서브에이전트에 위임하지 않는다. 회차가 쌓여도 다음 회차를 쓸 때 필요한 맥락을 빠르게 복원할 수 있도록, 매 회차 종료 시 핵심 내용을 요약해 누적 문서에 남긴다.

## "단일 세션" 원칙

이 회차의 집필과 자기교정을 부속 서브에이전트(Agent 툴)에 위임하지 않고, 현재 활성 세션이 직접 수행한다는 뜻이다. 여러 회차에 걸쳐 같은 대화가 끊기지 않고 계속 이어질 필요는 없다 — 새 세션에서 시작해도 `summaries.md`와 기존 산출물 파일들을 읽으면 맥락을 복원할 수 있다.

이 원칙의 예외는 `worldbuilder-update`/`plot-architect-update`/`character-designer-update`뿐이다. 이 셋은 집필 작업 자체를 위임하는 게 아니라, 3~5단계에서 이미 확립된 "세계관/플롯/캐릭터 문서 보완 제안" 절차를 재사용하는 것이므로 이번 단계에서도 필요하면 그대로 호출한다.

## 진입

`.claude/skills/novel-write/SKILL.md`를 호출한다.

## 절차 (회차당)

1. **맥락 복원**: `projects/<slug>/05-manuscript/summaries.md`(있으면)를 읽는다. 없으면(1화라면) `01-idea/synopsis.md`, `02-world/worldbuilding.md`, `03-characters/characters.md`, `04-outline/plot.md`를 읽는다.
2. **이번 회차 비트 확인**: `04-outline/plot.md`에서 이번 회차가 담당할 사건을 확인한다.
3. **초고 작성**: 이 세션이 직접 쓴다.
4. **자기교정** (최소요건 — 매 회차 반드시 점검):
   - 문체/시점 일관성 (`project.yaml`의 `style_guide` 준수)
   - 이전 회차·세계관·캐릭터·플롯과 모순되는 부분이 없는지
   - 분량이 `style_guide.chapter_length_chars` 근처인지
   - 회차 말미에 다음 화로 이어지는 훅이 있는지
5. **필요시 세계관/플롯/캐릭터 보완**: 자기교정 중 기존 설정과 안 맞는 지점을 발견했다면, 이 시점에 `worldbuilder-update`/`plot-architect-update`/`character-designer-update` 중 해당하는 서브에이전트를 호출해 제안을 받고, 사용자 승인 후에만 반영한다.
6. **저장**: `projects/<slug>/05-manuscript/ch<NNN>.md`로 저장한다 (`NNN`은 3자리 회차 번호, 예: `ch001.md`).
7. **요약 누적**: `projects/<slug>/05-manuscript/summaries.md`에 이번 회차 섹션을 추가한다 — 핵심 사건, 새로 심어진 떡밥, 이번 화에서 회수된 떡밥, 세계관·플롯·캐릭터 변화, 다음 화로 이어지는 훅. 그리고 파일 맨 위의 "떡밥 추적 표"를 갱신한다.

## `summaries.md` 구조

파일 맨 위에 항상 떡밥 추적 표를 둔다:

```
## 떡밥 추적 표

| 떡밥 | 설치 회차 | 회수 회차 | 상태 |
|------|-----------|-----------|------|
| ...  | ch003     | ch017     | 회수됨 |
| ...  | ch012     | -         | 미회수 |
```

그 아래에 회차별 섹션을 최신 화부터(또는 오래된 순, 프로젝트마다 택일해 일관되게) 나열한다:

```
## ch<NNN>
- 핵심 사건: ...
- 새로 심어진 떡밥: ...
- 회수된 떡밥: ...
- 설정 변화: ...
- 다음 화 훅: ...
```

## 확장성 규칙 (최소요건)

`summaries.md`의 회차 섹션이 40화를 넘으면:
1. 가장 오래된 구간(예: ch001~ch020)을 `projects/<slug>/05-manuscript/summaries-archive/ch001-020.md`로 분리 저장한다. 내용은 그대로 옮긴다.
2. 활성 `summaries.md`에는 최근 20화의 상세 회차 섹션만 남기고, 그 이전 회차들은 압축 색인(회차 번호 + 핵심 사건 한 줄)으로 축약한다.
3. **떡밥 추적 표는 아카이브 여부와 무관하게 항상 활성 `summaries.md` 맨 위에 전체를 유지한다** — 표만 보면 몇 화짜리 떡밥이든 미해결 여부를 바로 확인할 수 있어야 한다.

이렇게 하면 회차가 아무리 늘어나도 매 회차 세션이 읽어야 하는 `summaries.md`의 크기가 일정 범위로 유지된다.

## 산출물

- `projects/<slug>/05-manuscript/ch<NNN>.md` (회차 원고)
- `projects/<slug>/05-manuscript/summaries.md` (활성 누적 요약 + 떡밥 추적 표)
- `projects/<slug>/05-manuscript/summaries-archive/ch<NNN>-<NNN>.md` (40화 초과 시 생성되는 과거 구간 아카이브)
