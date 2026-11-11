Last verified: November 11, 2026

# Surge — Evidence Mapping

## What the platform is

Surge AI is a managed expert-data service, not a self-serve platform. Frontier labs and enterprises commission it to build evaluation datasets, scoring rubrics and verifiers, RLHF preference data, SFT demonstrations, human evaluations, red-teaming, and RL environments — produced by vetted domain experts (doctors, lawyers, engineers, finance professionals, and other specialists). The buyer receives **delivered datasets and reports**, not a live audit trail they control.

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Custom evaluation datasets — expert-built prompts with reference outputs for your domain and failure modes. The public example of the form is GSM8K, the 8,500-problem grade-school math dataset Surge built with OpenAI. | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | Retain the delivered dataset, its version, and its acceptance record. |
| Rubrics and verifiers — expert-written scoring rubrics and verifiers that grade outputs the same way every time. AdvancedIF paired 1,600 prompts with rubrics of this kind (built with Meta Superintelligence Labs); frontier models failed 22–30% of its complex instruction-following tests, and using the rubrics as RL reward signals lifted accuracy by 13%. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs pass thresholds and escalation documented. |
| Off-the-shelf datasets and RL environments — catalog datasets and agent environments such as EnterpriseBench, with held-out results showing whether skills transfer. CoreCraft, the first EnterpriseBench environment, is a customer-support simulation of 2,500+ entities across 14 entity types with 23 tools; frontier models solve roughly 30% of its tasks. | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement | CC4.1 Monitoring activities; CC8.1 Change management | Wrapper | Needs applicability to your system documented — a public benchmark result is not evidence about your deployment. |
| Human evaluation results — domain experts score model outputs for usefulness, safety, logic, and clarity, with explanations of where and why outputs fail. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | In hand | Retain the scored results and the failure explanations, not just a summary score. |
| RLHF preference data and SFT demonstrations — expert preference rankings, reward signals, and worked demonstrations that become the training record for the next version. | A.7.2 Data for development and enhancement; A.7.4 Quality of data; A.6.2.3 Design and development | CC8.1 Change management; CC4.1 Monitoring activities | Wrapper | Needs data provenance and acceptance criteria retained. |
| Red-teaming and safety evaluation — adversarial testing and safety annotation by vetted experts, surfacing vulnerabilities before deployment does. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use; A.6.2.6 Operation and monitoring | CC3.2 Risk identification; CC4.2 Evaluation of deficiencies | Wrapper | Needs findings tracked through to remediation. A red-team report with open findings is evidence of a known risk, not of a fixed one. |

## The gap is the engagement

No delivered dataset covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Surge gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags and footnotes

- **Surge is a managed service, not a self-serve platform.** You receive delivered datasets and reports, not a live audit trail you control. There is no public pricing and no self-serve entry — every engagement starts with a sales conversation, and the service is not set up for small one-off datasets.
- **Annotator selection and QC are not independently auditable from outside.** Quality control and annotator selection are a black box you take on trust; there is no way to audit the pipeline the way you can with software you host. Retain rubrics, acceptance criteria, and delivery records contractually — that retained paper trail is your evidence, not Surge's internal process.
- **A `surge-api` Python client exists for scripted workflows**, but it is a way to submit and receive work, not a self-serve platform or a live audit trail.
- **Workforce-size claims vary by source** (100,000+ vetted workers in some coverage; 200,000+ PhDs and experts in Surge's own counts) — do not cite a headcount number as evidence; cite the delivered dataset, its rubrics, and its acceptance record.
- **Public benchmarks prove the method, not your system.** GSM8K, AdvancedIF, and EnterpriseBench/CoreCraft demonstrate Surge's capability; only a dataset built and run against *your* system evidences *your* controls.

## Sources

- Surge AI — Research (GSM8K, AdvancedIF, EnterpriseBench / CoreCraft): https://surgehq.ai/research
- Surge AI — Building AdvancedIF: https://surgehq.ai/blog/advancedif-and-the-evolution-of-instruction-following-benchmarks
- Seminal — Data labeling, RLHF and human evaluation vendors (Surge delivery model): https://seminal.ai/reference/categories/data-labeling-rlhf-human-evaluation-vendors/
- Hokai — Surge AI review (product suite, sales-led model): https://hokai.io/hub/tools/surge-ai
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 CC criteria

## Disclaimer

This is readiness guidance, not a certification guarantee. Applicability is set in your Statement of Applicability and tested by your auditor. Any certification Surge holds covers Surge's own operations — not your deployment, your evaluation design, or your use of the delivered data.
