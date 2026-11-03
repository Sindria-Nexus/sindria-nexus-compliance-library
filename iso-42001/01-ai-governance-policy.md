# AI Governance Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title — the AI governance owner] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual, and after any Tier 3 deployment, incident, or major model change |
| **ISO 42001 mapping** | Annex A.2 (Policies related to AI), A.3 (Internal organization) |

## 1. Purpose

To govern every AI system the company builds, buys, or uses — so that AI
is deployed deliberately, with a named owner, a risk tier, and human
oversight where the output matters — and so the company can show a
certification reviewer how its AI is governed, not just that it has a
policy saying so.

This policy is the top of the company's AI management system (AIMS). The
companion templates carry the working parts: the AI system inventory
(`02-ai-system-inventory.md`), the impact assessment
(`03-ai-impact-assessment-template.md`), and data and model change
control (`04-ai-data-and-model-change-control.md`).

## 2. Scope

All AI systems, including:

- AI features in the company's own product (models built in-house and
  models called through a vendor API).
- Third-party AI tools used by staff (coding assistants, writing tools,
  support bots, analytics) — including free tiers.
- AI systems embedded in vendor products where the vendor's model touches
  company or customer data.

A spreadsheet macro is not an AI system. Anything that generates content,
makes a recommendation, classifies, scores, or decides — including a
vendor feature with "AI" in the name — is in scope until the AI
governance owner says otherwise in writing.

## 3. Principles

Every AI system in scope must satisfy these principles, or it does not
ship:

1. **A named human owns it.** Every system has one owner accountable
   for its behavior, its data, and its retirement.
2. **No silent automation of consequential decisions.** Where an AI
   output affects a person's access, money, employment, safety, or legal
   position, a human reviews it before it takes effect (see §5).
3. **Data in, data out, documented.** What data a system trains on or
   is prompted with, and what it returns, is recorded in the inventory.
4. **No customer data in public AI tools.** Customer data, credentials,
   and non-public company data go only into approved tools listed in
   the inventory. This rule is absolute — it is the AI-tools rule the
   rest of the library already enforces.
5. **If it cannot be explained, it cannot be defended.** For Tier 3
   systems, the team must be able to say, in plain language, what the
   system does, what data it uses, and how a wrong output is caught.

## 4. Risk tiers

Every system in the inventory carries one tier, assigned by the AI
governance owner with the system owner. Tiers are about impact, not
about how impressive the model is:

| Tier | Meaning | Examples |
|---|---|---|
| **Tier 1 — Low** | Internal productivity use; no customer data; no decision about a person | Drafting help, code completion on non-sensitive code, meeting notes |
| **Tier 2 — Limited** | Customer-facing or customer-data-touching, but a human reviews the output before it matters | Support-draft replies, marketing copy, internal summarization of customer tickets |
| **Tier 3 — High** | Automated output that affects an individual's access, money, employment, safety, or legal position; or a safety-critical function | Credit or fraud scoring, hiring or screening, medical or safety advice, autonomous actions on a customer's systems |

Tier 3 is the only tier that requires a completed impact assessment
before deployment (§6) and periodic re-assessment after any major model
change. If a system's tier is disputed, it is treated as the higher tier
until the AI governance owner rules in writing.

## 5. Human oversight

- **Tier 1:** no formal oversight beyond the inventory entry.
- **Tier 2:** a human reviews AI output before it reaches a customer or
  enters a record. Sampling is not enough where the output is
  customer-visible — review it, or do not send it.
- **Tier 3:** human review before the output takes effect, with the
  reviewer able to override, and overrides logged. Fully autonomous
  Tier 3 decisions are prohibited.

Oversight is real work, not a checkbox: the reviewer must have the
information and the authority to disagree with the system, and enough
time to do it. A reviewer rubber-stamping a hundred outputs an hour is
not oversight, and an auditor will treat it as such.

## 6. Deployment gate

No Tier 2 or Tier 3 system goes live without:

1. An inventory entry (system, owner, vendor/model, data in/out, tier).
2. For Tier 3: a completed, signed impact assessment.
3. For Tier 3: the oversight arrangement named (§5) and tested once
   with a real example, including an override.
4. Approval from the AI governance owner, recorded with a date.

Vendor AI features that arrive inside a product the company already
uses are not exempt: when a vendor ships a new AI feature that touches
company data, it enters the inventory and the gate before staff use it
for anything beyond Tier 1.

## 7. Roles

| Role | Responsibility |
|---|---|
| AI governance owner | Owns this policy, assigns tiers, approves Tier 3 deployments, runs the annual review |
| System owner | Owns one system's inventory entry, impact assessment, monitoring, and retirement |
| All staff | Use only approved tools; report AI concerns (wrong outputs, data leaks, vendor surprises) to the AI governance owner |

Concerns may be raised without penalty. A reported concern is logged,
assessed, and answered — silence is how small AI problems become audit
findings.

## 8. Third-party AI

Vendor AI is governed, not trusted on the vendor's word:

- The vendor, model, and data flows are recorded in the inventory.
- The vendor's AI and data terms are reviewed before Tier 2 or Tier 3
  use — especially whether vendor models train on customer inputs.
- If a vendor will not say what happens to your data, the system is
  Tier 3 by default and customer data stays out until the answer is in
  writing.

## 9. Incidents and monitoring

AI incidents — wrong outputs with real consequences, data leaked into a
model, a vendor model change that alters behavior — are handled under
the incident response policy, with the AI governance owner involved.
Tier 3 systems are monitored for drift, output quality, and complaint
patterns; monitoring results are reviewed at least quarterly.

## 10. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 11. Evidence this policy produces (Control AI-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Approved AI governance policy with owner and review date | [docs location] | Current + prior versions [3 years] |
| AI system inventory (every system tiered, owned, dated) | [inventory location] | Current + prior versions [3 years] |
| Tier 3 impact assessments, signed before deployment | [assessments location] | Life of system + [3 years] |
| Tier 3 deployment approvals (owner, date, override test) | [approvals location] | [3 years] |
| AI concern log (raised, assessed, answered) | [log location] | [3 years] |

## 12. Where startups fail this control

1. **Shadow AI.** The inventory lists three systems; staff actually use
   twelve. Free tiers and browser extensions are where governance goes
   to die. Ask the team what they actually use, and check the vendor
   list against it — the gap is the finding.
2. **A policy with no gate.** "We govern AI responsibly" means nothing
   if a Tier 3 system can ship without an assessment or an approval.
   The deployment gate (§6) is the control; the policy is the paper
   around it.
3. **Oversight theater.** A human "reviewing" AI output at a speed no
   human could actually review is worse than no review, because it
   teaches the organization to sign things it has not read.
4. **Vendor AI treated as vendor magic.** "The vendor handles it" is
   not a data flow, not a term review, and not an answer to what the
   model trains on. If the vendor will not answer, customer data stays
   out.

---

*What this template does not do: it does not make you ISO 42001
certified, and it does not map your systems to the EU AI Act — teams
selling into the EU should map Tier 3 systems to their EU AI Act
obligations separately. Certification is granted by an independent
body, on evidence that this system actually operates — the inventory,
the assessments, and the approvals above are where that evidence
starts.*
