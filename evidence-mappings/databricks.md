Last verified: November 11, 2026

# Databricks (Mosaic AI) — Evidence Mapping

## What the platform is

Databricks Mosaic AI is Databricks' suite for building, evaluating, deploying, and monitoring AI agents on the Databricks lakehouse. The evidence here comes from two places: **Mosaic AI Agent Evaluation** (LLM judges plus human feedback, with MLflow Tracing) and **Unity Catalog** — including the **Unity Gateway** (the current name for the AI Gateway) and its audit logs and inference tables. Unity Catalog provides the single permission model, lineage, and audit trail across data, models, and tools.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **Agent Evaluation with LLM judges.** Built-in and custom judges score correctness, grounding, and safety against your evaluation dataset. | A.6.2.4 Verification and validation; A.7.4 Quality of data; A.7.2 Data for development | CC4.1 Monitoring activities; CC7.2 System operations | In hand | — |
| **Human feedback in the Review App.** Stakeholders and subject-matter experts label responses and flag quality issues. | A.9.2 Processes for responsible use; A.8.2 Tools for reporting; A.6.2.4 Verification and validation | CC4.1 Monitoring activities; CC2.3 External communication | Wrapper | Needs a documented review cadence and named reviewers. |
| **MLflow Tracing on every step.** Inputs, outputs, and metadata for each retrieval, tool call, and model step, in development and production. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring; A.6.2.7 Technical documentation | CC7.2 System operations; CC4.1 Monitoring activities | In hand | — |
| **Unity Catalog audit logs in system tables.** Which principal accessed what, from which agent, and when (`system.access.audit`; `run_by` / `run_as` in `identity_metadata` distinguishes a human caller from an agent acting on their behalf). | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | — |
| **Inference tables: full payload logging.** The exact prompt sent, response returned, token counts, and latency for every model call via the gateway. | A.6.2.6 Operation and monitoring; A.7.5 Data provenance; A.6.2.8 Recording of event logs | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Needs your retention period and review process documented — and inference tables must be enabled per model service (see flags). |
| **Governed access and lineage in Unity Catalog.** One permission model for data, models, and tools; on-behalf-of-user auth; lineage to source tables. | A.4.5 System resources; A.7.5 Data provenance; A.10.3 Suppliers | CC6.1 Logical access; CC6.6 System boundaries | In hand | — |

## What Databricks does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Databricks gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **"AI Gateway" is now Unity Gateway.** Databricks' current, generally available control plane is Unity Gateway. The legacy AI Gateway inference-table experience is being retired: legacy inference tables cannot be enabled on new or existing model-serving endpoints from 20 February 2026 and are no longer supported from 20 March 2026. Use Unity Gateway inference tables, not the legacy path.
- **Inference tables are not automatic.** They must be enabled per model service/endpoint, require Unity Catalog and the right privileges (`MANAGE` on the service, `CREATE TABLE` in the target schema), and are a billed Unity Gateway feature. Rows can take up to about an hour to appear, and payloads larger than 10 MiB are not logged on Unity Gateway inference tables.
- **Payload logging for MCP is gated beta.** Unity Gateway's newer payload logging for MCP interactions was announced as a gated beta (May 2026) — enrolment via your Databricks account team. Do not assume it is on.
- **MLflow Tracing records what you instrument.** Tracing captures the steps your agent code runs through the traced SDKs; uninstrumented paths leave no trace. Confirm coverage in your own deployment.
- **Judge scores are not human sign-off.** LLM-judge scores need calibration against human labels and a documented review cadence; an uncalibrated judge is evidence of a process, not of quality.

## Sources

- Databricks — "Governing AI agents at scale with Unity Catalog": https://www.databricks.com/blog/governing-ai-agents-scale-unity-catalog
- Databricks — "What's new in Unity Gateway: service policies, guardrails, observability, and cost controls for AI agents and MCPs": https://www.databricks.com/blog/whats-new-unity-ai-gateway-service-policies-guardrails-observability-and-cost-controls-ai
- Databricks docs — Unity Gateway observability: https://docs.databricks.com/aws/en/ai-gateway/observability
- Databricks docs — Log requests and responses for serving endpoints (inference tables): https://docs.databricks.com/aws/en/ai-gateway/inference-tables-serving-endpoints
- Microsoft Learn — Configure governance on model serving endpoints / Unity Gateway inference tables (legacy retirement dates)
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is readiness guidance, not a certification guarantee. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
