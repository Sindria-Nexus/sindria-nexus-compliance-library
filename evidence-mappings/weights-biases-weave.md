Last verified: November 11, 2026

# Weights & Biases Weave — Evidence Mapping

## What the platform is

**W&B Weave** is the LLM evaluation and observability layer of Weights & Biases: tracing of LLM calls, tool invocations, and agent steps; versioned datasets and Evaluations with scorers; and production scoring of live traffic. Weights & Biases was acquired by **CoreWeave** (completed 5 May 2025); Weave docs and pricing now live under CoreWeave Forge at docs.coreweave.com/weave. On 30 September 2026 CoreWeave launched **Agent Lens** (Public Preview), now described as the recommended experience for tracing, monitoring, and analysing agents — Weave continues to cover what Agent Lens does not yet support: evaluations, function-level traces with Ops and Calls, and guardrails. The two share trace data.

## Mapping — platform artifact → ISO 42001 Annex A / SOC 2 CC

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| End-to-end tracing with `@weave.op()` — every LLM call, tool invocation, and agent step captured with inputs, outputs, code version, cost, and latency as a nested trace tree | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Tracing covers decorated ops and supported integrations only — document coverage in scope. |
| Monitors and Signals on production traces — the same scorers used in evaluation score live traffic; built-in signals flag hallucination, toxicity, PII, and bias | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs thresholds and escalation documented. See flags: Monitors are the previous approach — new implementations use Signals; built-in signals flag, they do not block. Blocking or modifying a response is done by guardrails, which your application code applies. |
| Human feedback and annotation queues — annotations and corrections on production traces, routed to domain experts; feedback becomes new test cases | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs named reviewers and a review cadence. |
| Versioned datasets and Evaluations — curated datasets run through an Evaluation; each run records outputs, scores, and traces per version, compared on leaderboards | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| Scorers — code, LLM-as-judge, and human — deterministic checks (exact match, regex), model-graded scorers, and human review in the same evaluation, plus built-in safety scorers | A.6.2.4 Verification and validation; A.7.4 Quality of data | CC4.1 Monitoring activities; CC7.2 System operations | In hand | — |
| Automatic versioning — prompts, data, models, code — every op call creates a new version when its code changes; prompts, datasets, and model configs are version-tracked, so results reproduce | A.6.2.5 Deployment; A.6.2.7 Technical documentation | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named approver for production. |

## The gap band — what Weave does not give you

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Weave gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Docs and ownership moved.** Weave is now a CoreWeave product (acquisition completed May 2025). Vendor docs are at docs.coreweave.com/weave, not wandb.ai/docs — cite the current location in evidence.
- **Agent tracing/monitoring has a new recommended home.** Agent Lens (launched 30 September 2026, Public Preview) is CoreWeave's recommended experience for agent tracing and monitoring. Weave remains the home for evaluations, function-level traces, and guardrails; both read the same trace data, so no migration is needed.
- **Monitors are the previous approach.** The Monitors page now points new implementations to **Signals** (Weave for Agents), which score agent turns as tags (e.g. `user-frustration`, `nsfw`) or ratings from 0 to 1, including via a customer-hosted HTTP scorer.
- **Monitors score root traces, not child spans.** Built-in quality signals (hallucination, user frustration, jailbreaking, and others) run on successful root-level traces, and error signals on failed traces; child spans and intermediate calls are not scored. Document that coverage limit in scope.
- **Signals flag; guardrails are code you write.** Built-in Signals flag live traces. A scorer only blocks or modifies a response when your application code applies it as a guardrail — the enforcement decision is yours to build and evidence.
- **SDK breaking change reported in v0.54.0 (23 October 2026).** `weave.shared` and the `weave.trace_server` alias modules were reported removed; ops saved with code importing them load as `None`. This was corroborated by a third-party check of the release notes, not verified against Weave's own release notes on this check — confirm against the release notes before citing in evidence. Pin and test the SDK version in evidence.

## Sources

- CoreWeave Docs, Monitor your agents with signals: https://docs.coreweave.com/products/wandb/weave/guides/tracking/view-agent-signals
- CoreWeave Docs, What is Agent Lens?: https://docs.coreweave.com/products/agent-lens/what-is-agent-lens
- CoreWeave Docs, Set up guardrails: https://docs.coreweave.com/products/wandb/weave/guides/evaluation/guardrails
- CoreWeave, Agent Lens launch (Sep 2026): https://www.coreweave.com/blog/automate-agent-observability-and-improvement-with-coreweave-agent-lens
- CoreWeave Docs, Manage Weave projects: https://docs.coreweave.com/products/wandb/weave/guides/platform/weave-projects
- Control references: ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10); AICPA 2017 Trust Services Criteria with 2022 revised points of focus (TSP Section 100)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
