# ONBOARDING — Integrate Existing Projects / 기존 프로젝트 통합

> **Read this when:** you've cloned `project-template` into your vault (replacing or as your `Projects/` folder) and you have existing project folders to integrate.
> **이 문서를 읽을 때:** `project-template`을 볼트에 clone(기존 `Projects/` 폴더 대체 또는 신규)했고 기존 프로젝트 폴더들을 통합하려 할 때.
>
> **Audience / 대상:** human user (Phase A) + next Claude session (Phase B).
> 사람 사용자(Phase A) + 다음 Claude 세션(Phase B).

---

## TL;DR

1. **You** move existing project folders into this vault root (same level as `templates/`).
   기존 프로젝트 폴더를 이 볼트 루트(`templates/`와 같은 레벨)로 이동.
2. **Start a new Claude session**, say: `"ONBOARDING.md 읽고 내 프로젝트들 통합해 줘"`.
   새 Claude 세션: `"ONBOARDING.md 읽고 내 프로젝트들 통합해 줘"`.
3. Claude proposes how to restructure each, applies after confirmation.
   Claude가 각 프로젝트 재구성안 제시, 확인 후 적용.

---

## Phase A — You prepare / 사용자 준비 단계

### A.1 Inventory / 인벤토리

List your existing project folders. For each, note:

각 기존 프로젝트 폴더마다:

- Project name
- Rough state: active / on-hold / completed
- What's inside (rough sense): brief? research materials? working files (Illustrator/InDesign)? meeting notes? deliverables?

### A.2 Move into this folder / 이 폴더로 이동

Move each existing project folder to the root of this vault folder (`Projects/`):

각 프로젝트 폴더를 이 볼트 폴더(`Projects/`) 루트로 이동:

```bash
mv ~/path/to/OldProjects/hotta ./
mv ~/path/to/OldProjects/rebrand ./
# repeat for each
```

Don't touch: `templates/`, `_shared/`, `_archive/`, root `*.md` files.

건드리지 말 것: `templates/`, `_shared/`, `_archive/`, 루트 `*.md` 파일.

### A.3 DO NOT pre-create structure / 미리 구조 만들지 말 것

Don't create `meta/`, `research/`, `working/` subfolders yourself inside each project. Claude does that per classification.

각 프로젝트 안에 `meta/`, `research/`, `working/` 서브폴더를 미리 만들지 마세요. Claude가 분류에 따라 생성.

### A.4 Backup / 백업

**Back up before Phase B.** Git commit is fine, or plain folder copy:

Phase B 이전 **백업**:

```bash
cp -R "./*" ~/backup/projects-pre-onboarding-$(date +%F)/
# or
cd .. && zip -r projects-backup-$(date +%F).zip Projects/
```

---

## Phase B — Claude integrates / Claude가 통합하는 단계

> **Claude: follow these steps.** Do NOT auto-execute anything destructive. Preview, confirm, then apply.
> Claude가 따를 절차. destructive 작업 자동 실행 금지. 미리보기 → 확인 → 적용.

### B.1 Discover / 발견

```bash
# List candidate projects (folders at root, excluding reserved)
ls -d */ | grep -vE '^(templates|_shared|_archive)/$'
```

### B.2 Classify each / 각 프로젝트 분류

For each candidate folder, detect the state:

각 후보 폴더의 상태 감지:

```
Has meta/brief.md or CLAUDE.md already?
  → Already integrated. Skip or propose refresh.

Empty or near-empty?
  → Suggest: "Was this started but never filled? Should I bootstrap as fresh project?"

Has mixed content (PDFs, .md notes, Illustrator/InDesign files, meeting notes)?
  → Classify content into: brief / research / working / comms / deliverables
  → Proposed restructure per sections below
```

### B.3 Content classification rules / 콘텐츠 분류 규칙

For each file in an existing project folder:

기존 프로젝트 폴더의 각 파일:

| File pattern / 파일 패턴 | Destination / 이동 목적지 |
|---|---|
| `brief*.md`, `proposal*.md` | `meta/brief.md` (merge or rename) |
| `timeline*.md`, `schedule*.md`, `gantt*` | `meta/timeline.md` (merge) |
| `contract*.pdf/.md`, `agreement*`, `nda*` | `meta/contract.md` (md) or `working/contracts/` (binary) |
| `meeting-*`, `미팅-*`, `meeting_notes*` | `comms/<date>-<topic>.md` |
| `decisions*.md` | `meta/decisions.md` |
| `status*.md`, `weekly*.md` | `status/YYYY-MM-DD-weekly.md` |
| Research `.pdf`, `.html`, web clips | `research/raw/` |
| Research `.md` summaries | `research/wiki/sources/` (after user review) |
| `.ai`, `.indd`, `.psd`, `.fig`, `.sketch` | `working/<type>/` |
| Final PDFs, final outputs | `deliverables/` |
| Images for reference | `research/raw/assets/` or `working/source-assets/` (judgment call) |
| Unclear / ambiguous | ASK USER |

