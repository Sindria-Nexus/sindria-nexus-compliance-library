Last verified: November 11, 2026

# Google Vertex AI — Evidence Mapping

## What the platform is

Google Vertex AI is Google Cloud's managed AI platform for building, training, evaluating, deploying, and running models and agents — Gemini and Model Garden models, custom-trained models, and agents hosted on Vertex AI Agent Engine. A deployment on Vertex AI already generates three auditable artifacts: Cloud Audit Logs, Gen AI evaluation runs, and Agent Engine traces.

> **Naming note (verified November 11, 2026):** at Google Cloud Next 2026 (April 22, 2026) Google folded the Vertex AI brand into the **Gemini Enterprise Agent Platform** (console cutover May 21, 2026); Agent Engine is now called **Agent Runtime** in the new naming. The underlying APIs, service name (`aiplatform.googleapis.com`), and documentation paths are unchanged, and this file keeps the Vertex AI names used in the source mapping.

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Admin Activity audit logs — every admin write recorded: `datasets.create`, `endpoints.create`, `endpoints.deployModel` — who, with which identity, and when. Always on; cannot be disabled. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC8.1 Change management | In hand | Retained **400 days** in the `_Required` log bucket (fixed, cannot be changed). System Event audit logs are also always on and retained 400 days. |
| Data Access audit logs — admin reads, data reads and writes, including prediction calls (`endpoints.predict`, `rawPredict`, `generateContent`) as `DATA_READ`. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Off by default — enable per project, folder, or organization; nothing is written before enabling, so there is no backfill.** Retained **30 days** in the `_Default` bucket unless you configure custom retention or route the logs elsewhere. Reading Data Access logs requires the Private Logs Viewer role (`roles/logging.privateLogViewer`); the ordinary Logs Viewer role does not cover them. |
| Request-response logging to BigQuery — sampled prompts and responses for an endpoint written to a BigQuery table you own. | A.6.2.8 Recording of event logs; A.7.5 Data provenance | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Off by default, sampled** — set `enabled` to true and `samplingRate` to 1.0 for full coverage. Payloads over 10 MB are skipped automatically (documented for dedicated and Private Service Connect endpoints). It is configured per endpoint via the API (console/gcloud do not support it), and retention is whatever you configure on your BigQuery dataset. It cannot be enabled on an endpoint that also has Model Monitoring v1 enabled. |
| Access and container logging — access logging records timestamp and latency per request in Cloud Logging; container logging records the inference node's `stdout`/`stderr`. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Access logging is **off by default** on both `v1` and `v1beta1` endpoints. Container logging is **on by default on `v1`**, off by default on `v1beta1`. Both are set per deployed model; changing access-log settings requires undeploying and redeploying the model. |
| Gen AI evaluation runs — adaptive rubrics (pass/fail per prompt), static rubrics, and computation-based metrics (ROUGE, BLEU) on Gemini and Model Garden models. | A.6.2.4 Verification and validation; A.6.2.6 Operation and monitoring | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs a documented dataset, metrics, and retained runs. Adaptive rubrics are the recommended method; the older `EvalTask` interface does not support them and is no longer under active development. |
| Model Registry, Experiments & ML Metadata — model versions and aliases, experiment parameters and metrics, and lineage from dataset to deployed model. | A.7.5 Data provenance; A.6.2.6 Operation and monitoring | CC8.1 Change management; CC7.2 System operations | Wrapper | Lineage depends on jobs logging to ML Metadata — automatic via the Experiments SDK / Vertex Pipelines, manual otherwise. Without that logging there is no lineage record to evidence. |
| Agent Engine traces, sessions & logs — OpenTelemetry spans for every step, tool, and model call into Cloud Trace, structured logs in Cloud Logging, and Sessions / Memory Bank records. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Agent Engine only — needs a retention rule and alerting. Sessions and Memory Bank storage are billed separately from runtime. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Google gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags and footnotes

- **Audit logs are metadata, not content.** Cloud Audit Logs record who, when, which method, and whether it succeeded — they do not contain prompt or response bodies. Content-level evidence requires request-response logging.
- **Data Access logs are not retroactive.** The docs state they "aren't written unless explicitly enabled" — if they were not enabled before an incident, there is no record of the calls to query. Enable them on day one, in every project that runs Vertex AI.
- **Audit-log retention is split.** Admin Activity and System Event logs are kept 400 days in the `_Required` bucket (fixed). Data Access logs sit in the `_Default` bucket for 30 days unless you configure custom retention or route them to Cloud Storage, BigQuery, or Pub/Sub.
- **Request-response logging is sampled and capped.** Off by default; payload pairs over 10 MB are skipped automatically (documented for dedicated and Private Service Connect endpoints). It is configured per endpoint via the API (console/gcloud do not support it), and retention is whatever you configure on your BigQuery dataset. It cannot share an endpoint with Model Monitoring v1.
- **Evaluation runs are only evidence if retained.** Runs, datasets, rubrics, and pass/fail thresholds must be kept and versioned; an unrecorded eval is not audit evidence.

## Sources

- Google Cloud Documentation — Agent Platform audit logging: https://docs.cloud.google.com/vertex-ai/docs/general/audit-logging
- Google Cloud Documentation — Store log entries (log bucket retention): https://docs.cloud.google.com/logging/docs/store-log-entries
- Google Cloud Documentation — Use online inference logging (request-response logging): https://docs.cloud.google.com/vertex-ai/docs/predictions/online-prediction-logging
- Google Cloud Documentation — Gen AI evaluation service overview: https://cloud.google.com/vertex-ai/generative-ai/docs/models/evaluation-overview
- Google Cloud Documentation — Vertex AI Agent Engine overview: https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/reasoning-engine

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
