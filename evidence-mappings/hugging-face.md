Last verified: November 11, 2026

# Hugging Face — Evidence Mapping

## What Hugging Face is

Hugging Face Hub is the shared repository layer for open AI: models, datasets and demo apps (Spaces) live as Git repositories, each documented by a model or dataset card. Teams deploy a chosen model revision through Inference Endpoints (dedicated, autoscaling) or call models through Inference Providers. For a readiness engagement, the Hub's organisation audit log and the Git history behind every repo are the audit trail — they already exist, they just need to be collected and wrapped in a management system.

## Mapping — evidence you already have

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Organisation audit log, exportable as JSON (and via API) — membership, repository, Spaces, Jobs, OAuth and billing actions, each with who acted, what changed, location, anonymised IP and timestamp | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Export the JSON log on a schedule for long-term retention — Hugging Face publishes no audit-log retention period in its audit-log documentation. Export needs a token with the `org.auditLog.write` permission; the export itself is recorded as `org.audit_log.export`. |
| SSO, Resource Groups and token controls — SAML and OIDC sign-on, Resource Groups scoping repo access, managed tokens, and SCIM on Enterprise | A.3.2 AI roles and responsibilities; A.6.2.6 Operation and monitoring | CC6.1 Logical access; CC6.6 Access restrictions | Wrapper | Needs a documented joiner / leaver process. Basic SSO is on Team and Enterprise; SCIM is invitation-based on Enterprise (full lifecycle on Enterprise Plus). |
| Git-versioned repos, pinned in production — every model and dataset is a Git repo with commits, branches and tags; Inference Endpoints deploy a chosen revision behind a managed API | A.6.2.5 Deployment; A.6.2.7 Technical documentation | CC8.1 Change management; CC7.2 System operations | Wrapper | Needs a named production approver. Endpoints can target a specific revision commit, so production always runs the same weights even as the repo moves on — but pinning is opt-in; the default is the most recent commit. |
| Model cards and dataset cards — the README on every repo documents intended use, training datasets, base model, licence and limitations in structured metadata | A.6.2.7 Technical documentation; A.9.4 Processes for defining intended use | CC2.3 External communication; CC7.2 System operations | Wrapper | Cards are author-written — review completeness. Hugging Face does not verify card content. |
| Versioned datasets with a Dataset Viewer — datasets as versioned repos with documented splits and schemas; the Viewer lets reviewers inspect the actual rows | A.7.2 Data for development; A.7.5 Data provenance | CC7.1 System operations; CC4.1 Monitoring activities | Wrapper | Needs a documented review of the dataset card, splits and schema before the dataset is relied on. The Viewer shows rows; it does not attest data quality. |
| Evaluation results recorded on the model — Evaluate and Lighteval run benchmarks against Hub datasets; results sit on the model card and in `.eval_results` files tied to the benchmark | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Needs pass thresholds and a re-evaluation cadence. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with other policies, and the Statement of Applicability for the 38 controls. SOC 2: CC1.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups and society, plus the AI risk register. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Hugging Face gives you the evidence. ISO 42001 makes it certifiable — the wrapper an auditor can test.

## Honest flags

- **Audit logs are a Team & Enterprise feature** (confirmed against Hugging Face's own plan table — audit logs are listed for Team, Enterprise and Enterprise Plus, not Free). They record org, repo and admin actions — **not inference prompts or outputs**, which need their own logging.
- **Audit-log coverage is admin-side only.** Events follow a `scope.action` pattern across `org`, `repo`, `collection`, `spaces`, `resource_group`, `jobs`, `scheduled_job`, `oauth` and `billing`. Nothing in the log shows what a model was asked or what it returned.
- **Model and dataset cards are author-written, not verified by Hugging Face.** Card completeness must be reviewed; a missing limitations section is a gap, not a platform fault.
- **Token revocation and service accounts are Enterprise-only**; token administration is on Team and above. Check the tier before promising a control.
- **Export the JSON log for long-term evidence.** The Hub shows the log; Hugging Face publishes no audit-log retention period, so retention of the export is your job.

## Sources

- Hugging Face docs — Audit Logs: <https://huggingface.co/docs/hub/en/audit-logs>
- Hugging Face docs — Team & Enterprise plans: <https://huggingface.co/docs/hub/enterprise>
- Hugging Face docs — User Provisioning (SCIM): <https://huggingface.co/docs/hub/enterprise-scim>
- Hugging Face docs — Inference Endpoints, Advanced Setup (revision pinning): <https://huggingface.co/docs/inference-endpoints/en/guides/advanced>
- Hugging Face docs — Model Cards: <https://huggingface.co/docs/hub/model-cards>
- Hugging Face docs — Model Release Checklist (evaluation results in `.eval_results`): <https://huggingface.co/docs/hub/model-release-checklist>
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
