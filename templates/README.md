# Templates — project-template / 템플릿 가이드

> Templates used inside individual projects within this multi-project hub.
> 이 멀티 프로젝트 허브 내 개별 프로젝트에서 사용되는 템플릿.

---

## File map / 파일 지도

### Hub-level / 허브 단위

| Template | Purpose / 용도 | Bootstrap path / 부트스트랩 경로 |
|---|---|---|
| [`project/`](project/) | Individual project bootstrap (brief, research, working, deliverables, comms, status) | `<project-name>/` |

### Page-level / 페이지 단위 (used inside a project's `research/wiki/`)

| Template | Use for / 용도 | Goes in / 저장 위치 |
|---|---|---|
| [`source.md`](source.md) | Per-source summary page | `<project>/research/wiki/sources/` |
| [`entity.md`](entity.md) | Person, org, product, place | `<project>/research/wiki/entities/` |
| [`concept.md`](concept.md) | Idea, theory, framework | `<project>/research/wiki/concepts/` |

---

## Bootstrap a new project / 새 프로젝트 부트스트랩

### Method A — ask Claude / Claude에게

In Claude Code, at this folder's root:

```
Projects/<name>을 프로젝트 허브로 부트스트랩해 줘.
- 클라이언트: <client>
- 목표: <one sentence>
- 시작일: <YYYY-MM-DD>
- 납기 목표: <YYYY-MM-DD>
```

Claude copies `templates/project/*` → `<name>/`, fills placeholders.

### Method B — shell / 직접 명령

```bash
cp -r templates/project <new-project-name>
# Then edit <new-project-name>/meta/brief.md
```

---

## What the project template includes / 프로젝트 템플릿 구성

```
templates/project/
├── README.md               ← when to use, structure
├── CLAUDE.md               ← per-project schema (workflows: brief, decisions, research, status, etc.)
├── meta/
│   ├── brief.md            ← 1-page brief template
│   ├── timeline.md         ← milestones template
│   ├── stakeholders.md     ← people template
│   ├── decisions.md        ← ADR-style log template
│   └── contract.md         ← commercial/legal terms template
├── research/               ← embedded research wiki (inherits page-level templates above)
│   ├── raw/.gitkeep
│   └── wiki/
│       ├── index.md
│       ├── log.md
│       ├── sources/.gitkeep
│       ├── entities/.gitkeep
│       └── concepts/.gitkeep
├── working/
│   └── README.md           ← ⛔ LLM off-limits declaration
├── deliverables/
│   └── README.md
├── comms/
│   └── README.md
└── status/
    └── README.md
```

See [`project/README.md`](project/README.md) for details.

---

## Modifying templates / 템플릿 수정

- **Edit a template file** → changes apply to NEW projects bootstrapped after the edit. Existing projects are not automatically updated.
  템플릿 파일 수정 → 이후 부트스트랩되는 **새** 프로젝트에 적용. 기존 프로젝트는 자동 갱신 안 됨.
- **Sync existing projects with updates**: the user must manually review and apply diffs per project. LLM can help: `"templates/project/CLAUDE.md의 최신 변경사항을 hotta/CLAUDE.md에 적용해 줘"`.
  기존 프로젝트 업데이트 반영: 프로젝트별로 수동 diff 적용. LLM이 도움: `"templates/project/CLAUDE.md의 최신 변경사항을 hotta/CLAUDE.md에 적용해 줘"`.
- **Add a brand-new template**: create here, document in this README, update root `CLAUDE.md` if relevant.
  새 템플릿 추가: 여기 생성, 본 README에 문서화, 필요 시 루트 `CLAUDE.md` 업데이트.

See [`../TEMPLATE-SYNC.md`](../TEMPLATE-SYNC.md) for the template ↔ personal-vault sync workflow.

템플릿과 개인 vault 간 동기화는 [`../TEMPLATE-SYNC.md`](../TEMPLATE-SYNC.md) 참고.

---

## Related / 관련

- [`../README.md`](../README.md) — vault intro
- [`../CLAUDE.md`](../CLAUDE.md) — multi-project root schema
- [`../ONBOARDING.md`](../ONBOARDING.md) — integrate existing projects
- [`../FOLDER-STRUCTURE.md`](../FOLDER-STRUCTURE.md) — design rationale
