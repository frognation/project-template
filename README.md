# Project Template — v.1.0 / 프로젝트 템플릿 v.1.0

> **A self-contained template for managing multiple projects** as a subfolder of your Obsidian vault. Each project gets: brief · timeline · stakeholders · decisions · contract · integrated research wiki · deliverables · meeting notes · status updates · working-file folder.
> 옵시디언 볼트의 서브폴더로서 **여러 프로젝트를 관리하는 self-contained 템플릿**. 각 프로젝트는: 브리프 · 일정 · 이해관계자 · 결정 · 계약 · 통합 리서치 위키 · 산출물 · 미팅 노트 · status · 작업 파일 폴더를 가짐.

> **Companion repo**: [learning-template](https://github.com/frognation/learning-template) — for long-term learning and domain research (study / research hubs).
> **짝 리포**: [learning-template](https://github.com/frognation/learning-template) — 장기 학습·도메인 리서치용 (study / research 허브).

---

## What this is / 이게 뭔가요

Clone this repo into your Obsidian vault to **replace your existing `Projects/` folder**. Move your existing project folders inside, run onboarding, and Claude integrates them per this template's structure.

이 리포를 옵시디언 볼트에 clone해서 **기존 `Projects/` 폴더를 대체**. 기존 프로젝트 폴더들을 안으로 옮기고 onboarding 실행 → Claude가 이 템플릿의 구조에 맞게 통합.

For new projects: copy `templates/project/` → `<project-name>/`, fill in the brief, done.

새 프로젝트는: `templates/project/`를 `<project-name>/`으로 복사 → 브리프 작성 → 끝.

---

## Each project contains / 각 프로젝트가 담는 것

```
<project>/
├── CLAUDE.md           ← project schema (workflows, rules)
├── meta/               ← project-level metadata
│   ├── brief.md        ← 1-page brief (goal, scope, success criteria)
│   ├── timeline.md     ← milestones
│   ├── stakeholders.md ← people involved
│   ├── decisions.md    ← ADR-style decision log
│   └── contract.md     ← commercial/legal terms
├── research/           ← integrated research wiki (raw/ + wiki/)
├── working/            ← ⛔ your binary work files — LLM HANDS OFF
├── deliverables/       ← final outputs, one markdown file per
├── comms/              ← meeting notes, email digests
└── status/             ← weekly status updates
```

Everything **except** `working/` is markdown that the LLM helps maintain. `working/` is for your `.ai`/`.indd`/`.psd`/`.fig`/etc. — the LLM reads file names only, never content.

`working/`를 **제외한** 모든 것은 LLM이 유지를 돕는 마크다운. `working/`은 `.ai`/`.indd`/`.psd`/`.fig`/등 — LLM은 파일명만 볼 뿐 내용은 건드리지 않음.

---

## Quick start / 빠른 시작

### A. Fresh setup / 신규 셋업

```bash
# 1. Clone this repo into your Obsidian vault as the Projects folder
cd ~/Dropbox/Obsidian/<your-vault>
git clone https://github.com/frognation/project-template.git Projects
cd Projects && rm -rf .git   # avoid Dropbox + git conflicts

# 2. (If you have existing project folders) move them in
mv ../OldProjects/* ./

# 3. Start Claude Code here and run onboarding
# Tell Claude: "Read ONBOARDING.md and integrate my projects"
```

### B. Add a new project / 새 프로젝트 추가

```bash
# from Projects/ root
cp -r templates/project hotta
# Then edit hotta/meta/brief.md with real info
# Or ask Claude: "Bootstrap Projects/hotta as a new project"
```

---

## The whole vault picture / 전체 볼트 구조

```
MyVault/                              ← Obsidian vault root
├── .obsidian/
│
├── Learning/                         ← cloned from learning-template
│   ├── CLAUDE.md, templates/, ...
│   ├── study-python/
│   └── research-llm/
│
├── Projects/                         ← cloned from THIS repo (project-template)
│   ├── CLAUDE.md, templates/, ...
│   ├── ONBOARDING.md
│   ├── hotta/
│   │   ├── meta/, research/, working/, deliverables/, ...
│   └── _archive/
│       └── 2026-04-old-project/
│
└── (your other categories: 작업, 하우스키핑, etc.)
```

---

## Separation of concerns / 관심사 분리

| | Learning template | Project template (this) |
|---|---|---|
| Time / 시간성 | Permanent knowledge | Time-bounded projects |
| Unit / 단위 | Concepts, entities, sources | Decisions, deliverables, status |
| Core question | "What do I know?" | "What did I decide? What did I produce? What's next?" |
| Archive cycle | Never archived | Archived when project completes |

The two templates are **complementary**. Research that's reusable across future projects → Learning. Research specific to this project → here.

두 템플릿은 **상호 보완**. 여러 프로젝트에서 재사용될 리서치 → Learning. 이 프로젝트 한정 리서치 → 여기.

Cross-link freely: `[[../../Learning/research-japanese-tea/wiki/concepts/matcha-grading]]`.

cross-link 자유: `[[../../Learning/research-japanese-tea/wiki/concepts/matcha-grading]]`.

---

## Documentation map / 문서 지도

- [`llm-wiki.md`](llm-wiki.md) — underlying pattern (bilingual)
- [`CLAUDE.md`](CLAUDE.md) — root schema for this multi-project folder
- [`ONBOARDING.md`](ONBOARDING.md) — **first-run integration of existing projects ⭐**
- [`FOLDER-STRUCTURE.md`](FOLDER-STRUCTURE.md) — design rationale
- [`TEMPLATE-SYNC.md`](TEMPLATE-SYNC.md) — **template ↔ personal vault sync workflow ⭐**
- [`MULTI-AGENT-GUIDE.md`](MULTI-AGENT-GUIDE.md) — **multi-agent usage + token optimization ⭐**
- [`templates/README.md`](templates/README.md) — template usage
- [`templates/project/README.md`](templates/project/README.md) — per-project template details

---

## What's intentionally NOT here / 의도적으로 제외된 것

This template is markdown-first, LLM-assisted. It does NOT replace:

- Sprint / ticket boards → **Linear, Jira, Asana**
- Time tracking → **Toggl, Harvest**
- Gantt charts → **MS Project, ClickUp, Notion**
- File versioning for binaries → **git-LFS, Figma history, cloud storage**
- Client CRM → **HubSpot, Notion, Pipedrive**

이 템플릿은 마크다운 중심·LLM 보조. 위 도구들을 대체하지 않음 — 필요하면 병행.

---

## License / 라이선스

MIT (suggested).

---

## Versioning / 버전 관리

**v1.0** — initial public release.

See [learning-template README §Versioning](https://github.com/frognation/learning-template#versioning--template--personal-separation--버전관리--템플릿개인-분리) for the clone / back-port strategy that applies equally here.

clone / back-port 전략은 [learning-template README §Versioning](https://github.com/frognation/learning-template#versioning--template--personal-separation--버전관리--템플릿개인-분리) 참고 — 이 리포에도 동일하게 적용.
