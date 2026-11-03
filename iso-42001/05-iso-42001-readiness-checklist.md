# ISO 42001 Readiness Checklist

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title — the AI governance owner] |
| **Scope** | [Which AI systems, teams, and business units are in the AI management system — and what is explicitly out, with reasons] |
| **ISO 42001 mapping** | Clauses 4–10 (the management system) + Annex A (A.2–A.10) |

## 1. Purpose

The phased path from "we use AI" to "we can pass a certification
audit" — and, at each phase, what the auditor will actually ask for.
Most teams fail ISO 42001 not on the hard parts but on sequencing:
they write a policy before they know what AI they run, or they book a
certification audit before anything has operated long enough to leave
evidence. This checklist fixes the order.

Planning estimate for a small company with a tight AI scope: roughly
4–9 months from gap analysis to certificate, driven mostly by scope
and by how much evidence already exists. That is a planning range,
not a promise — a company with five AI systems and a working SOC 2
program moves faster than a company with fifty systems and no
inventory. The phases below are the reason for the range: you cannot
skip one and buy it back later.

## 2. The phases

### Phase 0 — Scope (before anything else)

- [ ] AIMS scope written down: which AI systems, teams, products, and
  sites are in, and what is out — with a reason for every exclusion.
- [ ] Scope approved by leadership, not just the AI owner.

**Auditor asks:** "Show me the scope statement." Exclusions without
reasons are the first thing that gets challenged.

### Phase 1 — Governance (Clauses 5–7, Annex A.2–A.3)

- [ ] AI governance policy approved and published where staff read it
  (see `01-ai-governance-policy.md`).
- [ ] AI governance owner named, with authority to stop a deployment.
- [ ] Roles assigned: system owners per system, assessors who are not
  the system owner alone for Tier 3.
- [ ] A way to raise AI concerns, without penalty, that is actually
  answered.

**Auditor asks:** "Who owns AI governance, and show me a decision they
made." A policy with no decision behind it is paper.

### Phase 2 — Know what you run (Annex A.3–A.4)

- [ ] AI system inventory complete (see
  `02-ai-system-inventory.md`): every system, vendor feature, and
  free tier — owned, tiered, data flows recorded.
- [ ] Quarterly inventory review running (not just scheduled).
- [ ] Shadow AI hunt done once: ask the team, walk the vendor list,
  walk the expense report.

**Auditor asks:** "Show me the inventory, and show me a system you
found after the first pass." The second part is the tell — teams that
never find shadow AI are teams that never looked.

### Phase 3 — Impact assessments (Annex A.5)

- [ ] Every Tier 3 system has a signed impact assessment before
  deployment (see `03-ai-impact-assessment-template.md`).
- [ ] Assessments re-done after major model changes, at least
  annually.
- [ ] Mitigations have owners and check dates — and the checks exist.

**Auditor asks:** "Show me an assessment that changed a decision."
An assessment that always concludes "deploy" is a rubber stamp, and
auditors read it as one.

### Phase 4 — Data and life-cycle controls (Annex A.6–A.7, A.9–A.10)

- [ ] Dataset records: source, rights, quality checks, retention
  (see `04-ai-data-and-model-change-control.md`).
- [ ] Model change records: version, prompt diff, test, approver,
  rollback — including vendor model changes.
- [ ] Human oversight operating for Tier 3, with overrides logged.
- [ ] Vendor AI terms reviewed for every Tier 2/3 vendor system;
  unknowns carry no customer data.
- [ ] Transparency: affected people can understand and challenge
  outcomes that touch them (Annex A.8).

**Auditor asks:** "Show me a model change and its test, and show me
what happened the last time a vendor changed a model underneath you."
If the answer is "we didn't notice," Phase 4 is not done.

### Phase 5 — Internal audit and management review (Clauses 9–10)

- [ ] Internal audit of the AIMS performed by someone independent of
  the AI program — findings recorded, not softened.
- [ ] Findings closed or formally accepted with dates, before the
  certification audit.
- [ ] Management review meeting held and minuted: scope, risks,
  incidents, audit results, what changes next.

**Auditor asks:** "Show me your internal audit findings and what you
did about them." An internal audit with zero findings is not a clean
bill of health — it is evidence nobody looked hard.

### Phase 6 — Certification (the audit itself)

- [ ] Accredited certification body selected (accreditation matters —
  a certificate from a non-accredited body is a PDF, not a credential).
- [ ] Stage 1 audit: documentation review. Gaps closed before Stage 2.
- [ ] Stage 2 audit: evidence the system operated — inventory reviews,
  assessments, change records, monitoring, management review minutes.
  This is the audit that takes months of operating history, which is
  why the timeline cannot be compressed to weeks.
- [ ] Surveillance audits planned (typically annual) — certification
  is maintained, not won once.

**Auditor asks:** everything above, as evidence, over a period. Stage
2 does not test whether you wrote the system down. It tests whether
you ran it.

## 3. You are ready for Stage 1 when…

- The inventory has survived two quarterly reviews with changes.
- At least one Tier 3 assessment exists with a real decision in it.
- At least one model change has a complete record, including rollback.
- The internal audit found something, and the finding is closed.
- Management review minutes exist and name actions with owners.

If any of those is missing, you are not ready — and booking the audit
anyway is how teams pay for a failed Stage 1 and learn the same lesson
more expensively.

## 4. What slows teams down (the honest list)

1. **Shadow AI discovery.** The inventory is never complete on the
   first pass. Budget a full cycle for finding what staff actually use.
2. **Vendor answers.** "What do you train on?" can take weeks per
   vendor, and some vendors never answer — which means customer data
   stays out and the system stays Tier 3 by default.
3. **Tier 3 assessments.** A real assessment takes days of thought,
   not an afternoon of form-filling. Teams with many Tier 3 systems
   should tier ruthlessly and honestly — not everything is Tier 3.
4. **Operating history.** Stage 2 needs months of records. Starting
   the clock late is the one delay no amount of effort buys back.

## 5. Evidence this checklist produces (Control AI-05)

| Evidence | Where it lives | Retention |
|---|---|---|
| Completed checklist (phases signed off with dates) | [program location] | Life of certification + [3 years] |
| Scope statement with exclusions and reasons | [program location] | Current + prior versions [3 years] |
| Internal audit report + finding closures | [audit location] | [3 years] |
| Management review minutes with actions and owners | [governance location] | [3 years] |

---

*What this template does not do: it does not guarantee certification,
and it does not replace the standard itself — read ISO/IEC 42001:2023
Annex A alongside this checklist, and have your certification body
confirm scope and timing for your situation. What it does is stop the
two most expensive mistakes: building in the wrong order, and booking
an audit before there is anything to audit.*
