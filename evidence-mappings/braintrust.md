Last verified: November 11, 2026

# Braintrust — Evidence Mapping

## What Braintrust is

Braintrust is an evaluation-first platform for AI apps and agents: production traffic is logged as traces, failures are promoted into versioned datasets, experiments score prompt/model/code changes against a baseline, and the same scorers run online over live logs. For a readiness engagement, the logs are the audit trail and the experiment record is the verification-and-validation evidence — but retention is short on the lower tiers, so long-term evidence needs export or a paid retention extension.

## Mapping — evidence you already have

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Production logs and traces — every LLM call, tool call and retrieval step captured as nested spans with inputs, outputs, latency, tokens and cost | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Only auto-instrumented providers and decorated spans are captured — document tracing coverage in scope (see Honest flags). |
| Online scoring on live logs — the same scorers used offline run asynchronously on production traffic, with scores attached to each log row | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs thresholds and escalation documented. |
| Topics, Patterns and BTQL search — a daily pass classifies traces and clusters recurring failures; logs, experiments and datasets are queryable via BTQL | A.6.2.6 Operation and monitoring; A.6.2.8 Recording of event logs | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | In hand | — |
| Versioned datasets and experiments — datasets are versioned; each experiment pins to a dataset version and records inputs, outputs, expected values and scores vs a baseline. Failures promote from logs in one click | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| Scorers and human review — autoevals, custom code scorers and LLM-as-judge in one framework; human review is the ground-truth check on automated scorers | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs named reviewers and a review cadence. |
| Versioned prompts and CI eval gates — every prompt edit creates a version with diff and comment, assigned to an environment (e.g. production) for instant rollback. A GitHub Action runs evals in CI, posting regressions vs baseline | A.6.2.5 Deployment; A.6.2.7 Technical documentation | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named approver for production. Quality gates can block merges when metrics degrade below thresholds. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Braintrust gives you the evidence. ISO 42001 makes it certifiable — the policy, risk and accountability wrapper an auditor can test.

## Honest flags

- **Log retention is short: 14 days on Starter, 30 days on Pro** (confirmed against Braintrust's pricing and retention docs, November 2026). Pro retention can be extended to 180 days at $0.50 per GB per month, in 30-day increments; retention storage is billed on the highest amount retained during the billing month, so extending mid-month is not prorated. Enterprise retention is custom, up to 365 days. Export for long-term evidence — S3 export is Enterprise-only.
- **Retention applies to logs and playground data — experiments are kept up to 365 days on all plans.** The eval record outlasts the raw traces that produced it; do not assume the underlying logs are still there when an auditor asks.
- **Tracing covers auto-instrumented providers and decorated spans only.** Uninstrumented calls leave no trace, so coverage must be documented in scope.
- **Admin audit logs, SAML SSO and the BAA are Enterprise-only**, as are self-hosted / BYOC data planes. On Starter every member is an Owner — there is only one permission group — so access control evidence on the free tier is thin.
- **Topics is an AI feature that runs on Braintrust's built-in models unless you supply your own key** (model credits cover Topics and other built-in models). Confirm where classification runs before enabling Topics in a BYOC or self-hosted deployment, and note it in your data-handling scope.

## Sources

- Braintrust docs — Configure data retention: <https://docs.braintrust.dev/admin/data-management/retention>
- Braintrust docs — Access control (permission groups by plan): <https://docs.braintrust.dev/admin/access-control>
- Braintrust docs — Plans and limits: <https://docs.braintrust.dev/plans-and-limits>
- Braintrust pricing (retention: Starter 14 days, Pro 30 days, extendable to 180 days; Enterprise to 365 days): <https://www.braintrust.dev/pricing>
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
