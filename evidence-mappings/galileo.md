Last verified: November 11, 2026

# Galileo — Evidence Mapping

## What Galileo is

Galileo is an evaluation, observability and guardrails platform for LLM apps and agents: every run is traced end to end, Luna-2 evaluation models score production traffic, experiments compare prompt/model/workflow variants, and runtime guardrails enforce the same metrics inline. Galileo documents no ISO 42001 support itself — this mapping is evidence of behaviour, not framework controls. Since 7 August 2026 Galileo is sold as **Splunk Agent Observability** (Cisco completed its acquisition of Galileo on 22 May 2026); existing workspaces and docs.galileo.ai keep working for customers who joined before that date.

## Mapping — evidence you already have

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| End-to-end traces and spans — every LLM call, tool invocation and agent step logged with inputs, outputs, latency, cost, tags and session, in projects and log streams | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Traces come from LangChain/LangGraph, CrewAI, OpenAI Agents SDK, Strands, Vercel AI SDK, or any OpenTelemetry / OpenInference source. Only instrumented apps and supported integrations are traced — document coverage in scope. |
| Luna-2 metrics on production traffic — purpose-built evaluation models score live traces for context adherence, correctness, tool selection, action completion, toxicity, PII, prompt injection and bias | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs thresholds documented. Luna-2 (fine-tuned Llama 3B and 8B) is Enterprise-tier only. |
| Runtime guardrails — Protect / Agent Control — the same metrics run inline to block, redact, route or escalate a run before it reaches users; every verdict is logged | A.9.2 Processes for responsible use; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Needs the policy version behind each rule documented. |
| Datasets and Experiments — curated datasets run through an experiment; each run records outputs, scores and traces per prompt, model or workflow variant | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| Metrics — built-in, LLM-judge, code, Luna-2 — 20+ out-of-the-box evaluators plus custom LLM-as-judge and code metrics in one run, incl. PII, toxicity, injection and bias | A.6.2.4 Verification and validation; A.7.4 Quality of data | CC4.1 Monitoring activities; CC7.2 System operations | In hand | Signals detects failure patterns across production traces and can turn them into custom metrics. |
| Experiment record and CI/CD eval gates — evaluations can run in CI and gate releases on quality thresholds; the tested variant and its scores are on record | A.6.2.5 Deployment; A.6.2.7 Technical documentation | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named approver for production. Wire the gate into your own pipeline and record the thresholds it enforces. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Galileo gives you the evidence. ISO 42001 makes it certifiable — the policy, risk and accountability wrapper an auditor can test.

## Honest flags

- **Protect is deprecated — use Agent Control.** Galileo deprecated Protect in June 2026 in favour of Agent Control, an open-source (Apache 2.0) control plane released in March 2026. Agent Control applies central policies to agents — deny, steer, warn, log or allow — using Luna, NVIDIA NeMo, Amazon Bedrock or custom evaluators. Anyone who built on Protect has a migration ahead; name both in the record so an auditor does not chase a dead product.
- **Galileo is now Splunk Agent Observability** for customers onboarding after 7 August 2026. Galileo's own Free and Pro plans are no longer the onboarding path for new customers — the legacy pricing page still lists them for existing customers, so confirm current pricing and renewal terms with Splunk before relying on old Galileo plan names. Splunk lists the product from $100/month per 1.2 million spans, billed annually, including 500 million Luna tokens and 5 Luna fine-tuning runs a year.
- **Luna-2 metrics and real-time guardrails are Enterprise-tier.** The self-serve tiers get tracing and LLM-judge evals; Luna-2, real-time guardrails and VPC / on-prem deployment sit in the sales-led Enterprise tier.
- **Tracing covers instrumented apps and supported integrations only.** Uninstrumented calls leave no trace, so coverage must be documented in scope.
- **Galileo itself documents no ISO 42001 support.** The mapping below is evidence of behaviour mapped onto Annex A — it is not a vendor control claim.

## Sources

- Galileo documentation — tracing, metrics and Luna-2, datasets and experiments, Protect and Agent Control: <https://docs.galileo.ai>
- Splunk Agent Observability (Galileo product page and pricing, post-7 August 2026): <https://www.splunk.com/en_us/products/agent-observability.html>
- Cisco announcement of Galileo acquisition (announced 9 April 2026, completed 22 May 2026): <https://blogs.cisco.com/news/Cisco-announces-the-intent-to-acquire-galileo>
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
