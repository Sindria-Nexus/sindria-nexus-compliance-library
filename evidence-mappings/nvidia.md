Last verified: November 11, 2026

# NVIDIA — Evidence Mapping

## What the platform is

NVIDIA's AI stack for a self-hosted deployment is three layers: **NeMo** (build and evaluate — Evaluator, Guardrails, Curator, Customizer), **NIM** (serve — containerised inference microservices), and the **Open Agent Safety Platform** (govern agents — OpenShell secure runtime plus Sentry, the out-of-band watchdog). Together they generate evaluation records, guardrail decision records, runtime logs and metrics, and agent-policy enforcement records.

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| NeMo Evaluator jobs — benchmark bundles (`eval-*.json`), aggregate and row-level scores in `results.jsonl`, artifacts per run; `nel compare` regression checks, `nel gate` GO / NO-GO / INCONCLUSIVE release decision against a policy YAML. | A.6.2.4 Verification and validation; A.6.2.7 Technical documentation | CC8.1 Change management; CC4.1 Monitoring activities | Wrapper | Gate thresholds and the policy file are yours to define and retain; without per-problem `results.jsonl` the gate can only report INSUFFICIENT_EVIDENCE. |
| NeMo Guardrails records — Colang input / output / dialog rails; each `GenerationResponse` carries activated rails, actions, and timing, with OpenTelemetry spans per request. | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC5.3 Control activities; CC7.2 System operations | Wrapper | **No policy version or tenant ID stamped by default.** NVIDIA's own FAQ: do not assume a decision automatically includes a reason code, policy version, tenant ID, or replayable event schema — add application metadata and configuration version identifiers to your own audit record. `GenerationResponse` is returned only when generation options are passed; Colang history is LLMRails-only. OpenTelemetry content capture is off by default — prompts and responses are stored in your tracing backend only if you enable it. |
| NeMo Curator & Customizer — quality filtering, exact / fuzzy / semantic dedup, and PII redaction in Curator; fine-tuning jobs on proprietary data in Customizer. | A.7.4 Quality of data; A.7.5 Data provenance | CC8.1 Change management; CC7.1 System operations | Wrapper | Counts once configs are versioned and retained as the provenance record. |
| NIM logging & metrics — structured logs to `stderr`, JSONL logging, Prometheus-compatible metrics, and distributed tracing via OpenTelemetry. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Default log level is version-dependent — verify it for the NIM image you deploy (see footnote).** Set `NIM_LOG_LEVEL` explicitly and `NIM_JSONL_LOGGING=true` for machine-readable logs. Request-detail logging (`NIM_DISABLE_LOG_REQUESTS`) is disabled by default — prompts are not in the logs unless you deliberately enable it, and enabling it exposes prompt, `sampling_params`, and `prompt_token_ids` in container logs. |
| OpenShell sandbox & policy — YAML policy for files, processes, and network, enforced in the kernel (Landlock filesystem confinement, seccomp-staged networking, non-root, no capabilities, deny-by-default egress); credentials only to approved endpoints; Policy Prover (SMT solver) verifies proposed changes first. | A.9.2 Processes for responsible use; A.6.2.5 AI system deployment | CC6.1 Logical access; CC6.6 Boundary protection | In hand | Open-source (Apache 2.0), v0.1.5 as of October 20, 2026 — still 0.1.x. Enforcement is deepest on Linux; Windows support is experimental. The prover covers the policy features its model represents (filesystem, process, L4 network, REST) — GraphQL, MCP, WebSocket, and JSON-RPC rules return `unsupported`. |
| Sentry on BlueField-4 — DOCA Tower (Envoy-based transparent proxy, TLS termination in silicon) checks agent traffic against OPA policy, DOCA Argus introspects runtime out of band (live host-memory introspection, no host-resident agent), decisions written as attested, tamper-evident telemetry; quarantine in milliseconds. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC7.4 Recovery and response | Wrapper | **Reference design — not a shipped product.** Sentry is part of the Open Agent Safety Platform announced September 28, 2026 and the OpenShell Reference Architecture announced October 21, 2026; NVIDIA plans Sentry availability for **early 2027**. Route its telemetry to your SIEM; retain per policy. Quarantine-in-milliseconds and sub-millisecond policy evaluation are vendor claims, not independently benchmarked. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: NVIDIA gives you the guardrails, the evals, and a witness outside the agent. ISO 42001 makes it certifiable.

