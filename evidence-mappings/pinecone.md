Last verified: November 11, 2026

# Pinecone — Evidence Mapping

## What Pinecone is

Pinecone is a managed vector database — the retrieval layer behind RAG systems and agents. Embeddings are stored in serverless indexes, partitioned into namespaces and filtered by metadata at query time, and Pinecone enforces access control at the data layer, where retrieval happens. For a readiness engagement, its audit logs are the control-plane audit trail and its RBAC is the access evidence — but the data plane (what was actually retrieved) is not logged by Pinecone, so that evidence has to live in your application layer.

## Mapping — evidence you already have

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Audit logs exported to your own bucket — user, service-account and API actions written every 30 minutes as JSON to an S3 or GCS bucket you control, lockable WORM with S3 Object Lock | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Enterprise only, except the Standard HIPAA add-on ($190/month) also includes audit logging — Pinecone's cost docs list it in the add-on and require audit logs to be configured for HIPAA compliance with it. Off until enabled, never retroactive: only logs since the integration was created and enabled are saved. |
| Full control-plane event coverage — organisation, project, index, user, API-key and security events, each with actor, action, resource and timestamp | A.6.2.8 Recording of event logs; A.6.2.7 Technical documentation | CC7.2 System operations; CC6.1 Logical access | In hand | — |
| Index & backup lifecycle in the log — create, update and delete of indexes and backups are recorded; a backup restores to a new index | A.6.2.5 Deployment; A.6.2.8 Recording of event logs | CC8.1 Change management; CC7.4 Recovery | Wrapper | Needs a backup cadence and a tested restore. |
| RBAC for every principal — users, service accounts and API keys get organisation and project roles (Owner, Manager, Member), split into Control Plane and Data Plane Editor / Viewer, enforced at retrieval | A.9.2 Processes for responsible use; A.4.5 System and computing resources | CC6.1 Logical access; CC6.6 System boundaries | Wrapper | Permissions are the union of roles — needs access reviews. |
| SSO, SCIM & scoped API keys — SAML 2.0 SSO, SCIM provisioning on Enterprise, OAuth service accounts for the Admin API, and project-scoped keys that can never hold Owner or Manager | A.9.2 Processes for responsible use; A.6.2.6 Operation and monitoring | CC6.1 Logical access; CC6.2 Access provisioning | Wrapper | Needs a joiner / mover / leaver process behind it. SSO is on Standard and Enterprise plans. |
| Namespaces & metadata filtering — vectors partitioned by namespace and filtered by metadata at query time, so a search can be scoped to one tenant or classification — behind AES-256 at rest, TLS 1.2, CMEK and Private Endpoints | A.7.5 Data provenance; A.9.2 Processes for responsible use | CC6.1 Logical access; CC6.6 System boundaries | Wrapper | A namespace partitions — it does not authorise. Any data-plane key can query any namespace by naming it, so tenant scope must be enforced in application code. CMEK and Private Endpoints are Enterprise-only. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Pinecone gives you the evidence. ISO 42001 makes it certifiable — the policy, risk and accountability wrapper an auditor can test.

## Honest flags

- **Audit logs cover the management / control plane only** — not data-plane queries, upserts, or which vectors a RAG answer retrieved. That evidence lives in your application layer.
- **Audit logs are Enterprise-only, except the Standard HIPAA add-on also includes audit logging** (Pinecone's cost docs list audit logging in the $190/month add-on and require audit logs to be configured for HIPAA compliance with it). The add-on does not unlock private endpoints or CMEK.
- **Audit logs are off until enabled and never retroactive.** They are written every 30 minutes as JSON blobs to a bucket you control; only logs since the integration was created and enabled are saved. Disabling pauses delivery; removing the integration loses undelivered logs.
- **A namespace partitions — it does not authorise.** It is a filing system, not an entitlement check: a search inside one namespace never returns another namespace's vectors, but only if the application always queries the right one.
- **Pinecone's SOC 2 Type II / ISO 27001 covers Pinecone, not your deployment.** Your index configuration, keys, namespaces and application-layer enforcement are yours to evidence.

## Sources

- Pinecone Docs — Security overview: <https://docs.pinecone.io/admin/security/security-overview>
- Pinecone Docs — Configure audit logs: <https://docs.pinecone.io/admin/security/configure-audit-logs>
- Pinecone Docs — Manage roles and access (role tables, union of permissions): <https://docs.pinecone.io/admin/security/manage-rbac>
- Pinecone pricing (Audit Logs, Private Endpoints, CMEK and SCIM under Enterprise; HIPAA add-on $190/month on Standard): <https://www.pinecone.io/pricing/#plan-comparison-table>
- Pinecone Docs — Understand cost (HIPAA compliance add-on includes audit logging): <https://docs.pinecone.io/guides/cost/understand-cost>
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
