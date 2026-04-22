# Folder Structure — Project Template / 폴더 구조 — 프로젝트 템플릿

> Design rationale for how projects are organized in this vault.
> 이 볼트에서 프로젝트가 어떻게 구성되는지에 대한 설계 근거.

---

## 1. Big picture / 큰 그림

```
MyVault/                               ← your Obsidian vault root
├── Learning/                          ← from learning-template (optional companion)
├── Projects/                          ← THIS folder (from project-template)
│   ├── CLAUDE.md, templates/, ...
│   ├── ONBOARDING.md, TEMPLATE-SYNC.md
│   │
│   ├── hotta/                         ← individual project
│   ├── rebrand/                       ← individual project
│   └── _archive/
│       └── 2025-11-old-project/
└── (other categories like 작업, 하우스키핑, etc.)
```

**One Obsidian vault** covers everything. `Projects/` is one category among your vault's categories.

**옵시디언 볼트 1개**가 모든 것을 담음. `Projects/`는 볼트 카테고리 중 하나.

---

## 2. Per-project structure / 프로젝트별 구조

```
<project>/
├── CLAUDE.md            ← project-specific workflow rules
│
├── meta/                ← WHAT THIS PROJECT IS
│   ├── brief.md         ← goal, scope, success criteria
│   ├── timeline.md      ← milestones
│   ├── stakeholders.md  ← people involved
│   ├── decisions.md     ← ADR log
│   └── contract.md      ← commercial terms
│
├── research/            ← WHAT WE LEARN FOR THIS PROJECT
│   ├── raw/             ← source PDFs, articles, clips
│   └── wiki/            ← LLM-built knowledge
│       ├── sources/     ← per-source summaries
│       ├── entities/    ← competitors, key people, orgs
│       └── concepts/    ← industry concepts, frameworks
│
├── working/             ← HOW WE MAKE IT (⛔ LLM off-limits)
│   ├── ai/              ← Illustrator
│   ├── indd/            ← InDesign
│   ├── psd/             ← Photoshop
│   └── figma-exports/
│
├── deliverables/        ← WHAT WE SHIP
│
├── comms/               ← WHO WE TALKED TO
│
└── status/              ← HOW IT'S GOING
```

### Mental model / 멘탈 모델

Each subfolder answers a different question about the project:

각 서브폴더가 프로젝트에 대한 다른 질문에 답:

| Folder | Question answered / 답하는 질문 |
|---|---|
| `meta/` | What IS this project? / 이 프로젝트는 무엇인가? |
| `research/` | What do we know about the domain? / 도메인에 대해 무엇을 아는가? |
| `working/` | How are we making it? (raw craft) / 어떻게 만들고 있는가? (원본 작업) |
| `deliverables/` | What are we shipping? / 무엇을 납품하는가? |
| `comms/` | Who did we talk to? / 누구와 이야기했나? |
| `status/` | How is it going? / 어떻게 진행 중인가? |

All except `working/` are LLM-maintained markdown. `working/` is yours alone.

`working/` 외 모두 LLM이 유지하는 마크다운. `working/`는 사용자만.

---

## 3. Why working/ is separate / 왜 working/만 분리

**The LLM is good at**: summaries, knowledge structure, cross-referencing, status drafting, decision articulation.

**LLM이 잘하는 것**: 요약, 지식 구조화, 교차 참조, status 초안, 결정 명문화.

