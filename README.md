# gstack (fork by @identity16)

> [Garry Tan](https://github.com/garrytan)의 [gstack](https://github.com/garrytan/gstack)을 포크하여 나만의 워크플로우에 맞게 커스터마이징한 버전입니다.

원본 gstack은 Claude Code를 가상 엔지니어링 팀으로 만들어주는 오픈소스 스킬 모음입니다. CEO가 제품을 재구성하고, 엔지니어링 매니저가 아키텍처를 잡고, 디자이너가 AI 슬롭을 잡아내고, 리뷰어가 프로덕션 버그를 찾고, QA가 실제 브라우저를 열어 테스트하고, 릴리즈 엔지니어가 PR을 올리는 — 슬래시 커맨드 하나로 동작하는 스프린트 시스템입니다.

**이 포크의 목표:** 원본의 강력한 스킬 시스템을 유지하면서, 내 개발 워크플로우와 선호에 맞게 다듬어 사용하는 것.

## Origin & Credit

이 프로젝트는 [garrytan/gstack](https://github.com/garrytan/gstack) (MIT License)의 포크입니다.

- **원본 저자:** [Garry Tan](https://x.com/garrytan) — Y Combinator President & CEO
- **원본 라이선스:** MIT (Copyright (c) 2026 Garry Tan)
- **업스트림 버전:** v0.12.5.0 기준 포크

원본 프로젝트의 철학과 핵심 구조에 대한 경의를 표합니다. Garry의 말처럼 — "Fork it. Improve it. Make it yours."

## Quick start

1. 이 포크를 설치 (30초)
2. `/office-hours` 실행 — 만들고 있는 것 설명
3. `/plan-ceo-review`로 아이디어 리뷰
4. `/review`로 코드 리뷰
5. `/qa`로 스테이징 테스트
6. `/ship`으로 PR 올리기

## Install

**요구사항:** [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [Git](https://git-scm.com/), [Bun](https://bun.sh/) v1.0+

### Step 1: 머신에 설치

Claude Code에서 아래를 붙여넣기:

> Install gstack: run **`git clone https://github.com/identity16/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup`** then add a "gstack" section to CLAUDE.md that says to use the /browse skill from gstack for all web browsing, never use mcp\_\_claude-in-chrome\_\_\* tools, and lists the available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /retro, /investigate, /document-release, /codex, /cso, /autoplan, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade.

### Step 2: 프로젝트에 추가 (선택)

> Add gstack to this project: run **`cp -Rf ~/.claude/skills/gstack .claude/skills/gstack && rm -rf .claude/skills/gstack/.git && cd .claude/skills/gstack && ./setup`** then add a "gstack" section to this project's CLAUDE.md with the available skills list.

### Codex, Gemini CLI, or Cursor

```bash
git clone https://github.com/identity16/gstack.git .agents/skills/gstack
cd .agents/skills/gstack && ./setup --host codex
```

또는 사용자 전역 설치:

```bash
git clone https://github.com/identity16/gstack.git ~/gstack
cd ~/gstack && ./setup --host auto
```

## The sprint

gstack은 도구 모음이 아니라 프로세스입니다:

**Think -> Plan -> Build -> Review -> Test -> Ship -> Reflect**

각 스킬이 다음 스킬에 연결됩니다. `/office-hours`가 디자인 문서를 쓰면 `/plan-ceo-review`가 읽고, `/plan-eng-review`가 테스트 계획을 쓰면 `/qa`가 가져갑니다.

| Skill | 역할 | 설명 |
|-------|------|------|
| `/office-hours` | **YC Office Hours** | 제품 프레이밍을 재구성하는 6가지 질문. 디자인 문서 생성. |
| `/plan-ceo-review` | **CEO / Founder** | 문제를 재정의. 10-star 제품 찾기. |
| `/plan-eng-review` | **Eng Manager** | 아키텍처, 데이터 플로우, 엣지 케이스 고정. |
| `/plan-design-review` | **Senior Designer** | 디자인 차원 0-10 평가. AI Slop 탐지. |
| `/design-consultation` | **Design Partner** | 디자인 시스템을 처음부터 구축. |
| `/review` | **Staff Engineer** | CI 통과하지만 프로덕션에서 터지는 버그 찾기. |
| `/investigate` | **Debugger** | 체계적 근본 원인 디버깅. |
| `/design-review` | **Designer Who Codes** | 디자인 감사 + 수정. |
| `/qa` | **QA Lead** | 실제 브라우저로 테스트, 버그 찾기, 수정, 재검증. |
| `/qa-only` | **QA Reporter** | 버그 리포트만 (코드 수정 없음). |
| `/cso` | **Chief Security Officer** | OWASP Top 10 + STRIDE 위협 모델. |
| `/ship` | **Release Engineer** | main 동기화, 테스트, 커버리지 감사, PR 생성. |
| `/land-and-deploy` | **Release Engineer** | PR 머지 -> CI/배포 대기 -> 프로덕션 확인. |
| `/canary` | **SRE** | 배포 후 모니터링 루프. |
| `/benchmark` | **Performance Engineer** | 페이지 로드, Core Web Vitals 비교. |
| `/document-release` | **Technical Writer** | 배포 후 문서 자동 업데이트. |
| `/retro` | **Eng Manager** | 주간 회고. `global` 모드로 전체 프로젝트 통합. |
| `/browse` | **QA Engineer** | 실제 Chromium 브라우저. ~100ms/커맨드. |
| `/setup-browser-cookies` | **Session Manager** | 실제 브라우저 쿠키 가져오기. |
| `/autoplan` | **Review Pipeline** | CEO -> design -> eng 리뷰 자동 파이프라인. |

### Power tools

| Skill | 설명 |
|-------|------|
| `/codex` | OpenAI Codex CLI로 독립적 코드 리뷰 (세컨드 오피니언). |
| `/careful` | 파괴적 명령 전 경고 (rm -rf, DROP TABLE, force-push). |
| `/freeze` | 파일 편집을 특정 디렉토리로 제한. |
| `/guard` | `/careful` + `/freeze` 동시 활성화. |
| `/unfreeze` | `/freeze` 해제. |
| `/setup-deploy` | `/land-and-deploy` 일회성 설정. |
| `/gstack-upgrade` | gstack 자체 업그레이드. |

## Upstream과의 차이점

이 포크에서 변경/추가한 사항:

- (아직 원본과 동일 — 커스터마이징 시작 시 여기에 기록)

업스트림 변경사항을 가져오려면:

```bash
# upstream 리모트 추가 (최초 1회)
git remote add upstream https://github.com/garrytan/gstack.git

# upstream 변경사항 가져오기
git fetch upstream
git merge upstream/main
```

## 기존 gstack 사용자를 위한 마이그레이션 가이드

원본 garrytan/gstack에서 이 포크로 전환하는 방법입니다.

### 전역 설치 전환 (`~/.claude/skills/gstack`)

```bash
# 1. 기존 설치 백업
mv ~/.claude/skills/gstack ~/.claude/skills/gstack-original

# 2. 이 포크로 설치
git clone https://github.com/identity16/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup

# 3. 정상 동작 확인
# Claude Code에서 /review, /ship 등 기존 스킬이 동작하는지 확인

# 4. 백업 제거 (확인 후)
rm -rf ~/.claude/skills/gstack-original
```

### 프로젝트 내 설치 전환 (`.claude/skills/gstack`)

```bash
# 1. 기존 것 제거
rm -rf .claude/skills/gstack

# 2. 이 포크로 교체
cp -Rf ~/.claude/skills/gstack .claude/skills/gstack
rm -rf .claude/skills/gstack/.git
cd .claude/skills/gstack && ./setup

# 3. 커밋
git add .claude/skills/gstack
git commit -m "chore: switch gstack to identity16 fork"
```

### Codex/Gemini CLI 전환

```bash
# 기존 것 제거하고 다시 설치
rm -rf ~/.codex/skills/gstack
git clone https://github.com/identity16/gstack.git ~/gstack-fork
cd ~/gstack-fork && ./setup --host codex
```

### 원본으로 되돌리기

언제든 원본으로 되돌릴 수 있습니다:

```bash
rm -rf ~/.claude/skills/gstack
git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup
```

### 주의사항

- **CLAUDE.md 수정 불필요.** 스킬 이름과 사용법은 원본과 동일합니다.
- **설정 파일 호환.** `~/.gstack/config.yaml` 등 기존 설정이 그대로 동작합니다.
- **`/gstack-upgrade` 주의.** 이 포크에서는 `/gstack-upgrade`가 원본 대신 이 포크의 최신 버전을 가져옵니다. remote URL이 `identity16/gstack`인지 확인하세요.

## Development

```bash
bun install          # 의존성 설치
bun test             # 무료 테스트 (browse + snapshot + skill validation)
bun run test:evals   # 유료 evals (LLM judge + E2E, ~$4/run)
bun run build        # 문서 생성 + 바이너리 컴파일
bun run dev <cmd>    # 개발 모드로 CLI 실행
```

자세한 개발 가이드는 [CLAUDE.md](CLAUDE.md)와 [Contributing](CONTRIBUTING.md) 참고.

## Docs

| Doc | 내용 |
|-----|------|
| [Skill Deep Dives](docs/skills.md) | 모든 스킬의 철학, 예시, 워크플로우 |
| [Builder Ethos](ETHOS.md) | 빌더 철학: Boil the Lake, Search Before Building |
| [Architecture](ARCHITECTURE.md) | 설계 결정과 시스템 내부 구조 |
| [Browser Reference](BROWSER.md) | `/browse` 전체 커맨드 레퍼런스 |
| [Contributing](CONTRIBUTING.md) | 개발 환경 설정, 테스트, 기여 가이드 |
| [Changelog](CHANGELOG.md) | 버전별 변경사항 |

## License

MIT. 원본 저작권: Copyright (c) 2026 Garry Tan. [전체 라이선스](LICENSE) 참고.