### B.4 Preview plan / 계획 미리보기

**BEFORE making any changes**, output a markdown plan per project:

**변경 전**, 프로젝트별 계획을 마크다운 표로 출력:

```markdown
## Integration plan — hotta / 통합 계획

Proposed final structure:
- meta/brief.md     ← merged from brief.md, proposal-v2.md
- meta/contract.md  ← converted from contract-signed.pdf (text extracted; PDF kept in working/contracts/)
- meta/timeline.md  ← extracted from email thread (comms/kickoff-email-2026-01-15.md references)
- research/raw/     ← 8 PDFs from matcha-research/
- working/ai/       ← 12 .ai files from design/
- working/indd/     ← 3 .indd files from layout/
- comms/            ← 5 meeting note .md files (renamed to YYYY-MM-DD-<topic>.md format)
- deliverables/     ← final-brand-guide.pdf, logo-exports/

Files to delete (none — all content reorganized, none removed):
Files requiring user decision:
- `old-mood-board.png` — unclear if research reference or working asset. Ask.
- `client-feedback-raw.txt` — extract to comms/ or discard?

Proceed? [y/n]
```

Only after `y` proceed with file moves.

`y` 이후에만 이동 실행.

### B.5 Apply / 적용

For each confirmed project:

확인된 각 프로젝트마다:

1. Create target subfolders: `meta/`, `research/{raw,wiki/{sources,entities,concepts}}/`, `working/`, `deliverables/`, `comms/`, `status/`.
2. `mv` files to their destinations (never `rm`).
3. Create stub pages in `meta/` that don't have source material yet:
   - `meta/stakeholders.md` — "Please fill in" placeholder
   - `meta/decisions.md` — empty log header
   - `meta/timeline.md` — milestones placeholder if none existed
4. Copy `templates/project/CLAUDE.md` → `<project>/CLAUDE.md`, filling placeholders with what's known from brief/folder name.
5. Create `<project>/status/<today>-onboarding.md` summarizing what was done.

### B.6 Working folder special handling / working/ 특별 처리

⛔ When moving binary files into `working/`:

바이너리 파일을 `working/`로 이동 시:

- **Do NOT read file contents.** Use `mv` only.
- Organize by file type: `working/ai/`, `working/indd/`, `working/psd/`, `working/figma-exports/`.
- If a file is clearly a final output (e.g. named `final-delivery.pdf`), put it in `deliverables/` instead of `working/`.

파일 내용 읽지 말 것. `mv`만 사용. 파일 타입별 정리. 최종 출력물은 `deliverables/`로.

### B.7 Report / 보고

After all projects processed:

모든 프로젝트 처리 후:

```markdown
## Integration complete / 통합 완료

- ✅ 4 projects integrated
- 📁 Files moved: 127
- 🗑️ Files deleted: 0
- ❓ Files requiring user decision: 3 (see list)

### Pending / 남은 작업
- Fill in stakeholders.md for: hotta, rebrand
- Review 3 ambiguous files flagged above
- Run status update for each active project
```

---

## Safety contract / 안전 규약

Claude MUST:

- ✅ Preview the full plan before any file move
- ✅ Get explicit `y` confirmation before destructive ops
- ✅ NEVER delete user files (only move, with a recorded log)
- ✅ Log every move to `<project>/status/` onboarding entry
- ✅ If classification is ambiguous → ASK, don't guess

Claude MUST NOT:

- ❌ Read content of files inside `working/` (only file names via `ls`)
- ❌ Auto-generate content the user didn't provide (brief, stakeholders — only create stubs)
- ❌ Modify `templates/`, `_shared/`, or any root `*.md`
- ❌ Combine multiple projects into one without explicit user instruction
- ❌ Touch `.ai`, `.indd`, `.psd`, `.fig`, or other binary files beyond `mv`

---

## After onboarding / 통합 이후

- Daily operations: each project has its own `CLAUDE.md` with workflows (brief kickoff, decisions, status, ingestion, etc.).
  일상 운영: 각 프로젝트의 `CLAUDE.md`에 워크플로우 정의.
- New projects: `cp -r templates/project/ <new-project>/` then fill in brief. Or ask Claude to bootstrap.
  새 프로젝트: `templates/project/` 복사 후 브리프 작성. 또는 Claude에게 부트스트랩 요청.
- Sync with template updates: see [`TEMPLATE-SYNC.md`](TEMPLATE-SYNC.md).
  템플릿 업데이트 동기화: [`TEMPLATE-SYNC.md`](TEMPLATE-SYNC.md).