## Honest flags and footnotes

- **Evaluator output is JSON, not YAML.** In the current `nel`-based SDK, runs write an `eval-*.json` bundle plus per-problem `results.jsonl` (and `trajectories.jsonl`, `runtime_stats.json`, `failure_analysis.json`). Retain the bundle and the JSONL, not a YAML summary. (Older launcher documentation shows a `results.yml` file; that is not the current SDK output.)
- **NIM's default log level differs by NIM line and version — NVIDIA's own docs disagree, and both statements are current.** The Logging and Observability reference for NIM for LLM and VLM (latest) and for NIM for LLMs 2.0 lists `NIM_LOG_LEVEL` default `WARNING`; the Configuration reference for NIM for LLMs 1.x lists default `DEFAULT`, which sets all loggers to `INFO` (except TRT-LLM, set to `ERROR`); the 2.0 Environment Variables reference lists default `None` (application default). At `WARNING` a correctly served completion generates no log line; at `DEFAULT`/`INFO` it does. Set the level explicitly for the image you deploy and record which value you use — do not assume either default. Nothing in the documented telemetry records caller identity, role, or an authorization decision — correlation headers identify the request, not the caller.
- **Guardrails do not stamp your audit fields.** Reason code, policy version, and tenant ID must be added by your application; version the library dependency, guardrails configuration, prompts, and custom actions together. There is no library-wide fail-closed policy — error behaviour depends on the rail, engine, and integration, so test timeouts and provider failures.
- **Sentry is a reference design with planned availability.** Do not present it as a deployed control until it ships (planned early 2027) and is running on BlueField-4 in your environment. OpenShell itself is available open-source now.
- **Self-hosted means self-retained.** NVIDIA supplies no log retention, SIEM, or alerting — log shipping, retention, and review cadence are yours.

## Sources

- NVIDIA Documentation — NeMo Evaluator, Implementing Quality Gates: https://docs.nvidia.com/nemo/evaluator/nightly/tutorials/quality-gate
- NVIDIA Documentation — NeMo Evaluator Quickstart: https://docs.nvidia.com/nemo/evaluator/nightly/get-started/quickstart
- NVIDIA Documentation — NeMo Guardrails, AI Runtime Security FAQ: https://docs.nvidia.com/nemo/guardrails/resources/runtime-security-faq
- NVIDIA Documentation — NeMo Framework, Data Curation (Curator): https://docs.nvidia.com/nemo-framework/user-guide/25.07/datacuration/index.html
- NVIDIA Documentation — NIM Logging and Observability (LLM and VLM, latest): https://docs.nvidia.com/nim/large-language-models/latest/reference/logging-and-observability.html
- NVIDIA Documentation — NIM Logging and Observability (LLMs 2.0): https://docs.nvidia.com/nim/large-language-models/2.0.0/reference/logging-and-observability.html
- NVIDIA Documentation — Configure Your NIM (LLMs 1.10, Configuration reference): https://docs.nvidia.com/nim/large-language-models/1.10.0/configuration.html
- NVIDIA OpenShell — Release v0.1.5: https://github.com/NVIDIA/OpenShell/releases/tag/v0.1.5
- NVIDIA Newsroom — Open Agent Safety Platform (Sept 28, 2026): https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Launches-Open-Agent-Safety-Platform-to-Secure-Agents-From-Testing-to-Deployment/default.aspx
- NVIDIA Developer Blog — Inside NVIDIA Sentry: https://developer.nvidia.com/blog/inside-nvidia-sentry-secure-ai-agents-at-runtime

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
