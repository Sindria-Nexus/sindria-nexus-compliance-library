# AI Data and Model Change Control

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title — the AI governance owner] |
| **Review cadence** | Quarterly, and after any Tier 3 model change |
| **ISO 42001 mapping** | Annex A.6 (AI system life cycle), A.7 (Data for AI systems) |

## 1. Purpose

To control the two things that silently change an AI system's behavior
after deployment: its data and its model. A model update, a new prompt,
a new training source, or a vendor model change can alter outputs
without anyone shipping code — so this policy treats model and data
changes with the same discipline as software changes, and records them
where a reviewer can find them.

This template pairs with the change management policy for software
releases: code changes follow that policy; model, prompt, and data
changes follow this one, and a release containing both follows both.

## 2. Scope

- Training, fine-tuning, and evaluation data for in-house models.
- Prompts, system instructions, and retrieval sources for vendor-model
  features.
- Model versions, including vendor model versions the company does not
  control but depends on.
- Data the company's systems send to vendor models (inputs), and what
  comes back.

## 3. Data rules

### 3.1 Provenance and quality

For every dataset used to train, fine-tune, or evaluate a model,
record:

| Field | Meaning |
|---|---|
| Source | Where the data came from, and under what right (owned, licensed, public, customer-provided) |
| Contents | What kinds of data it holds, including personal data |
| Quality checks | What was checked before use (duplicates, errors, bias spot-checks, contamination) |
| Retention | How long it is kept, and when it is deleted |
| Owner | One named person accountable for it |

Data with unknown provenance or unclear rights is not used for Tier 2
or Tier 3 systems until the question is answered in writing.

### 3.2 Data that never goes where it should not

- Customer data, credentials, and non-public company data go only into
  approved tools listed in the AI system inventory — never into public
  AI tools, personal accounts, or unapproved vendor features.
- Personal data used in training or evaluation is minimized: the
  smallest set that achieves the purpose, and no more.
- Where a vendor model may train on inputs, customer data stays out
  until the vendor's terms say otherwise in writing.

### 3.3 Data incidents

Data leaked into a model, a dataset found to contain data it should
not, or a vendor disclosure that inputs were used for training is an
incident under the incident response policy, with the AI governance
owner involved. The affected dataset and model version are recorded,
and the response — including whether retraining or deletion is
required — is decided and documented, not improvised.

## 4. Model change control

### 4.1 What counts as a change

Any of: a new model version; a changed prompt or system instruction;
a changed retrieval source; a new training or fine-tuning dataset; a
vendor model update behind an API; a changed decision threshold or
safety filter. If it can change outputs, it is a change.

### 4.2 The change record

| Field | Meaning |
|---|---|
| System | Inventory name |
| Change | What changed, precisely (version numbers, prompt diff, dataset) |
| Reason | Why, in one sentence |
| Risk tier effect | Does the tier change? Does the impact assessment need updating? |
| Test | What was checked before release (evaluation set, spot checks, rollback plan) |
| Approver | AI governance owner for Tier 3; system owner for Tier 1/2 |
| Date | When it went live |
| Rollback | How to revert, and whether it was tested |

### 4.3 Tier 3 rules

- A Tier 3 model change requires an updated impact assessment (or a
  written note from the AI governance owner saying why the change
  does not affect the assessment) before release.
- The previous model version and its evaluation results are kept until
  the new version has run clean for [30 days].
- Rollback is tested, not assumed: the team can say how it reverts,
  and has done it at least once in a non-production setting.

### 4.4 Vendor model changes

Vendor models change without a release note you control. For Tier 2
and Tier 3 vendor-model systems:

- Pin the model version where the vendor allows it; where it does not,
  record the version in use at least weekly.
- Re-run the evaluation checks after any vendor-announced model
  update, and log the result.
- If outputs shift materially, treat it as an incident until the cause
  is understood.

## 5. Monitoring and retirement

Tier 3 systems are monitored for output quality, drift, complaint
patterns, and incident signals, reviewed at least quarterly. A system
is retired when it is replaced, its vendor ends it, or its risk
outweighs its benefit — retirement removes it from active use,
archives its inventory entry with a date, and deletes or returns its
data per the retention rules. Retired does not mean deleted from the
record.

## 6. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 7. Evidence this policy produces (Control AI-04)

| Evidence | Where it lives | Retention |
|---|---|---|
| Dataset records (source, rights, quality checks, retention) | [data records location] | Life of model + [3 years] |
| Model change records (change, test, approver, date, rollback) | [change log location] | Life of system + [3 years] |
| Tier 3 impact-assessment updates after model changes | [assessments location] | Life of system + [3 years] |
| Vendor model version log + post-update evaluation results | [monitoring location] | [3 years] |
| Monitoring reviews (quarterly, Tier 3) | [monitoring location] | [3 years] |

## 8. Where startups fail this control

1. **The vendor updated the model and nobody noticed.** Outputs shift,
   customers complain, and the team cannot say what changed or when.
   Version pinning and post-update checks are the whole control.
2. **Prompts as tribal knowledge.** The production prompt lives in
   someone's chat history, unversioned. A prompt change is a model
   change — record it like one, or the system is unreproducible.
3. **Training data with no provenance.** "We scraped it" is not a
   source, a right, or a quality check. When a buyer or auditor asks
   where training data came from, the answer is a record, not a shrug.

---

*What this template does not do: it does not evaluate your models for
you. It creates the record — versions, tests, approvals — that makes
evaluation repeatable and reviewable. A model nobody can reproduce is
a model nobody can defend.*
