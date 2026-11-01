# Risk Assessment Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual formal assessment; register reviewed quarterly |
| **SOC 2 mapping** | CC3 (Risk Assessment) |

## 1. Purpose

To find risks before customers or auditors do, score them honestly, and
treat them in priority order — with an owner and a date on every treatment.

## 2. Scope

All risks to the security, availability, and integrity of company and
customer data, including vendor risk, people risk, and infrastructure risk.
Fraud risk and business risk are in scope where they touch customer data or
system integrity.

## 3. The risk register

All identified risks live in one register — a document or tracker owned by
the policy owner — with these fields:

| Field | Meaning |
|---|---|
| Risk | What could happen, in one sentence |
| Cause | What makes it possible |
| Impact (1–5) | Harm if it happens: 1 negligible, 5 existential |
| Likelihood (1–5) | Chance in the next 12 months: 1 rare, 5 almost certain |
| Score | Impact × Likelihood |
| Owner | One named person accountable for treatment |
| Treatment | Accept / Mitigate / Transfer / Avoid, with the action |
| Due date | When treatment completes |
| Status | Open / In progress / Treated / Accepted |

## 4. Scoring and appetite

- **Score 1–4:** monitor; no formal treatment required.
- **Score 5–9:** treat within [90 days] or formally accept with a written
  rationale signed by [founder / CEO].
- **Score 10–16:** treat within [30 days]; leadership reviews progress weekly.
- **Score 17–25:** treat immediately; leadership reviews daily until the
  score drops.

Accepting a risk is a decision, not an omission: it is written, signed,
dated, and re-reviewed at the next quarterly register review.

## 5. Assessment process

The formal annual assessment runs in four steps:

1. **Identify.** Brainstorm with engineering, operations, and leadership;
   review the previous register, incident history, vendor reviews, and
   audit findings. Add new risks; close risks that no longer apply, with a
   reason recorded.
2. **Score.** Score each risk with the owner in the room, not in absentia.
   Disagreements are resolved by the policy owner and recorded.
3. **Treat.** Assign every risk above appetite an owner, a treatment, and a
   due date. Treatment plans are tracked in the register, not in someone's
   head.
4. **Report.** The assessment summary goes to [founder / leadership team]:
   top risks, accepted risks, overdue treatments, and what changed since
   last year.

Between formal assessments, new risks are added to the register as they are
identified — after an incident, a vendor change, or a new product launch —
and scored at the next quarterly review at the latest.

## 6. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 7. Evidence this policy produces (Control RA-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Risk register (every risk scored, owned, dated) | [register location] | Current + prior versions [1 year] |
| Annual assessment summary to leadership (top risks, accepted risks, overdue treatments) | [docs location] | [3 years] |
| Accepted-risk sign-offs (written, signed, dated, re-reviewed quarterly) | [register] | [3 years] |
| Overdue treatment escalation records | [register / tracker] | [1 year] |

## 8. Where startups fail this control

1. **A blank register.** The single finding no auditor misses. Start with
   ten honest risks — lost laptop, vendor breach, key leak, single-person
   dependency, unreviewed access — and the register becomes the most
   useful document you own.
2. **Risks accepted verbally.** "We decided to live with it" is not an
   acceptance. An accepted risk needs a signature, a date, and a
   re-review — otherwise it is an omission wearing a decision's clothes.
3. **Treatments overdue with no escalation.** A register full of past-due
   treatments with no escalation record tells the auditor the process
   runs on paper only. Overdue means escalated, visibly, in the register.

---

*What this template does not do: it does not contain your risks. A blank
register is the one finding no auditor will miss — start with ten honest
risks (lost laptop, vendor breach, key leak, single-person dependency,
unreviewed access) and the register becomes the most useful document you own.*
