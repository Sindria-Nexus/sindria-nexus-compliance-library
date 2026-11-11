Last verified: November 11, 2026

# LangSmith — Evidence Mapping

## What the platform is

LangSmith is LangChain's observability and evaluation platform for LLM applications and agents (LangChain / LangGraph and framework-agnostic via OpenTelemetry). The evidence here is the trace record itself — end-to-end tracing of every run — plus the evaluation record: datasets, experiments, human feedback via annotation queues, and versioned prompts in Prompt Hub. Deployment options are managed cloud, bring-your-own-cloud, or self-hosted Enterprise.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **End-to-end tracing of every run.** Every LLM call, tool invocation, and reasoning step, logged with inputs, outputs, and timestamps as a full run tree. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Traces only exist for instrumented runs — confirm tracing is wired into every production path, not just the happy path. |
| **Online evaluators scoring live traces.** Built-in checks for hallucination, toxicity, PII leakage, bias, and prompt injection, plus your own LLM-as-judge evaluators. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs thresholds and escalation documented. Online evaluators score a configurable sample of production traces, not every trace. |
| **Dashboards, alerts, and Insights.** Dashboards track quality, latency, and cost; alerts fire via PagerDuty or webhook; Insights clusters traces into failure modes. | A.6.2.6 Operation and monitoring; A.6.2.8 Recording of event logs | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | In hand | — |
| **Datasets and offline experiments.** Curated examples with reference outputs; each experiment records outputs, scores, and traces per version. | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| **Annotation queues for human feedback.** Production runs routed to subject-matter experts against a rubric; their corrections calibrate your LLM-as-judge evaluators. | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC4.1 Monitoring activities; CC2.3 External communication | Wrapper | Needs named reviewers and a review cadence. |
| **Prompt Hub — versioned prompts.** Every save is an immutable, hash-stamped commit; production pulls a pinned commit or tag. | A.6.2.5 Deployment; A.6.2.7 Technical documentation | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named approver for production. Tags are movable pointers — pin to a commit hash where reproducibility matters (e.g. evaluations), not a moving tag. |

## What LangSmith does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: LangSmith gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Managed-cloud trace retention is 14 days base / 180 days extended — export for long-term evidence.** Base traces are retained for 14 days (short-term debugging); extended traces for 180 days. Neither is an audit-period archive. Export traces you need as evidence, or use self-hosted / BYOC deployment where you control retention.
- **Retention auto-upgrades are opt-in per feature, not automatic.** A trace is upgraded to extended (180-day) retention only where that feature's retention extension is switched on: online evaluators and automation rules can opt out, feedback upgrades only when passed via API/SDK with `extend_trace_retention=true` (UI feedback and notes do not upgrade), and manually adding runs to an annotation queue does **not** upgrade by default. Adding a trace to a dataset does **not** trigger an upgrade (datasets store copies of inputs/outputs with indefinite retention, but the original trace follows its normal tier). When your extended-retention limit is reached, only actions that would create another extended trace are blocked (retention-extending run rules and evaluators) — UI feedback and annotation-queue adds still work — so budget the extended tier for the evaluation activity that actually needs it.
- **Online evaluators sample; they do not watch everything.** Scores are logged with full trace context and alerts fire on threshold breaches, but coverage is a configurable sample. A clean evaluator dashboard is not proof that every production trace was scored.
- **An LLM judge needs calibration.** Human feedback in annotation queues is what calibrates LLM-as-judge evaluators; an uncalibrated judge, and a judge scoring the same model it grades, are both weak evidence. Pin a distinct judge model and record the calibration.
- **Prompt Hub commits are immutable; tags are not.** A commit hash never changes, but a tag (e.g. `production`) is a movable pointer. If production pulls a tag, the prompt can change without a code change — which is the point of the feature, and also the thing to govern.

## Sources

- LangSmith docs — Data retention (Usage and billing): https://docs.langchain.com/langsmith/usage-and-billing
- LangSmith docs — Evaluators (prebuilt templates): https://docs.langchain.com/langsmith/evaluators
- LangChain — "How LangSmith and LangChain OSS Help You Meet EU AI Act Requirements" (online evaluators; annotation queues): https://www.langchain.com/blog/langsmith-langchain-oss-eu-ai-act
- LangChain Support — automatic upgrades to extended retention: https://support.langchain.com/articles/3206725817-why-are-my-traces-being-automatically-upgraded-to-extended-retention?threadId=13aaa13b-73b3-405a-9024-2654a6a212b3
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
