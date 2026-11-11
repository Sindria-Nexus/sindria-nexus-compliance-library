Last verified: November 11, 2026

# Cloudflare AI Gateway — Evidence Mapping

## What the platform is

**Cloudflare AI Gateway** is a managed edge proxy you put in front of LLM calls (20+ providers, plus Workers AI): change the base URL and get per-request logging, analytics, exact-match response caching, rate and spend limits, retries/fallbacks, and Guardrails/DLP in the request path. Core gateway features (analytics, caching, rate limiting) are free on all plans; Guardrails are billed as Workers AI inference and Logpush follows Logpush pricing. Provider keys can be brought-your-own (BYOK), held encrypted in Cloudflare's Secrets Store.

## Mapping — platform artifact → ISO 42001 Annex A / SOC 2 CC

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Per-request request / response logs — prompt, response, provider, model, status, tokens, cost, and duration for every call through the gateway; export via Logpush | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Retention is days, not an audit period — export via Logpush. Logs are on by default per gateway. |
| Analytics & custom metadata — requests, tokens, cost, and errors across providers; requests tagged by user / team, plus verified user ID behind Cloudflare Access | A.6.2.6 Operation and monitoring; A.4.5 System resources | CC4.1 Monitoring activities; CC7.2 System operations | In hand | — |
| Gateway authentication, BYOK & account audit logs — token-gated gateways, provider keys held encrypted, and an account record of gateway changes | A.4.5 System resources; A.6.2.8 Recording of event logs | CC6.1 Logical access; CC6.6 System boundaries | In hand | — |
| Exact-match response caching — identical requests served from cache under a set TTL (60 seconds to 1 month), with HIT / MISS recorded per response | A.6.2.6 Operation and monitoring; A.7.5 Data provenance | CC7.2 System operations; CC7.1 System configuration | Wrapper | Off by default; a cached reply never reaches the provider — document TTL policy. |
| Rate limits & spend limits — request caps per gateway (fixed or sliding window, 429 on breach) and dollar budgets by model, provider, or metadata that block when exceeded | A.4.5 System resources; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Rate limits are gateway-scoped only — no per-user or per-key rate limits. (Spend limits can be scoped by metadata dimensions such as user, team, or application.) |
| Guardrails & DLP decisions — Llama Guard 3 8B screens prompts and responses, flag-or-block by category; DLP scans for PII and financial data; actions recorded in the log | A.9.2 Responsible use; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC6.6 System boundaries | Wrapper | Flag or block only — no masking; full DLP profiles need Zero Trust. |

## The gap band — what Cloudflare does not give you

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Cloudflare gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Log retention is days, not an audit period — export via Logpush.** Accounts whose first gateway was created on or after 24 September 2026 keep logs in Workers Logs (new customers' logs kept 3 or 7 days) under Workers Logs pricing; older accounts keep legacy limits (100,000 logs total on Workers Free, 10,000,000 per gateway on Workers Paid) until deleted. Logpush export needs Workers Paid (4 jobs per account).
- **Caching is off by default.** Exact-match only (cache key is a hash of provider, endpoint, model, auth header, and full request body); TTL minimum 60 seconds, maximum 1 month; cacheable requests up to 25 MB; streaming responses are not cached by default. A cache hit never reaches the provider — document the TTL policy and the staleness risk.
- **Rate limits are gateway-scoped only.** The gateway's own limit is set by its owner (fixed or sliding window, 429 on breach); there is no native per-user or per-key rate limit. Spend limits are the finer control: up to 20 rules per gateway, each a dollar budget over a fixed or sliding window, scoped by model, provider, or metadata key.
- **Guardrails are flag-or-block, with limits.** Evaluated by `@cf/meta/llama-guard-3-8b` on Workers AI, billed as Workers AI inference; about ~500 ms added per evaluated request; Guardrails do not support streaming requests. Direct prompt injection is detected via category P1 (prompt-guard model); detection of injected instructions in tool outputs or retrieved documents is not described.
- **DLP is flag-or-block, no masking.** DLP scanning is free; accounts without a Zero Trust subscription get two predefined profiles (Financial Information; Social / Insurance / National Identifier Numbers). The full set — all predefined profiles, custom profiles, integration profiles, DLP datasets, OCR — requires a Zero Trust subscription that includes DLP.
- **Zero Data Retention does not switch off gateway logs.** ZDR routing applies to Unified Billing traffic on marked models; it does not apply to BYOK and does not switch off AI Gateway's own logs.
- **Third-party models sit outside Cloudflare's DPA.** Per Cloudflare's service-specific terms, the DPA and Information Security Exhibit do not apply to third-party models reached through AI Gateway — confirm the contractual position for each provider.

## Sources

- Cloudflare AI Gateway docs, Features: https://developers.cloudflare.com/ai-gateway/features/
- Cloudflare AI Gateway docs, Pricing (DLP, Guardrails): https://developers.cloudflare.com/ai-gateway/reference/pricing/
- Cloudflare AI Gateway documentation — logging, caching, rate limiting, Guardrails, DLP, log retention / Logpush (developers.cloudflare.com/ai-gateway)
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 CC criteria

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
