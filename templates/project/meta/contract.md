---
title: <Project Name> Contract / <프로젝트 한글명> 계약
type: project-contract
status: draft | signed | amended | closed
signed_date: <YYYY-MM-DD>
effective_date: <YYYY-MM-DD>
---

# Contract & Commercial Terms / 계약 및 상업 조건

> Single source of truth for commercial, legal, and contractual details of this project. The LLM can **read** this to answer questions, but **should not modify** without explicit instruction — contract changes require deliberate edits, not inferred ones.
> 이 프로젝트의 상업·법률·계약 세부사항의 single source of truth. LLM은 질문 답변을 위해 **읽을 수 있지만**, 명시적 지시 없이 **수정하지 않음** — 계약 변경은 추론이 아닌 신중한 편집이 필요.

> 🔒 **Privacy note:** If this project is in a shared git repo, consider whether contract details should be tracked. You can add `meta/contract.md` to `.gitignore` or encrypt with git-crypt. Default: trackable.
> 🔒 **프라이버시 참고:** 이 프로젝트가 공유 git 리포에 있다면 계약 세부사항을 tracking할지 결정. `meta/contract.md`를 `.gitignore`에 추가하거나 git-crypt로 암호화 가능. 기본: trackable.

---

## Parties / 당사자

- **Client / 의뢰인**: <legal name, entity type>
- **Service provider / 수행자**: <your name or entity>
- **Signatories / 서명자**: <names and roles>

## Scope of work / 업무 범위

What is being delivered (should match `brief.md` §Scope, but in contract-legal language).

납품 대상 (`brief.md` §Scope와 일치하되 계약 법률 언어로).

- <deliverable>
- <deliverable>

## Commercial terms / 상업 조건

| Item | Amount | Notes |
|---|---|---|
| Total fee / 총 비용 | | |
| Currency / 통화 | | |
| Payment schedule / 지급 일정 | | e.g. 30% upfront / 40% mid / 30% on delivery |
| Invoicing cadence / 청구 주기 | | |
| Late payment terms / 지연 조건 | | |
| Expenses / 경비 | | reimbursable or included |

## Key dates / 핵심 일자

- **Contract signed / 계약 체결일**: <YYYY-MM-DD>
- **Effective date / 효력 발생일**: <YYYY-MM-DD>
- **Kickoff / 킥오프**: <YYYY-MM-DD>
- **Delivery deadline / 납기**: <YYYY-MM-DD>
- **Contract end / 계약 종료일**: <YYYY-MM-DD>

## IP & rights / 지식재산권

- **Ownership of deliverables / 납품물 소유**: <client | shared | service provider>
- **Working files / 작업 원본**: <retained by service provider? delivered?>
- **Portfolio usage / 포트폴리오 사용권**: <allowed | restricted | NDA>
- **Third-party assets / 3자 자산**: <fonts, stock — who pays, who licenses>

## Confidentiality / 기밀 유지

- **NDA status / NDA**: <signed on YYYY-MM-DD | mutual | one-way>
- **What's confidential / 기밀 범위**: <brief description>
- **Expiry / 해제 시점**: <YYYY-MM-DD or "perpetual">

## Revisions & scope changes / 수정·범위 변경

- **Included revisions / 포함 수정 횟수**: <e.g. 2 rounds per deliverable>
- **Additional revision fee / 추가 수정 비용**: <rate>
- **Scope change process / 범위 변경 절차**: <e.g. written change order required>

## Termination / 해지 조건

- **Termination clauses / 해지 조항**: <notice period, conditions>
- **Kill fee / 중도 해지 비용**: <amount or formula>

## Disputes / 분쟁

- **Governing law / 준거법**: <jurisdiction>
- **Dispute resolution / 분쟁 해결**: <arbitration | court | mediation>

## Contract document references / 계약 문서 참조

- Signed PDF / 서명된 PDF: `working/contracts/<filename>.pdf` (if stored locally)
- Cloud reference / 클라우드 원본: <link to DocuSign / Adobe Sign / etc.>
- Amendments / 수정본: list below
  - <YYYY-MM-DD>: <brief description> — `working/contracts/amendment-01.pdf`

## Amendment log / 수정 이력

Append every material change:

중요 변경 시마다 추가:

- <YYYY-MM-DD> — <what changed> — signed by <parties>
- <YYYY-MM-DD> — <...>
