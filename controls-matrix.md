# Controls Matrix

The one-page index auditors build first — so this library builds it for
you. Every policy in this library maps to a control ID, a Trust Services
Criterion, the evidence that proves it operates, and the cadence that keeps
it alive. Use this matrix as the table of contents for your audit evidence:
when an auditor asks for a control, this row tells you exactly what to hand
them.

| Control | Control name | Policy | SOC 2 mapping | Evidence that proves it | Cadence |
|---|---|---|---|---|---|
| IS-01 | Security program governance | `policies/01-information-security-policy.md` | CC1, CC2, CC7 | Quarterly review minutes, training records, approval signatures, exception log | Quarterly review; annual policy review |
| AC-01 | Logical access | `policies/02-access-control-policy.md` | CC6.1–CC6.3, CC6.6 | Onboarding tickets, MFA report, signed quarterly reviews, leaver checklists, break-glass log, key rotation log | Quarterly review; monthly privileged review |
| AU-01 | Acceptable use | `policies/03-acceptable-use-policy.md` | CC1, CC6 | Signed acknowledgments, training records, approved-tools register, device enrollment report | Annual policy review |
| IR-01 | Incident response | `policies/04-incident-response-policy.md` | CC7.3, CC7.4 | Incident records, post-incident reviews, tabletop record, restore test records, notification records | Annual review; after every incident |
| VM-01 | Vendor management | `policies/05-vendor-management-policy.md` | CC9.2, CC6.1 | Completed tracker, vendor evidence on file, signed DPAs, offboarding confirmations | Critical/Important annual; Low every 2 years |
| CM-01 | Change management | `policies/06-change-management-policy.md` | CC8.1 | PR approvals (author ≠ approver), deployment log, emergency retrospectives, rollback records | Annual policy review; per change |
| DC-01 | Data classification & retention | `policies/07-data-classification-and-retention-policy.md` | CC6.1, CC6.5 | Classified data inventory, retention/deletion records, subject-request log, signed DPAs | Annual policy review |
| RA-01 | Risk assessment | `policies/08-risk-assessment-policy.md` | CC3 | Risk register, annual assessment summary, accepted-risk sign-offs, escalation records | Quarterly register review; annual assessment |

## ISO 42001 controls

| Control | Control name | Template | ISO 42001 mapping | Evidence that proves it | Cadence |
|---|---|---|---|---|---|
| AI-01 | AI governance | `iso-42001/01-ai-governance-policy.md` | A.2, A.3 | Approved policy, inventory, Tier 3 assessments, deployment approvals, concern log | Annual review; per Tier 3 deployment |
| AI-02 | AI system inventory | `iso-42001/02-ai-system-inventory.md` | A.3, A.4, A.6 | Current inventory, quarterly review records, retired entries kept | Quarterly review |
| AI-03 | AI impact assessment | `iso-42001/03-ai-impact-assessment-template.md` | A.5 | Signed assessments, re-assessments after model changes, mitigation check records | Per Tier 3 deployment; annual |
| AI-04 | AI data & model change control | `iso-42001/04-ai-data-and-model-change-control.md` | A.6, A.7 | Dataset records, model change records, vendor version log, monitoring reviews | Quarterly; per change |
| AI-05 | ISO 42001 readiness | `iso-42001/05-iso-42001-readiness-checklist.md` | Clauses 4–10, Annex A | Completed checklist, scope statement, internal audit report, management review minutes | Per phase; annual |
| AI-06 | SOC 2 to 42001 evidence map | `iso-42001/06-soc2-to-42001-evidence-map.md` | Annex A (A.2–A.10) | Completed map, reuse claims, gap closure records | Per program; on change |
| AI-07 | Clause mistakes and fixes | `iso-42001/07-clause-mistakes-and-fixes.md` | Clauses 4–10 | Clause self-tests completed, gate records, audit reports, nonconformity log with effectiveness checks | Per clause; on change |

## How to use this matrix in an audit

1. **Point-in-time (Type 1):** the auditor tests whether each control is
   *designed* — the policy exists, is approved, and describes your real
   systems. The Policy column is your answer.
2. **Over a period (Type 2):** the auditor tests whether each control
   *operated* for 6–12 months. The Evidence column is your answer — and
   the Cadence column is why gaps in the timeline become findings.
3. **Before either:** pick one row, follow it to its evidence, and check
   you could produce that evidence within an hour. Any row you cannot is
   your next piece of work.

## A note on scope

This matrix covers the control set most AI startups and small SaaS teams
need first. It is not the full Trust Services Criteria — a complete SOC 2
program also covers areas like system monitoring (CC7.2), availability
commitments (A1), and confidentiality commitments (C1) where they apply to
your business. Treat this matrix as the foundation, and extend it with
control IDs in the same format as your program grows.

---

*Built by Sindria Nexus. These templates are educational starting points, not
legal advice and not a substitute for advice tailored to your company.*
