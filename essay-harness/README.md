# 에세이 하네스

짧은 블로그 포스팅용 에세이를 쓰기 위한 가벼운 작업 폴더.

## 사용법

Claude Code에서 `/essay`를 호출하면 `.claude/skills/essay/SKILL.md`에 정의된 흐름을 따라
소재구상 → 초안 → 퇴고 → 발행준비 순으로 대화하며 에세이를 완성한다.

에세이 한 편은 `essays/<slug>.md` 파일 하나로 관리되며, 파일 상단 frontmatter의
`status` 값이 현재 진행 단계를 나타낸다. 그 외 별도의 상태 관리 파일이나
서브에이전트, changelog는 두지 않는다.

새 에세이를 시작하려면 `/essay`로 바로 시작하거나, `essays/`에 새 파일을 만들고
frontmatter만 채운 뒤 불러오면 된다.
