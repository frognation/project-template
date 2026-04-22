# Multi-Agent Usage Guide / 멀티 에이전트 사용 가이드

> Use this projects folder from Claude Code, Codex CLI, Cursor, Windsurf, or Gemini CLI — with the **same rules** applying to all of them.
> 이 프로젝트 폴더를 Claude Code, Codex CLI, Cursor, Windsurf, Gemini CLI 어디서든 **동일 규칙**으로 사용.

---

## 1. Why this file exists / 이 파일의 이유

Each agent reads its own config filename:

각 에이전트는 서로 다른 파일명을 읽습니다:

| Agent / 에이전트 | Default config / 기본 설정 |
|---|---|
| Claude Code | `CLAUDE.md` |
| Codex CLI | `AGENTS.md` |
| Cursor | `CLAUDE.md` (recent) or `.cursor/rules/*.mdc` |
| Windsurf | `.windsurfrules` |
| Gemini CLI | `GEMINI.md` |

**`CLAUDE.md` is the single source of truth.** All other variants are generated mirrors.

**`CLAUDE.md`가 유일한 원본.** 나머지는 자동 생성 미러.

> ⚠️ **Never edit `AGENTS.md` or `GEMINI.md` directly** — they get overwritten.
> **`AGENTS.md`·`GEMINI.md` 직접 수정 금지** — 덮어써짐.

---

## 2. Generate mirror files / 미러 파일 생성

After cloning, and whenever any `CLAUDE.md` changes:

clone 직후, 그리고 `CLAUDE.md` 수정 시마다:

```bash
bash scripts/sync-agent-configs.sh
```

Generates `AGENTS.md` and `GEMINI.md` next to every `CLAUDE.md` (root + each project). Excludes `working/`, `.git/`, `node_modules/`, `.obsidian/`.

모든 `CLAUDE.md`(루트 + 각 프로젝트) 옆에 `AGENTS.md`·`GEMINI.md` 생성. `working/`, `.git/`, `node_modules/`, `.obsidian/` 제외.

---

## 3. Per-agent startup / 에이전트별 시작

```bash
cd <project-folder>
claude   # Claude Code → CLAUDE.md
codex    # Codex CLI   → AGENTS.md
gemini   # Gemini CLI  → GEMINI.md
```

For Cursor / Windsurf: open the folder as workspace.

Cursor / Windsurf: 폴더를 워크스페이스로 열기.

---

## 4. Session scoping — the biggest win / 세션 범위 — 가장 큰 최적화

**Open sessions INSIDE a specific project.** This is the single biggest token-saving decision.

**특정 프로젝트 안에서 세션 열기.** 토큰 절약 최대 효과.

| Where you `cd` / `cd` 위치 | Scope / 범위 |
|---|---|
| Projects root (`Projects/`) | All projects + archive — huge context / 모든 프로젝트 + 아카이브 — 거대 컨텍스트 |
| Specific project (`Projects/hotta/`) ⭐ | Just this project / 이 프로젝트만 |
| Subfolder (`Projects/hotta/research/`) | Even narrower / 더 좁게 |

Use the Projects root only for cross-project queries ("compare X and Y"). For any single-project work: `cd` into it.

프로젝트 루트는 프로젝트 간 비교 쿼리 때만. 단일 프로젝트 작업은 무조건 프로젝트 폴더 안으로.

---

## 5. Token optimization / 토큰 최적화

### 5.1 `working/` is a hard boundary / `working/`는 절대 경계

The per-project `CLAUDE.md` already enforces "LLM OFF-LIMITS" for `working/`. Don't relax this — `.ai`/`.psd`/`.fig` binaries would explode token usage even if readable.

프로젝트별 `CLAUDE.md`가 `working/` 출입 금지 강제. 절대 풀지 말 것 — 바이너리는 토큰 폭발.

### 5.2 Let the agent use `research/wiki/index.md` first / `index.md` 먼저

Project research wiki has its own `index.md`. Cheapest first read for any research query.

프로젝트 리서치 위키에 `index.md` 존재. 어떤 리서치 쿼리든 가장 저렴한 첫 읽기.

```
"research/wiki/index.md 먼저 보고 관련 페이지만 골라 읽은 뒤 답해 줘"
```

