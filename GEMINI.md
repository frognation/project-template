<!-- AUTO-GENERATED from CLAUDE.md by scripts/sync-agent-configs.sh — do not edit / CLAUDE.md에서 자동 생성. 직접 수정 금지 -->
# CLAUDE.md — Multi-Project Root Schema / 멀티 프로젝트 루트 스키마

> This folder is a **multi-project hub** cloned from [`project-template`](https://github.com/frognation/project-template). Each subfolder (except `templates/`, `_shared/`, `_archive/`, underscored dirs) is an individual project.
> 이 폴더는 [`project-template`](https://github.com/frognation/project-template)에서 clone한 **멀티 프로젝트 허브**. `templates/`, `_shared/`, `_archive/`, underscore 디렉토리를 제외한 모든 서브폴더가 개별 프로젝트.

---

## 0. First-time / 첫 실행

If non-template folders exist at root without an individual project structure (no `meta/brief.md`, no `CLAUDE.md`), they're likely un-integrated existing projects.

루트에 비템플릿 폴더가 있는데 개별 프로젝트 구조가 없으면(`meta/brief.md` 없음, `CLAUDE.md` 없음), 아직 통합되지 않은 기존 프로젝트들.

→ **Read [`ONBOARDING.md`](ONBOARDING.md) and offer to run project integration.**
→ [`ONBOARDING.md`](ONBOARDING.md) 읽고 프로젝트 통합 실행 제안.

---

## 0a. Session start auto-scan / 세션 시작 자동 스캔

When a session begins with a generic greeting ("안녕", "시작", "상태", "status") OR a project-agnostic message, scope to the active project (CWD = deepest ancestor with `meta/brief.md`) and run a **cheap scan**.

세션 시작 시 일반 인사("안녕", "시작", "상태", "status") 또는 프로젝트 미지정 메시지면, 활성 프로젝트(CWD = `meta/brief.md`를 가진 가장 가까운 조상)에 범위 잡고 **저비용 스캔**.

**Scan checklist / 스캔 체크리스트:**

1. **New research sources / 새 리서치 자료** — `<project>/research/raw/` filenames not in `<project>/research/wiki/index.md`.
   `<project>/research/raw/` 중 `index.md`에 없는 파일.

2. **Unlogged comms / 미기록 커뮤니케이션** — `<project>/comms/*.md` newer than the latest `<project>/status/*.md` and not linked from it.
   `<project>/comms/*.md` 중 최신 `status/*.md`보다 신규이면서 링크 안 된 것.

3. **Upcoming milestones / 임박한 마일스톤** — `<project>/meta/timeline.md` entries due within 7 days.
   `<project>/meta/timeline.md` 중 7일 이내 마감.

4. **Stale status / 오래된 status** — latest `<project>/status/*.md` older than 10 days.
   최신 `status/*.md`가 10일 이상 경과.

**Report format / 보고 형식:**

```
📋 <project-name>
  • 3 new research sources / 새 리서치 3건
  • 1 meeting note not in latest status / 최신 status에 미반영 미팅노트 1건
  • Milestone "Design review" due Fri / 마일스톤 "Design review" 금요일 마감
  • Status last updated 12 days ago / status 12일 전 업데이트
```

Then ask: "Which first? / 어느 것부터 처리할까요?"

**Cost cap / 비용 상한:** Filenames + `index.md` + timeline + latest status only. ≤3 tool calls. Never read `working/` contents.

**비용 상한:** 파일명 + `index.md` + timeline + 최신 status만. 도구 호출 ≤3회. `working/` 내용 절대 읽지 않음.

**Skip scan when / 생략 조건:** User's first message targets a specific file or says "no scan" / 사용자가 특정 파일 지정 또는 "스캔 생략" 요청.

---

## 1. Folder layout / 폴더 구조

```
<this-folder>/                # cloned from project-template; replaces user's Projects/
├── CLAUDE.md                 # This file / 이 파일
├── README.md                 # Human intro / 사람용 소개
├── ONBOARDING.md             # First-run project integration guide / 첫 통합 가이드
├── FOLDER-STRUCTURE.md       # Design rationale / 설계 근거
├── TEMPLATE-SYNC.md          # Template ↔ personal-use sync workflow / 동기화 워크플로우
├── llm-wiki.md               # Underlying pattern doc / 기저 패턴 문서
│
├── templates/                # Shared templates / 공용 템플릿
│   ├── project/              # Per-project bootstrap / 개별 프로젝트 부트스트랩
│   ├── source.md, entity.md, concept.md   # Page-level / 페이지 단위
│   └── README.md
│
├── _shared/                  # Cross-project pages (people, vendors, etc.) / 프로젝트 간 공유
├── _archive/                 # Completed projects / 완료 프로젝트
│
└── <project-name>/           # Individual project (one per folder)
    ├── CLAUDE.md             # project-specific overrides / 프로젝트별 오버라이드
    ├── meta/                 # brief, timeline, stakeholders, decisions, contract
    ├── research/             # embedded research wiki (raw/ + wiki/)
    ├── working/              # ⛔ binary files — LLM OFF-LIMITS
    ├── deliverables/         # final outputs
    ├── comms/                # meeting notes, email digests
    └── status/               # weekly status
```

**Reserved names / 예약 이름** (not projects): `templates`, `_shared`, `_archive`, anything starting with `_` or `.`.

---

## 2. Global rules / 전역 규칙

### 2.1 ⛔ working/ is off-limits / working/ 출입 금지

Inside ANY project, the `working/` folder is **strictly off-limits** to the LLM. See [`templates/project/working/README.md`](templates/project/working/README.md).

어느 프로젝트든 `working/` 폴더는 LLM **엄격 출입 금지**.

LLM MUST NOT:
- Read content of any file inside any `*/working/` path
- Move, rename, delete, or copy files inside `working/`
- Run shell commands that modify `working/` contents

LLM MAY:
- Use `ls` to see file names if the user explicitly asks
- Reference `working/` paths in deliverables or decisions as text

### 2.2 Bilingual format / 영한 병기

Every LLM-generated markdown is bilingual (EN + KO) in a single file. Alternating paragraphs, slash-separated headings. **No `*.ko.md` / `*.en.md` pairs.**

LLM 생성 마크다운은 단일 파일 영한 병기. 단락 교대, 제목 슬래시 구분. **`*.ko.md` / `*.en.md` 분리 금지.**

Exception: contract documents (`meta/contract.md`) may be in the original legal language of the contract; user controls this.

예외: 계약 문서(`meta/contract.md`)는 계약 원문 언어일 수 있음; 사용자가 결정.

### 2.3 Scoping / 범위

The LLM always operates in the context of ONE project at a time. To work across projects, the user must say so explicitly (e.g., "compare Project A's brief to Project B").

LLM은 항상 한 번에 하나의 프로젝트 맥락에서 작업. 여러 프로젝트에 걸친 작업은 사용자가 명시적으로 요청.

### 2.4 Contract & sensitive data / 계약·민감 데이터

Treat `meta/contract.md` and any `meta/*-sensitive.md` as read-primarily. Modify only on explicit user instruction — never infer contract changes from context.

`meta/contract.md` 및 `meta/*-sensitive.md`는 주로 읽기. 명시적 지시 없이 수정 금지 — 맥락 추론으로 계약 변경 금지.

---

## 3. Naming / 명명

Individual project folders:

개별 프로젝트 폴더:

- **Bare / 기본**: `<project-name>/` (e.g. `hotta/`, `brand-rebrand/`)
- **With year prefix** (recommended for many projects): `YYYY-<name>/` (e.g. `2026-hotta/`)
- **With client prefix**: `<client>-<name>/` (e.g. `client-x-rebrand/`)

Pick one pattern and stay consistent within this folder.

---

## 4. Per-project schema / 프로젝트별 스키마

Individual project workflow rules are in each project's own `CLAUDE.md`, which is copied from [`templates/project/CLAUDE.md`](templates/project/CLAUDE.md) at bootstrap.

개별 프로젝트의 워크플로우 규칙은 각 프로젝트의 `CLAUDE.md`에 있음. 부트스트랩 시 [`templates/project/CLAUDE.md`](templates/project/CLAUDE.md)에서 복사.

Those rules define: brief kickoff, decision logging (ADR), research ingestion, weekly status, deliverable tracking, meeting notes.

---

## 5. Archive workflow / 아카이브 워크플로우

When a project reaches `status: completed`:

프로젝트가 `status: completed`에 도달하면:

1. LLM writes final status entry and retrospective in `meta/brief.md`.
2. LLM identifies potentially reusable research → suggests promoting to `Learning/` (if companion [learning-template](https://github.com/frognation/learning-template) is in use).
3. User decides: move to `_archive/` OR export zip OR leave in place.

LLM does not auto-archive — user triggers it explicitly.

LLM이 자동 아카이브하지 않음 — 사용자가 명시적으로 실행.

---

## 6. Cross-references / 교차 참조

### Between projects / 프로젝트 간

Rare but legitimate (e.g. "our previous client had the same problem"). Use wikilinks: `[[../<other-project>/meta/decisions.md#<anchor>]]`.

드물지만 유효 (예: "이전 클라이언트도 같은 문제"). 위키링크 사용.

### To _shared/ / _shared/로

For entities/concepts common to multiple projects (recurring vendors, reusable playbooks), put them in `_shared/` and link from multiple projects.

여러 프로젝트에 공통(반복 벤더·재사용 플레이북)은 `_shared/`에 두고 여러 프로젝트에서 링크.

### To companion Learning vault / learning-template으로

If [learning-template](https://github.com/frognation/learning-template) is also installed as a sibling folder (e.g. at `MyVault/Learning/`), cross-link with relative paths: `[[../../../Learning/research-<topic>/wiki/concepts/<page>]]`.

[learning-template](https://github.com/frognation/learning-template)이 형제 폴더로 설치돼 있으면(예: `MyVault/Learning/`) 상대경로 링크.

---

## 7. Language defaults / 기본 언어

- Conversation with user: **Korean**.
  사용자와 대화: **한국어**.
- All markdown docs (except user notes / contract): **bilingual EN+KO**.
  모든 마크다운 문서(사용자 노트·계약 제외): **영한 병기**.
- File names, code, tags: **English** (kebab-case).
  파일명·코드·태그: **영문 kebab-case**.
- Commit messages (if user uses git): **English**.
  커밋 메시지: **영문**.

---

## 8. Modifying this schema / 스키마 수정

Edit this file directly. Common changes:

- Add a global rule → new section here
- Change per-project template → edit `templates/project/CLAUDE.md`
- Change bilingual style → rewrite §2.2 + update all per-project CLAUDE.md files

Per-project overrides go in `<project>/CLAUDE.md` and shadow this file's rules for that project only.

프로젝트 단위 오버라이드는 `<project>/CLAUDE.md`에. 해당 프로젝트에만 적용되며 이 파일을 가림.
