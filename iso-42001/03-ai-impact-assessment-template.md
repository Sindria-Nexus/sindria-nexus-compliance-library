# AI Impact Assessment Template

| | |
|---|---|
| **Company** | [Company Name] |
| **System** | [System name — must match its inventory entry] |
| **Owner** | [Name, Title — the system owner] |
| **Assessor** | [Name, Title — not the system owner alone for Tier 3] |
| **Assessment date** | [YYYY-MM-DD] |
| **Next review** | [Date — at least annually, and after any major model change] |
| **ISO 42001 mapping** | Annex A.5 (Assessing impacts of AI systems) |

## 1. Purpose

To assess, before deployment and at least annually after, what an AI
system does to individuals, groups, and society — and to record the
mitigations and the sign-off. Required for every Tier 3 system under
the AI governance policy, and good practice for any Tier 2 system whose
output reaches customers.

An impact assessment is a decision record, not a formality. If it
cannot change the deployment decision, it is theater. A completed
assessment that concludes "do not deploy" or "deploy with these
conditions" is a successful assessment.

## 2. When it is required

- Before the first deployment of any Tier 3 system.
- Again after any major model change (new model version, new training
  data source, new data type, new decision the system is allowed to
  make).
- At least annually for every live Tier 3 system.
- After any AI incident involving the system.

## 3. The assessment

### 3.1 The system, plainly

| Question | Answer |
|---|---|
| What does the system do, in one paragraph a non-engineer can follow? | [ ] |
| What decision or output does it produce, and who acts on it? | [ ] |
| What data does it use (training data, inputs, personal data)? | [ ] |
| Who is affected if it is wrong — individuals, groups, customers, the public? | [ ] |
| What human oversight applies, and can the human genuinely override it? | [ ] |

### 3.2 Benefits

| Benefit | Who gains it | How it will be checked |
|---|---|---|
| [ ] | [ ] | [ ] |

A benefit nobody can check is a claim, not a benefit. If the benefit
is "faster decisions," say faster by how much, measured how.

### 3.3 Risks and harms

For each risk, score it before and after mitigation. Use the same
honesty as the risk register: a risk left blank is a risk accepted
without a decision.

| Risk / harm | Who is harmed | Likelihood (1–5) | Severity (1–5) | Mitigation | Residual likelihood | Residual severity |
|---|---|---|---|---|---|---|
| Biased or unfair output (wrongful denial, skewed scoring) | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| Privacy harm (personal data exposed, inferred, retained) | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| Safety harm (wrong advice or action with physical or financial consequence) | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| Transparency harm (affected people cannot understand or challenge the outcome) | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| Security harm (prompt injection, data poisoning, model theft) | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| Societal harm (effects beyond the individual user, at scale) | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |
| [Other: ] | [ ] | [ ] | [ ] | [ ] | [ ] | [ ] |

### 3.4 Mitigations that actually mitigate

A mitigation names an owner and a check, or it is not a mitigation:

| Mitigation | Owner | How it will be checked | Check date |
|---|---|---|---|
| [ ] | [ ] | [ ] | [ ] |

"Monitor closely" is not a mitigation. "Weekly sample of 50 outputs
reviewed by [name], logged in [location]" is.

### 3.5 Decision

| | |
|---|---|
| **Decision** | Deploy / Deploy with conditions / Do not deploy |
| **Conditions (if any)** | [ ] |
| **Residual risks accepted** | [Each accepted residual risk, with rationale and sign-off] |
| **Approved by** | [AI governance owner, signature, date] |
| **System owner sign-off** | [Signature, date] |

Accepted residual risk is a signed decision with a re-review date, not
an omission. Re-review is at the next scheduled assessment at the
latest.

## 4. Evidence this assessment produces (Control AI-03)

| Evidence | Where it lives | Retention |
|---|---|---|
| Completed assessment (system, risks, mitigations, decision, sign-offs) | [assessments location] | Life of system + [3 years] |
| Re-assessments after major model changes | [assessments location] | Life of system + [3 years] |
| Mitigation check records (samples reviewed, logs) | [monitoring location] | [3 years] |

## 5. Where startups fail this control

1. **Assessment after deployment.** Written to justify a system already
   live, it can only conclude "deploy." The assessment gates the
   deployment — before means before.
2. **Copy-paste risks.** Every system's risk table identical to the
   last one's tells a reviewer nobody thought about this system. The
   risks that matter are the specific ones: this data, these people,
   this failure mode.
3. **Mitigations without owners.** A mitigation list with no owner and
   no check date is a wish list. When the audit asks "show me it
   working," the check records are the answer — or the absence is.

---

*What this template does not do: it does not give legal advice, and it
does not map your system to the EU AI Act or any other regulation.
Teams with Tier 3 systems affecting people in regulated contexts
should have the assessment reviewed by qualified counsel. What it does
is make the impact conversation written, signed, and re-reviewed —
which is the part most teams skip entirely.*
