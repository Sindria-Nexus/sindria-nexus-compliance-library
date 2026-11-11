Last verified: November 11, 2026

# Helicone — Evidence Mapping

## What the platform is

**Helicone** is an open-source (Apache-2.0) LLM observability platform with an AI gateway: point an existing model client at Helicone's base URL and every proxied request is logged with prompt, response, model, tokens, cost, and latency, with edge caching, rate limits, evals, datasets, and security checks on top. Async logging (via OpenLLMetry/OpenTelemetry) covers calls that do not go through the gateway.

> **Status warning — read first.** Mintlify acquired Helicone on 3 March 2026 and the hosted product is now in **maintenance mode**: security fixes and new-model support continue, but feature development has stopped (changelog last entry 26 November 2025) and **new signups are disabled**. The Apache-2.0 self-hosted version remains open to everyone. Treat Helicone as an existing-user / self-host option, not a new-vendor recommendation, until Mintlify says otherwise.

## Mapping — platform artifact → ISO 42001 Annex A / SOC 2 CC

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Full request & response logs — every proxied call logged with prompt, response, model, tokens, cost, latency, and status, searchable in one record | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Retention is plan-gated (see flags) — export for long-term evidence. |
| Sessions, users & custom properties — calls tagged by user, session, and custom property, queryable with HQL, so a log traces to a customer, feature, or release | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Needs tagging applied consistently in scope. |
| Edge caching record — cache enabled per request with TTL (7 days default, up to 365), bucket and seed controls; responses stamp HIT / MISS | A.6.2.5 Deployment; A.6.2.6 Operation and monitoring | CC8.1 Change management; CC7.2 System operations | Wrapper | Needs TTL, seed, and stale-response policy documented. |
| Scores & online evaluators — numeric scores and thumbs feedback per request or session, plus LLM-as-judge evaluators scoring live traffic | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs thresholds and escalation documented. |
| Datasets built from production logs — logged requests curated into datasets for evaluation and replay before a prompt or model change ships | A.7.2 Data for development and enhancement; A.7.4 Quality of data; A.6.2.4 Verification and validation | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| LLM Security & Moderations — header-enabled threat detection for prompt injection, anomalies, and exfiltration, plus OpenAI moderation pre-checks on user messages | A.6.2.6 Operation and monitoring; A.9.2 Processes for responsible use | CC6.6 Boundary protection; CC7.2 System operations | Wrapper | Needs block-vs-flag choices documented per surface. |

## The gap band — what Helicone does not give you

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Helicone gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Prompt and response bodies are logged by default.** Use omit-log headers and redaction where data is sensitive. `Helicone-Omit-Request` / `Helicone-Omit-Response` stop *storage*, but Helicone's own docs note the content is still sent to its backend. Keeping payloads out entirely requires async logging with content tracing off (which takes the gateway out of the request path) or fully disabling logging in async mode.
- **Retention is plan-gated: 7 days free, 1 month on Pro ($79/mo), 3 months on Team ($799/mo), configurable on Enterprise.** Free tier is 10,000 requests/month, 1 seat, 1 GB storage. Export for long-term evidence.
- **Hosted product in maintenance mode since March 2026; new signups disabled.** Feature development has stopped; only security fixes and new-model support continue. Mintlify has said it will help customers migrate to another platform. The standalone Rust ai-gateway repo has been idle since 21 November 2025 (relicensed Apache-2.0 → GPL-3.0 on its final commit).
- **LLM Security is header-enabled (`Helicone-LLM-Security-Enabled`) and built on Meta security models (Prompt Guard / Llama Guard).** Third-party comparisons report it currently works with OpenAI models only — verify per-provider coverage before relying on it for non-OpenAI traffic.
- **Caching is exact-match, edge-stored (Cloudflare Workers KV), not on your infrastructure.** Default TTL 7 days (`max-age=604800`), maximum 365 days; bucket max 20 outside Enterprise. In async-logging mode, caching, custom rate limiting, and retries are not available.
- **Tracing is request-level, not span-based.** There is no nested trace tree of tool calls and agent steps as in Weave/Langfuse — scope the A.6.2.8 claim to per-request records.

## Sources

- Helicone docs, LLM Caching: https://docs.helicone.ai/features/advanced-usage/caching
- Helicone docs, Omit Logs: https://docs.helicone.ai/features/advanced-usage/omit-logs
- Helicone docs, Stringent compliance requirements: https://docs.helicone.ai/faq/compliance
- Helicone docs — request logging, scores, LLM security, moderations (docs.helicone.ai)
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 CC criteria

## Disclaimer

This is readiness guidance, not a certification guarantee. A vendor's own certification covers the vendor, not the prospect's deployment. Applicability is set in your Statement of Applicability and tested by your auditor.
