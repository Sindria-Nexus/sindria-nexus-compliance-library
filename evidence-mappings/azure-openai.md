Last verified: November 11, 2026

# Azure OpenAI — Evidence Mapping

## What the platform is

Azure OpenAI (in Microsoft Foundry) is Microsoft's managed service for running OpenAI models on Azure, with built-in content safety filtering and a Foundry evaluation framework. A deployment already generates three auditable artifacts: diagnostic logs, content safety filter decisions, and evaluation runs.

> **Naming note (verified November 11, 2026):** Microsoft renamed Azure AI Foundry to **Microsoft Foundry**, effective January 1, 2026 (announced at Ignite, November 18, 2025). Documentation now lives under `learn.microsoft.com/azure/foundry/` for the new Foundry portal and `learn.microsoft.com/azure/foundry-classic/` for the Foundry (classic) portal; both names appear in current docs. The diagnostic log categories and evaluation features below are the same under either portal.

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Audit logs — control-plane / administrative operations recorded via diagnostic settings: deployments and configuration changes, with caller identity and time. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Off by default — must be routed to Log Analytics or Storage.** Audit logs are administrative operations only; they do not record model calls or prompt content. The monitoring reference lists four diagnostic log categories for the service: `Audit`, `RequestResponse`, `AzureOpenAIRequestUsage`, and `Trace`. |
| RequestResponse logs — every inference call logged: operation, deployment, status, duration, caller IP (first three octets) and Entra ID object identity. | A.6.2.8 Recording of event logs; A.7.5 Data provenance | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Metadata, not prompt bodies.** RequestResponse logs are not a prompt/response record — do not rely on them for content. Full capture needs APIM or app-level logging. Token/usage counts are **not** in RequestResponse logs — they come from the separate `AzureOpenAIRequestUsage` log category and platform metrics. |
| Built-in content filters — hate, sexual, violence, and self-harm, each at four severity levels (safe, low, medium, high — returned as 0 / 2 / 4 / 6 in the Content Safety annotation), blocked at the configured threshold, on prompt and completion; result returns in `content_filter_result`. Default threshold is medium for all four categories. | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC5.3 Control activities; CC7.2 System operations | In hand | Default safety settings apply to all models except audio API models such as Whisper. The default blocks medium and high; low-severity content passes unless you tighten the threshold. |
| Custom RAI policy, Prompt Shields & blocklists — per-deployment thresholds, jailbreak and indirect-attack detection, protected-material detection, custom blocked terms. | A.9.2 Processes for responsible use; A.7.2 Data for development | CC5.3 Control activities; CC6.1 Logical access | Wrapper | Only where assigned; Shields must be enabled and documented. A custom filter that is created but never assigned to a deployment has no effect — the deployment keeps the default filter. **Prompt Shields defaults differ by attack type: user-prompt attack detection is on by default; document-attack detection is off by default and must be enabled; Spotlighting (preview) is off by default.** Thresholds can be adjusted self-serve; turning filters partially or fully off needs Microsoft approval, and full content-filtering control is limited to managed customers. |
| Quality evaluators — groundedness, relevance, coherence, and fluency over your test datasets, in the Foundry portal or Evaluation SDK. | A.6.2.4 Verification and validation; A.6.2.3 AI system design and development | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs your datasets, pass thresholds, and a release gate. Groundedness returns a 1–5 score; the other evaluators are individual built-in evaluators. The combined Quality Grader evaluator is deprecated and can no longer be run — use the individual evaluators. |
| Safety evaluators & adversarial simulation — safety evaluators plus simulated attack queries testing whether harmful content gets through; the AI Red Teaming Agent (preview, built on PyRIT) automates adversarial probing. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.2 Evaluation of deficiencies; CC7.2 System operations | Wrapper | Counts once runs are scheduled and failures tracked. Red-teaming features are in preview without an SLA. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Microsoft gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags and footnotes

- **Diagnostic logging is off by default.** No diagnostic setting means no Audit, RequestResponse, Trace, or usage logs at all — and nothing is backfilled when you turn it on.
- **The built-in logs are not a prompt/response record.** RequestResponse rows carry operation, status, latency, truncated IP, and identity — not what was asked or answered. Foundry tracing into Application Insights can capture content, but content recording is a separate setting — check whether it is enabled in your deployment rather than assuming prompt/response capture is on.
- **Token counts live in a different log category.** If your evidence needs token/usage accounting, enable `AzureOpenAIRequestUsage` (and platform metrics); do not expect it in RequestResponse.
- **Content-filter severity is safe / low / medium / high** (0 / 2 / 4 / 6 in the API annotation). The default blocks medium and high; low-severity content passes unless you tighten the threshold.
- **Microsoft retains prompts and completions for up to 30 days** for abuse monitoring under its own data-handling commitments; that is Microsoft's retention, not your audit trail. Eligible customers can apply for modified abuse monitoring (which removes storage and human review) or zero data retention.
- **Log Analytics retention defaults to 30 days** unless you configure it — set analytics and long-term retention per table to match your evidence-retention commitment (up to 12 years is supported).

## Sources

- Microsoft Learn — Monitoring data reference for Azure OpenAI (classic): https://learn.microsoft.com/en-us/azure/foundry-classic/openai/monitor-openai-reference
- Microsoft Learn — Configure content filters: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/content-filters
- Microsoft Learn — Prompt Shields in Microsoft Foundry: https://learn.microsoft.com/en-us/azure/foundry/openai/concepts/content-filter-prompt-shields
- Microsoft Learn — Built-in evaluators reference: https://learn.microsoft.com/en-us/azure/foundry/concepts/built-in-evaluators
- Microsoft Learn — Data, privacy, and security for Azure OpenAI Service: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?tabs=azure-portal
- Microsoft Learn — Transparency Note and use cases for AI Content Safety: https://learn.microsoft.com/en-us/azure/foundry/responsible-ai/content-safety/transparency-note?view=foundry-classic
- Microsoft Learn — Run evaluations from the Microsoft Foundry portal: https://learn.microsoft.com/en-us/azure/ai-studio/how-to/evaluate-generative-ai-app

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
