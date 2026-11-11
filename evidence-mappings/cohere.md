Last verified: November 11, 2026

# Cohere — Evidence Mapping

## What the platform is

Cohere is an enterprise AI platform: **North** (the agent workspace — agents, automations, shared knowledge, admin controls), **Compass** (enterprise search and retrieval over company documents, built on Embed and Rerank), and the **Command** model family with the Datasets and fine-tuning APIs. North runs in Cohere's cloud, a customer VPC, on-premises, or fully air-gapped. North 2 (announced 5 October 2026) added persistent agent memory, spending caps, and shared skill libraries. Cohere lists SOC 2 Type 2, ISO 27001, and ISO 42001 certifications for North — those cover Cohere, not a prospect's deployment.

## Mapping — platform artifact → ISO 42001 Annex A / SOC 2 CC

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| North audit trail & activity analytics — detailed logs of agent actions and changes; North Admin shows usage in real time down to user and agent, with token spend and limits | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | — |
| Compass structured activity logs — one INFO entry per index, document, and search request: endpoint, tenant, index, timestamp, and the user behind the token. Token rotations logged too | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | You collect and retain them in your own logging stack — Compass writes the entries to standard output; retention is your logging stack's policy. |
| North Admin — RBAC, SSO & human gates — roles, per-user identity, autonomy policies, guardrails for PII and prompt injection, human-in-the-loop approvals | A.9.2 Processes for responsible use; A.6.2.6 Operation and monitoring | CC6.1 Logical access; CC7.2 System operations | Wrapper | Needs named approvers and autonomy limits documented. |
| Datasets API with async validation — training and evaluation files as versioned datasets; data is validated before use, and the eval split drives early stopping | A.7.2 Data for development; A.7.4 Quality of data | CC8.1 Change management; CC4.1 Monitoring activities | In hand | — |
| Fine-tuning metrics record — Command R jobs log training loss at every step and validation loss and accuracy at every validation step, via Weights & Biases when a WandbConfig is supplied (chat fine-tuning only) | A.6.2.4 Verification and validation; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | — |
| Grounded output — citations & safety mode — Command returns inline citations; safety mode (Strict / Contextual — Off only on pre-R7B models) is set per request. RAG and tool use force Contextual. RAG guidance scores faithfulness, correctness, and coverage | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | RAG scoring is a method you run, not a managed eval suite. |

## The gap band — what Cohere does not give you

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Cohere gives you the evidence. ISO 42001 makes it certifiable — the wrapper an auditor can test. Cohere's own certification covers Cohere, not your deployment.

## Honest flags

- **Compass does not INFO-log user/group/role changes or invalid-token rejects.** Capture those from ingress-controller access logs. (Compass Access Management docs, verified.)
- **Compass logs are stdout, not a retained audit store.** Collection and retention are yours — e.g. Azure Monitor, CloudWatch, or Google Cloud Logging, under your retention policy. One token per person is what makes each logged operation map to an individual.
- **North Admin Audits are reported as Alpha** (permission, role, connector, and MCP-server changes via `/admin/audits`) — confirm availability on your North version before relying on it as evidence.
- **North 2 is new (October 2026).** Memory, spending caps, and Flow Control tiers are recent additions; confirm the exact behaviour on the deployed version.
- **Safety mode `Off` is not universal.** `OFF` is unavailable on Command R7B, Command A, and newer models, and with `tools` or `documents` the mode always defaults to `CONTEXTUAL` regardless of the value set; R7B / Command A RAG or tool-use calls support only `CONTEXTUAL`. (Cohere Safety Modes docs, verified.)

## Sources

- Cohere, North 2 announcement (Oct 2026): https://cohere.com/blog/introducing-north-2
- Cohere, Configuring Analytics Settings (North): https://private.docs.cohere.com/docs/admin/configuring_analytics_settings
- Cohere, Compass Access Management: https://private.docs.cohere.com/compass-standalone/compass/access-control
- Cohere, Safety Modes: https://docs.cohere.com/docs/safety-modes
- Cohere, Finetuning on Cohere's Platform (W&B integration): https://docs.cohere.com/v2/page/convfinqa-finetuning-wandb
- Cohere, RAG Citations: https://docs.cohere.com/docs/rag-citations
- Cohere, Deep Dive Into Evaluating RAG Outputs (faithfulness, correctness, coverage): https://docs.cohere.com/v1/page/rag-evaluation-deep-dive
- ISO/IEC 42001:2023 Annex A (38 controls)
- AICPA SOC 2 CC criteria

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
