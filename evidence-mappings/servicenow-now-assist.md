Last verified: November 11, 2026

# ServiceNow Now Assist — Evidence Mapping

## What the platform is

ServiceNow Now Assist is the AI layer on the Now Platform — skills and agents that act inside ServiceNow workflows — governed by **AI Control Tower**, the platform's AI governance layer. A deployment already generates two records: the Generative AI execution log and the Control Tower inventory and lifecycle record.

> **Naming note (verified November 11, 2026):** Now Assist Guardian is now **AI Guardian**; the unified AI experience (Now Assist, Moveworks, AI Experience) is now branded **ServiceNow Otto**. Entitlements did not change with the renaming. The current release is **Australia** (GA May 5, 2026), following Zurich (March 2026).

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Generative AI log (`sys_generative_ai_log`) — prompt, response, and edited response per skill call, with model and source task. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Corrected November 11, 2026: this table is MAINT-only.** It holds full prompt/response text including sensitive case data, and even administrators cannot access it — ServiceNow Support staff only, by design, and ACL changes do not open it. The customer-usable records are `sys_gen_ai_usage_log` (who ran which skill, how often, token counts — no prompt content) and the Generative AI Metrics table (`sys_generative_ai_metric`). Do not promise an auditor direct access to `sys_generative_ai_log`. |
| Agent execution plans (`sn_aia_execution_plan`) — every step and tool call, with inputs and outcome; alongside `sn_aia_agent` (the agent) and `sn_aia_usecase` (the use case). | A.6.2.8 Recording of event logs; A.6.2.7 Technical documentation | CC7.2 System operations; CC4.1 Monitoring activities | In hand | — |
| AI Guardian + Data Privacy — offensiveness, prompt-injection, and sensitive-topic checks; PII de-identified in prompts before they reach the LLM and restored in the response. | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC5.3 Control activities; CC7.2 System operations | Wrapper | Needs log-vs-block documented. Prompt-injection detection is on by default (block and log, medium threshold) for AI skills — **except** ServiceNow Otto for Platform skills and custom skills, which admins must configure manually. Offensiveness defaults to log-only unless you choose block. |
| AI inventory: model, asset & CI — every system, model, dataset, and MCP server, with owner and risk tier. | A.6.2.7 Technical documentation; A.10.3 Suppliers | CC7.2 System operations; CC6.6 System boundaries | Wrapper | Needs a coverage check for unconnected AI. Discovery spans 30+ enterprise connectors, but anything without a connector must be registered by hand — shadow AI is only inventoried if you put it there. |
| Lifecycle gates, intake to retire — Assess, Build and Test, and Deploy require evidence and approval pre-production. | A.6.2.2 Requirements and specification; A.6.2.5 Deployment | CC5.3 Control activities; CC8.1 Change management | Wrapper | Needs named approvers per gate. |
| Observe & Measure + Analytics — runtime metrics, skill feedback, value and ROI per asset; five Control Tower dimensions: Discover, Observe, Govern, Secure, Measure. | A.6.2.6 Operation and monitoring; A.6.2.4 Verification and validation | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs thresholds and a response process. The Secure dimension includes a real-time kill switch; runtime observability is deepened by the Traceloop acquisition. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: ServiceNow gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags and footnotes

- **The full prompt/response log is not yours to read.** `sys_generative_ai_log` is restricted to ServiceNow Support (MAINT role) even from admins. Build your audit trail on the execution plans, the usage log, and the Generative AI Metrics table — and say so plainly to the auditor.
- **Guardrail defaults differ by skill type.** Prompt injection is block-and-log by default for standard AI skills, but custom skills and Otto for Platform skills need manual configuration; offensiveness is log-only unless you switch it to block. Document the setting per skill.
- **Control Tower coverage is connector-dependent.** ServiceNow's own AI gets the full treatment; external AI is seen as well as its connector allows. AI Gateway enforcement for MCP traffic is not on by default.
- **Tier matters.** Custom AI skill and agent creation requires the Prime tier (legacy Pro Plus / Enterprise Plus remained valid until renewal and reached end of sale July 1, 2026). AI Control Tower is bundled in every AI Native tier (Foundation, Advanced, Prime).
- **Consumption is counted in assists**, not tokens — one assist per skill or agentic workflow execution (per tool action in the current model). Trace an assist charge back to its business record by joining `sys_generative_ai_log`'s case reference with `sys_gen_ai_usage_log`.

## Sources

- ServiceNow Community — AI Guardian FAQ: https://www.servicenow.com/community/servicenow-otto-articles/ai-guardian-faq/ta-p/3601580
- ServiceNow Community — Now Assist skill kit feature (Generative AI log tables): https://www.servicenow.com/community/now-assist-forum/now-assist-skill-kit-feature/m-p/3465095
- ServiceNow Community — ServiceNow AI Agents: Build, Operations & Governance Guide (Australia release): https://www.servicenow.com:443/community/s/cgfwn76974/attachments/cgfwn76974/now-assist-articles/930/4/ServiceNow_AI_Agents_Build_Operations_Governance_Guide_v3.2.pdf
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 CC criteria

## Disclaimer

This is readiness guidance, not a certification guarantee. Applicability is set in your Statement of Applicability and tested by your auditor. ServiceNow's own certifications cover ServiceNow's platform — not your instance, your skill configurations, your guardrail settings, or your agents.
