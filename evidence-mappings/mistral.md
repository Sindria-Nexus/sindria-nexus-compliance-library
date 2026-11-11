Last verified: November 11, 2026

# Mistral — Evidence Mapping

## What the platform is

Mistral AI's **Studio (La Plateforme)** is the console for building on Mistral models: managed agents, workflows, apps, observability (tracing and evaluations), and governance (workspaces, roles, audit logs, guardrails, zero data retention). **Vibe** (formerly Le Chat) is the chat/work surface covered by the same audit logs. The November 5, 2026 Studio release added managed agents, a workflow builder, hosted apps, and offline/online evaluations — almost all of it in Public Preview, so APIs, behaviour, and limits may still change.

## Mapping — platform artifact → ISO 42001 Annex A / SOC 2 CC

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Audit logs across Studio and Vibe — who did what, and when: sign-ins, API key creation and deletion, and actions on resources by a user, key, or the system. Retrieved via the Admin API | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Enterprise-tier only; enabled by default for all workspaces. |
| Workspaces, roles, and service accounts — org and workspace roles via groups, SAML SSO, scoped API keys with expiry, Secrets Manager, and workloads running under service accounts named in the logs | A.3.2 AI roles and responsibilities; A.6.2.6 Operation and monitoring | CC6.1 Logical access; CC6.6 Access controls | Wrapper | Needs your access review documented. |
| Moderation, guardrails, and zero data retention — guardrails check what goes in and out of a model; the moderation API returns raw scores per category; ZDR stops storage of supported stateless inputs/outputs | A.9.2 Processes for responsible use; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Needs rules, thresholds, and ZDR scope documented. |
| Distributed tracing over OpenTelemetry — model calls, tool calls, agent activity, and workflow runs in one trace view; spans redacted on the client before export | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Enterprise-tier only; traces kept 30 days — export for long-term evidence. |
| Offline evaluations and datasets — Evaluation SDK (`mistralai-evaluations`) runs a dataset, task, and scorers (rule-based or LLM-as-judge) with pass/fail goals; results and per-record scores land in Studio | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | Enterprise-tier only; in Public Preview. |
| Online evaluations on production traces — LLM judges score live traces after ingestion; production cases feed back into datasets, so versions compare on real cases before release | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs thresholds and escalation documented. Public Preview; Enterprise-tier only. |

## The gap band — what Mistral does not give you

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Mistral gives you the evidence. ISO 42001 makes it certifiable — the wrapper an auditor can test.

## Honest flags

- **Audit logs, traces, datasets, and evals are Enterprise-tier only.** Audit logs are available on Enterprise plans and enabled by default for all workspaces; reading traces in Studio requires an Enterprise organisation and an observability role. The Admin API (which retrieves audit logs) is Enterprise.
- **Traces are kept 30 days.** Export them for any evidence that must survive an audit period. Traces are redacted on the client before export, by default.
- **Offline evaluations are in Public Preview** (Evaluation SDK, `mistralai-evaluations`) and Enterprise-only, like the rest of Observability. Preview means the API, behaviour, and limits may change and an update may require code changes.
- **Zero data retention is narrow.** ZDR is available on paid plans for supported stateless API calls only (e.g. chat completions, embeddings, moderation, OCR), must be requested and is approved at Mistral's discretion. It does **not** cover stateful products — agents, conversations, libraries, files, batch processing, or Vibe. ZDR is separate from opting out of model training. Default API retention is 30 rolling days for abuse monitoring.
- **Audit logs are reviewed in the console;** programmatic retrieval is via the Enterprise Admin API — confirm export format and retention on your plan before promising an auditor a feed.

## Sources

- Mistral Docs, Governance: https://docs.mistral.ai/studio/governance
- Mistral Docs, Observability: https://docs.mistral.ai/studio/observability
- Mistral Docs, Offline evaluations: https://docs.mistral.ai/studio/observability/evaluations
- Mistral Docs, Zero data retention: https://docs.mistral.ai/admin/monitor-comply/zero-data-retention
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 CC criteria

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