**The LLM is bad at (or shouldn't touch)**: your actual design files, video cuts, CAD files, Final Cut projects, etc. Those are:
- Binary (LLM can't read meaningfully)
- Your craft (your editorial / aesthetic control)
- Often large (not git-friendly)
- Already versioned elsewhere (Figma history, Photoshop snapshots, cloud storage)

**LLM이 못하는/건드리면 안 되는 것**: 실제 디자인 파일, 영상 컷, CAD, Final Cut 프로젝트 등. 바이너리이고, 사용자의 craft이고, 크고, 이미 다른 곳에서 버전관리됨.

By walling `working/` off explicitly, we get the best of both: AI helping with knowledge work, hands-off for craft files.

`working/`를 명시적으로 분리해 양쪽의 장점: AI는 지식 작업 돕고, craft 파일은 건드리지 않음.

---

## 4. Queryability / 질의 가능성

Because brief, timeline, stakeholders, decisions, contract, research, comms, and status are all **markdown inside the project folder**, you can ask the LLM:

브리프·일정·이해관계자·결정·계약·리서치·커뮤니케이션·status가 **모두 프로젝트 폴더 안 마크다운**이기에 LLM에게 질문 가능:

```
"Hotta 프로젝트 계약 조건 요약해 줘"
"지난 달 Hotta에서 내린 결정 3개 뭐였지?"
"이번 주 Hotta status 보여주고, blocked 항목 해결방안 제안해 줘"
"Hotta 경쟁사 중 가장 유사한 포지셔닝인 곳은?"
"클라이언트가 최근 미팅에서 언급한 요구사항들 정리해 줘"
```

The answers come from parsing the markdown files — no external system, no cloud sync latency, no vendor lock-in.

답은 마크다운 파싱에서 옴 — 외부 시스템 불필요, 클라우드 동기화 지연 없음, 벤더 종속 없음.

---

## 5. Archive & reuse / 아카이브·재사용

When a project completes:

프로젝트 완료 시:

```bash
# Move to archive
mv hotta _archive/2026-04-hotta

# Optional: extract reusable knowledge to Learning/
# Only what's TRULY reusable across future projects (not project-specific details)
```

Archived projects stay searchable in Obsidian (just in a different folder). If you need to revisit the decisions or research, it's all preserved.

아카이브된 프로젝트도 Obsidian에서 검색 가능 (폴더만 다를 뿐). 결정이나 리서치 다시 볼 필요 있으면 모두 보존됨.

---

## 6. Multiple projects / 다수 프로젝트 관리

Just add more project folders as siblings:

프로젝트 폴더를 형제로 추가:

```
Projects/
├── hotta/
├── rebrand-project/
├── brand-system-x/
└── _archive/
    └── 2025-11-old-project/
```

The LLM knows to scope by project — when you say "Hotta", it operates in `hotta/` only.

LLM은 프로젝트별로 범위 인식 — "Hotta"라고 하면 `hotta/`에서만 작업.

For cross-project analysis ("which of our projects dealt with Japanese market?"), ask explicitly. LLM searches across but presents grouped results.

프로젝트 간 분석("일본 시장 다룬 프로젝트는?")은 명시 요청. LLM이 여러 프로젝트 검색 후 그룹화해 표시.

---

## 7. Relationship to learning-template / learning-template과의 관계

| | Project (this) | Learning (companion) |
|---|---|---|
| Time horizon | Weeks → months | Years |
| Unit | Deliverable | Mastery |
| Archive cycle | When project ends | Never |
| Research scope | This client, this brief | General domain (reusable) |

If you install both, place them as siblings:

둘 다 설치하면 형제 폴더로:

```
MyVault/
├── Learning/           ← from learning-template
└── Projects/           ← from project-template
```

Cross-link: `[[../../Learning/research-japanese-tea/wiki/concepts/matcha-grading]]`.

**Rule of thumb**: if a concept/entity would be useful in a FUTURE project unrelated to the current one, promote to `Learning/`. Otherwise keep in project.

**판단 기준**: 개념·엔티티가 현재와 무관한 **미래 프로젝트**에서도 쓸 것 같으면 `Learning/`으로 승격. 아니면 프로젝트에 보존.

---

## 8. What this vault is NOT / 이 볼트가 아닌 것

- Not a ticketing system (use Linear/Jira/Asana)
- Not a CRM (use HubSpot/Notion)
- Not time tracking (use Toggl/Harvest)
- Not a design file repository (Figma/Illustrator files live in `working/`, not git)
- Not a live collaboration tool (use Obsidian Sync, Dropbox, etc. separately)

티켓·CRM·시간추적·디자인 파일 리포·실시간 협업 도구 아님.

This is a **knowledge + decision record** for each project. The craft lives in `working/`; the "what/why/how" lives in markdown.

이것은 프로젝트별 **지식·결정 기록**. 실제 craft는 `working/`, "무엇·왜·어떻게"는 마크다운.
