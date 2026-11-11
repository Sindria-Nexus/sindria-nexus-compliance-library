Last verified: November 11, 2026

# Vercel AI Gateway — Evidence Mapping

## What Vercel AI Gateway is

Vercel AI Gateway is a hosted router for model APIs: one API key or OIDC token reaches models from OpenAI, Anthropic, Google and others through OpenAI-compatible interfaces, with provider failover, spend budgets and request logs built in. Tokens are billed at the provider's list price with no markup. For a readiness engagement, the request log is the audit trail for every model call — but it is metadata evidence only: the gateway retains no prompt or response content by design, and it runs no evaluations, so A.6.2.4 still needs an eval tool.

## Mapping — evidence you already have

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Request logs for every call — each request listed with status, model, provider, usage, cost and duration; the detail view shows every provider attempt and retry | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Logs are metadata only — prompts and responses are not logged. Routing-attempt details are kept 30 days and the log view looks back 36 days; export via Trace Drains for long-term evidence. |
| AI Traces and Trace Drains — an OpenTelemetry trace of every gateway request, forwarded to your own observability tool; the trail in a system you control | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Pro / Enterprise. Needs destination and retention documented. Traces contain request metadata, not prompt or completion content. |
| Overview analytics and Custom Reporting — usage, spend, time to first token and tokens by model, project and API key; request tags and user IDs, queried back through the reporting API | A.6.2.6 Operation and monitoring; A.6.2.8 Recording of event logs | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | In hand | Up to 10 tags per request (each 1–64 characters) and a user ID up to 256 characters. The reporting endpoint is Pro / Enterprise; writes are metered ($0.075 per 1,000 tag/user ID writes). |
| Budgets with spend alerts — caps per team, project, API key or member, email alerts on the way to the cap; requests past the limit are rejected with HTTP 402 (`quota_for_entity_exceeded`) | A.6.2.6 Operation and monitoring; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Soft cap — the check runs at the start of each request, so the request that crosses the limit still completes. BYOK spend is not counted. Needs a provider-side limit. |
| Provider routing and model fallbacks — ordered provider preference, provider filters and fallback models; each response records which model and provider served it | A.6.2.5 Deployment; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC8.1 Change management | Wrapper | Needs an approved model and provider list. |
| Zero data retention routing — prompts and responses deleted after each request by default; ZDR enforcement can restrict routing to providers with zero-retention agreements | A.9.2 Processes for responsible use; A.6.2.6 Operation and monitoring | CC6.1 Logical access; CC7.2 System operations | Wrapper | Needs ZDR scope documented. See the honest flags — the default covers Vercel's own layer, not providers. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups and society, plus the AI risk register behind them. SOC 2: CC3.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.
- **Evaluation** — the gateway runs no evaluations. A.6.2.4 verification and validation still needs an eval tool; the gateway is the router, not the judge.

The point: Vercel AI Gateway gives you the evidence. ISO 42001 makes it certifiable — the policy, risk and accountability wrapper an auditor can test.

## Honest flags

- **The gateway retains no prompt or response content, so its logs are metadata, not content, evidence.** What is recorded: status, model, provider, token usage, cost, duration, authentication method and routing attempts. Content evidence must come from your own application logging.
- **Zero data retention by default covers Vercel's own layer only.** Default routing does not constrain providers' retention or training policies — to restrict routing to providers with zero-retention agreements, set `zeroDataRetention` (or `disallowPromptTraining`) per request. Per-request ZDR costs nothing extra but needs a paid account — Pro, Enterprise, or purchased credits; Hobby teams can use it after purchasing credits. Team-wide ZDR costs $0.10 per 1,000 requests. BYOK keys are skipped under ZDR unless flagged ZDR-compliant. The no-training filter is available to all users at no extra charge, but it is not enforced on BYOK requests — your own provider agreement governs there (it is honoured if the gateway falls back to system credentials).
- **Budgets are a soft cap, and BYOK spend is never counted.** Vercel's own docs: "A budget is a soft cap, not a hard limit. The check runs at the start of each request, so the request that crosses the limit still completes." BYOK spend is metered separately and does not count toward any limit — but an exceeded budget still rejects BYOK requests in its scope with HTTP 402. A failed BYOK request falls back to Vercel system credentials and is billed to your credits. Keep a hard limit on the provider account too.
- **Spend alerts are off by default.** When you add or edit a budget, pick 50%, 75% and/or 100%; each selected threshold fires at most once per period. Budgets themselves are optional — a team, project, key or member without one has unlimited spend.
- **Routing details are kept 30 days** (log view looks back 36 days). Long-term evidence needs Trace Drains export.
- **Trace Drains and Custom Reporting's reporting endpoint are Pro / Enterprise; per-request and team-wide ZDR need a paid account (Pro/Enterprise or purchased credits).** Confirm the tier before promising the control.

## Sources

- Vercel docs — AI Gateway overview: <https://vercel.com/docs/ai-gateway>
- Vercel docs — Budgets and spend limits: <https://vercel.com/docs/ai-gateway/observability-and-spend/budgets>
- Vercel docs — Request logs, Observability, Trace Drains, Custom Reporting: <https://vercel.com/docs/ai-gateway/observability-and-spend>
- Vercel docs — AI Gateway pricing (add-on meters): <https://vercel.com/docs/ai-gateway/pricing>
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