### 5.3 Keep `CLAUDE.md` tight / `CLAUDE.md` 짧게

Under ~300 lines per `CLAUDE.md`. Long design rationale goes in `FOLDER-STRUCTURE.md`.

`CLAUDE.md`당 300줄 이내. 긴 설계 설명은 `FOLDER-STRUCTURE.md`로.

### 5.4 Tell the agent what NOT to read / 읽지 말 것 명시

```
- Don't read working/ contents (ever).
- Don't read research/raw/ unless ingesting a specific file.
- Don't read _archive/ unless explicitly asked.
- Don't read contract.md unless I say so.
```

### 5.5 Use Dataview for project dashboards / 프로젝트 대시보드는 Dataview

Zero LLM cost. Great for:

LLM 비용 0. 적합:
- Status across all projects / 전체 프로젝트 status 현황
- Milestones due this week / 이번 주 마감 마일스톤
- Open decisions / 미해결 결정사항
- Deliverables by status / status별 산출물

LLM is for synthesis (comparing briefs, summarizing decisions), not counting.

LLM은 종합용(브리프 비교·결정 요약). 집계용 아님.

### 5.6 Clear context between projects / 프로젝트 전환 시 리셋

Claude Code: `/clear` or new session. Codex: restart. Project contexts should not bleed into each other — especially because each has its own contract / sensitive data.

Claude Code: `/clear` 또는 새 세션. 특히 프로젝트마다 계약·민감 데이터 분리 중요.

### 5.7 `/compact` for long sessions / 장시간 세션

Claude Code: `/compact` keeps salient facts, drops transient tool output.

Claude Code: `/compact`로 중요 사실만 보존, 임시 출력 제거.

### 5.8 Skip patterns for agent-aware tools / 에이전트용 skip

Codex `.codexignore`, Cursor `.cursorignore`:

```
working/
_archive/
research/raw/
**/*.pdf
**/*.psd
**/*.ai
**/*.fig
node_modules/
.obsidian/
```

### 5.9 Scoped reads / 범위 지정 읽기

```
"meta/decisions.md의 ## 2026-04 섹션만"
"status/의 최근 3개 파일만"
```

### 5.10 Batch similar work / 유사 작업 배치

"3개 미팅 노트 한 번에 status에 반영" > "미팅 노트 하나씩 3번 처리".

### 5.11 Per-project CLAUDE.md overrides / 프로젝트별 오버라이드

Each `<project>/CLAUDE.md` shadows root rules for that project only. Use this to keep root rules short while projects get custom rules.

각 `<project>/CLAUDE.md`는 해당 프로젝트에만 적용. 루트 규칙은 짧게, 프로젝트별 세부 규칙은 자체 파일에.

---

## 6. Cross-project queries / 프로젝트 간 쿼리

When you DO want cross-project work:

프로젝트 간 작업이 필요할 때:

1. `cd` to Projects root
2. **Tell the agent exactly which projects** — don't let it scan all.
   **어느 프로젝트들인지 명시** — 전체 스캔 허용 X.

```
✅ "hotta와 client-x의 브리프 비교해 줘"
❌ "모든 프로젝트 현황 봐 줘"   (비용 비쌈 / expensive)
```

For "all projects" status, use Dataview dashboard — not an LLM scan.

"모든 프로젝트 현황"은 Dataview 대시보드 사용 — LLM 스캔 X.

---

## 7. Quick reference / 빠른 참조

```bash
# Generate mirrors / 미러 생성
bash scripts/sync-agent-configs.sh

# Open in specific project / 특정 프로젝트
cd <this-folder>/<project-name>
claude     # or: codex / gemini

# Claude Code
/compact   # summarize long session / 세션 압축
/clear     # switch projects / 프로젝트 전환
```

---

## 8. When rules should diverge / 규칙을 다르게 하고 싶을 때

Default: one `CLAUDE.md`, mirror to all. To diverge for a specific agent:

기본: `CLAUDE.md` 하나 + 전체 미러. 에이전트별로 다르게 하려면:

1. **Conditional section** in `CLAUDE.md`: `### For Codex only / 코덱스 전용`.
2. **Remove from mirror**: drop `AGENTS.md` from `VARIANTS` in sync script and maintain manually.
3. **Override file**: e.g., `.codex/overrides.md`.
