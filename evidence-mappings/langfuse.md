Last verified: November 11, 2026

# Langfuse — Evidence Mapping

## What the platform is

**Langfuse** is an open-source LLM engineering platform (MIT-licensed core, self-hostable) for tracing, evaluation, datasets, and prompt management — cloud or self-hosted. ClickHouse, Inc. acquired Langfuse in January 2026; the company states it stays open source with no planned licensing changes. Core tracing, evaluations, datasets, prompt management, and the playground are in the free MIT core with no limits; nine governance features are gated behind a paid Enterprise licence key when self-hosting (see flags).

## Mapping — platform artifact → ISO 42001 Annex A / SOC 2 CC

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| End-to-end tracing — traces, observations, sessions — every LLM and non-LLM call as nested observations, with inputs, outputs, model, tokens, cost, and latency; sessions group multi-turn work. OpenTelemetry-based | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Coverage: instrumented code and supported integrations only. |
| Scores and LLM-as-judge on live traces — managed judges run on production traces, step-wise if needed; scores also arrive via SDK, API, and user feedback | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs thresholds and escalation documented. |
| Annotation queues for human review — production traces routed to reviewers against a rubric; corrections baseline the automated evaluators and become new dataset items | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs named reviewers and a review cadence. |
| Versioned datasets and experiments — datasets version automatically on every change (timestamped, item diffs); experiments pin the dataset version they ran and compare runs on scores, cost, and latency | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| Evaluators — LLM-as-judge, custom, and human — managed judges, code-based evaluators, and human scores in one record, in development and production | A.6.2.4 Verification and validation; A.7.4 Quality of data | CC4.1 Monitoring activities; CC7.2 System operations | In hand | — |
| Prompt management — versions pinned by label — prompts versioned centrally, deployed by label (production, staging) with no code change; every generation links to the prompt version behind it | A.6.2.5 Deployment; A.6.2.7 Technical documentation | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named approver for the production label. |

## The gap band — what Langfuse does not give you

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Langfuse gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Audit logs, project RBAC, retention policies, and server-side masking are Enterprise-licensed on self-host.** The nine Enterprise-gated features are: project-level RBAC, protected prompt labels, data retention policies, audit logs, server-side data masking, SCIM, organisation creators, UI customisation, and the admin/instance management APIs. Cloud access varies by plan — set retention and export explicitly. Cloud data history is reported as 30 days (Hobby), 90 days (Core), 3 years (Pro) — confirm on the pricing page before relying on it.
- **Protected prompt labels are also gated.** As of September 2026, protected labels (restricting who can move `production`) are available on the Pro plan with the Teams add-on, on Enterprise, and in the self-hosted Enterprise Edition — not in the free core. A "named approver for production" wrapper is only enforceable in the product where protected labels exist.
- **Without the Enterprise key, governance falls back to you.** Masking and retention fall back to your applications and operating procedures; audit evidence falls back to reverse-proxy or application logs, which show requests but not who changed prompts or settings.
- **Langfuse is not a gateway.** Requests never pass through Langfuse on the way to a provider, so it cannot route, fall back, or enforce anything at request time — it observes and records.
- **Prompt versions are immutable; labels are the deployment mechanism.** Every save creates a new immutable version; a label points to exactly one version, and fetching by label (e.g. `production`) needs no code change. SDK cache TTL is 60 seconds by default, so a label move propagates within about a minute.

## Sources

- Langfuse Docs, Prompt caching (60-second default TTL): https://langfuse.com/docs/prompt-management/features/caching
- Langfuse, Self-Hosted Pricing (OSS vs Enterprise): https://langfuse.com/pricing-self-host
- Langfuse, Protected prompt labels (changelog, Apr 2025): http://langfuse.com/changelog/2025-04-02-protected-prompt-labels
- Langfuse, Prompt CI/CD: version, gate, and roll out prompts like code: https://langfuse.com/resources/engineering/prompt-cicd
- Langfuse, How to organize, version, and test hundreds of prompts: https://langfuse.com/resources/engineering/prompt-management-at-scale
- Control references: ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10); AICPA 2017 Trust Services Criteria with 2022 revised points of focus (TSP Section 100)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
