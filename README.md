# Sindria Nexus Compliance Library

Free, genuinely usable starting templates for AI startups and small SaaS companies
preparing for SOC 2 and ISO 42001 — built by **Sindria Nexus** (readiness for AI & SaaS startups).

## What is in here

**Policies** (`/policies`) — eight Markdown policies mapped to the SOC 2 Trust
Services Criteria. Copy them, replace the bracketed placeholders with your own
details, and adopt them through your normal approval process:

| File | Covers | SOC 2 mapping |
|---|---|---|
| `01-information-security-policy.md` | Security program, roles, governance | CC1, CC2, CC7 |
| `02-access-control-policy.md` | Accounts, MFA, least privilege, joiner/mover/leaver | CC6.1–CC6.3, CC6.6 |
| `03-acceptable-use-policy.md` | What staff may and may not do with company systems | CC1, CC6 |
| `04-incident-response-policy.md` | Detect, contain, recover, learn | CC7.3, CC7.4 |
| `05-vendor-management-policy.md` | Choosing, reviewing, and offboarding vendors | CC9.2, CC6.1 |
| `06-change-management-policy.md` | Shipping changes safely, with review and rollback | CC8.1 |
| `07-data-classification-and-retention-policy.md` | Data classes, handling rules, retention | CC6.1, CC6.5 |
| `08-risk-assessment-policy.md` | Finding, scoring, and treating risk | CC3 |

**Tools** (`/tools`) — three working templates, not checklists about checklists:

| File | Use it to |
|---|---|
| `vendor-review-tracker.md` | Track every vendor, its data access, and its next review date |
| `access-review-template.md` | Run a quarterly access review and record who approved what |
| `security-questionnaire-answer-bank.md` | Starter answers for the questions enterprise buyers actually ask |

**ISO 42001 (`/iso-42001`)** — seven templates for governing AI under
ISO/IEC 42001:2023, in the same evidence-first style as the SOC 2 policies:

| File | Covers | ISO 42001 mapping |
|---|---|---|
| `01-ai-governance-policy.md` | AI policy, risk tiers, human oversight, deployment gate | A.2, A.3 |
| `02-ai-system-inventory.md` | Every AI system owned, tiered, and reviewed | A.3, A.4, A.6 |
| `03-ai-impact-assessment-template.md` | Impact assessment with signed deploy / do-not-deploy decision | A.5 |
| `04-ai-data-and-model-change-control.md` | Data provenance, model + prompt changes, vendor drift | A.6, A.7 |
| `05-iso-42001-readiness-checklist.md` | Phased path to certification + what auditors ask at each phase | Clauses 4–10, Annex A |
| `06-soc2-to-42001-evidence-map.md` | What SOC 2 evidence already proves, what to extend, what is new | Annex A (A.2–A.10) |
| `07-clause-mistakes-and-fixes.md` | Where teams fail each clause, with examples, the auditor's finding, and the fix | Clauses 4–10 |

**Index** — `controls-matrix.md` maps every control ID to its policy, Trust
Services Criterion, evidence, and cadence. Start there if you only read one
file.

## What makes these different

Most template packs tell you what to *say*. This one is built
**evidence-first** — around the question an auditor actually asks, which is
never "do you have a policy?" but "show me it working":

- **Every policy names its evidence.** Each policy ends with an "Evidence
  this policy produces" table: the exact artifact, where it lives, and how
  long to keep it. If you maintain those artifacts, the audit assembles
  itself.
- **Every policy carries a control ID** (IS-01 through RA-01), indexed in
  `controls-matrix.md`. Cite a control ID in a questionnaire answer and
  the buyer — or auditor — can trace it to the policy and its evidence in
  one hop.
- **Every policy names where startups fail it.** The "Where startups fail
  this control" notes are the findings auditors actually write: reviewers
  reviewing their own access, leavers revoked weeks late, SOC 2 reports
  from two years ago treated as current, blank risk registers. Read those
  before you adopt, and you skip the most common first-audit findings.
- **AI-startup specifics, not generic SaaS.** The AI-tools rule (no
  customer data in public AI tools), the approved-tools register, and the
  questionnaire answers on model training and AI data handling are written
  for the teams this library is for — the ones whose product *is* an AI
  system, not just a company that happens to use one.

## Start here in 30 minutes

1. Read `controls-matrix.md` — one page, the whole program at a glance.
2. Open `tools/security-questionnaire-answer-bank.md` and answer the AI
   and model-training questions honestly. Those are the ones enterprise
   buyers ask AI startups first, and they are the ones most teams fumble.
3. Fill in `tools/vendor-review-tracker.md` with every tool that touches
   customer data — including free tiers. The empty tracker is the most
   common gap auditors find.
4. Then read `TAILORING-GUIDE.md` and adopt one policy properly, with an
   owner and an approval, rather than adopting all eight on paper.

## How to use these

1. Copy the files into your own repo or docs.
2. Replace every `[bracketed placeholder]` — company name, owner, dates, tools.
3. Get each policy approved by whoever owns it at your company, then publish it
   where your team will actually read it.
4. Set the review dates. A policy nobody reviews is evidence of nothing.

## What these templates do NOT do

This is the honest part, and it matters. A template is a starting point, not
readiness:

- **They are not tailored to your stack.** Your infrastructure, vendors, and data
  flows are specific. A generic policy that does not describe your real systems
  will not survive an auditor's questions.
- **They are not evidence.** Auditors ask for proof — tickets, logs, review
  records, screenshots. Templates describe what you do; evidence proves you did it.
- **They are not an audit outcome.** Nothing here guarantees a SOC 2 report.
  Readiness is the work of implementing, operating, and evidencing controls over
  time.

If you want help turning these into a tailored, evidenced control set, that is
what Sindria Nexus does: start with a free 30-minute Stalled Deal Triage at
[sindrianexus.com](https://sindrianexus.com), or the flat-fee SOC 2 Readiness
Diagnostic.

## Who these are for

AI startups and small SaaS teams selling to enterprise customers — the teams
that first meet SOC 2 as row 12 of a 140-row security questionnaire, six weeks
before a deal dies in silence. If that is you, start with the questionnaire
answer bank, then the access control and vendor policies. Those three cover the
questions buyers ask first.

## License

MIT — use them commercially, modify them, keep them private. Attribution is
appreciated but not required. See `LICENSE`.

## A note on staying current

SOC 2 criteria and auditor expectations change. This library grows over time —
new templates and revisions land here as they are written. Check back, and
pin a version when you adopt a policy so your approved copy does not drift.

---

*Built by Sindria Nexus. These templates are educational starting points, not
legal advice and not a substitute for advice tailored to your company.*
