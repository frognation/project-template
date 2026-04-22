# Working Files / 작업 파일

> ⛔ **OFF-LIMITS to LLM agents** — this folder contains the user's actual working files (Illustrator, InDesign, Figma exports, Photoshop, etc.). LLM must not read, modify, move, rename, or delete anything here.
> ⛔ **LLM 에이전트 출입 금지** — 이 폴더는 사용자의 실제 작업 파일(일러스트레이터·인디자인·Figma export·포토샵 등). LLM은 여기 있는 것을 읽지·수정·이동·이름변경·삭제 모두 금지.

---

## Why this folder exists / 이 폴더가 있는 이유

Project research, decisions, and notes go in `meta/`, `research/`, `comms/`, etc. — those are **markdown** and the LLM helps maintain them.

프로젝트 리서치·결정·노트는 `meta/`, `research/`, `comms/` 등에. 그것들은 **마크다운**이고 LLM이 유지를 돕습니다.

But you also have **binary working files** — `.ai`, `.indd`, `.psd`, `.fig`, video, audio, source files for tools that aren't markdown-friendly. They live HERE.

하지만 **바이너리 작업 파일** — `.ai`, `.indd`, `.psd`, `.fig`, 영상·음원·기타 마크다운과 안 어울리는 도구의 원본 파일들. 그것들은 **여기**에.

The LLM:
- ❌ Cannot read or summarize these files
- ❌ Cannot reorganize them (you organize them in your tool of choice)
- ❌ Cannot delete or move them
- ✅ CAN see the file names (via `ls`) if explicitly asked, to reference them in deliverables/decisions
- ✅ CAN suggest a folder organization in **plain text** for you to apply manually

---

## Recommended sub-organization / 권장 하위 정리

Up to you, but a common pattern:

본인 마음대로지만 흔한 패턴:

```
working/
├── ai/                  # Illustrator files
├── indd/                # InDesign files
├── figma-exports/
├── photoshop/
├── source-assets/       # raw photos, fonts, brand assets received from client
├── exports/             # PDF/PNG/etc exports for review (intermediate)
└── archive/             # old versions
```

Final outputs ready to deliver → move to `../deliverables/` (separate folder, LLM helps document them there).

납품 가능한 최종 출력물은 `../deliverables/`로 이동 (별도 폴더, LLM이 거기서 문서화 도움).

---

## .gitignore guidance / .gitignore 권장

These files are usually too large for git. The repo's `.gitignore` already excludes common patterns:

이 파일들은 보통 git에 두기엔 너무 큼. 리포의 `.gitignore`가 이미 일반 패턴 제외:

```gitignore
**/working/**/*.ai
**/working/**/*.indd
**/working/**/*.psd
**/working/**/*.fig
**/working/**/*.mp4
**/working/**/*.mov
```

Add specific patterns you need.

추가 패턴은 본인 필요에 따라.

---

## If you want LLM to reference a working file / LLM이 작업파일 언급하길 원할 때

You can manually create a markdown reference page:

수동으로 마크다운 참조 페이지를 만들 수 있음:

```markdown
<!-- in deliverables/poster-v2.md -->
## Source file / 원본 파일

`working/ai/poster-v2.ai` (Illustrator, ~80MB)

## What it contains
<your description in plain text>
```

This way the LLM knows about the file's existence and purpose, but never touches the binary itself.

이렇게 하면 LLM이 파일의 존재와 목적은 알지만 바이너리 자체는 건드리지 않음.
