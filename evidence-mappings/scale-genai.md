Last verified: November 11, 2026

# Scale GenAI — Evidence Mapping

## What the platform is

Scale GenAI Portfolio (SGP) is Scale AI's enterprise offering for building, deploying, and continuously improving agents that reason over your data. **Scale Post-Training**, a newer offering within the GenAI Portfolio launched 15 October 2026 in partnership with NVIDIA, customises open-weight models (including the NVIDIA Nemotron family) for a specific enterprise workflow. Agents can be deployed inside your own VPC on AWS, Azure, or GCP.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **GenAI Portfolio — full audit trail for every production agent.** What the agent did and why, with source-cited outputs. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | — |
| **Oversight built in before production.** Agents are built and tested against your enterprise standards, workflows, rules, and definition of "good" before they touch production. | A.6.2.4 Verification and validation; A.6.2.5 Deployment; A.9.2 Processes for responsible use | CC5.3 Control activities; CC8.1 Change management | Wrapper | Needs named approval and oversight roles. |
| **Deployment inside your own VPC** (AWS, Azure, or GCP). Data and agent activity stay in your boundary. | A.4.5 System resources; A.6.2.5 Deployment; A.10.3 Suppliers | CC6.1 Logical access; CC6.6 System boundaries | In hand | — |
| **Post-Training — representative evaluation dataset.** Scale defines what "correct" means for your workflow, then measures your current model against it. | A.6.2.4 Verification and validation; A.7.2 Data for development and enhancement; A.7.4 Quality of data | CC4.1 Monitoring activities; CC7.2 System operations | In hand | — |
| **Training and evaluation data built for that workflow**, including held-out data the model was not trained on. | A.7.3 Acquisition of data; A.7.5 Data provenance; A.7.6 Data preparation | CC8.1 Change management; CC7.2 System operations | Wrapper | Needs provenance recorded in your own register. |
| **Every version tested in its production workflow** — tested in the same agent workflow it will run in. | A.6.2.2 Requirements and specification; A.6.1.3 Responsible design and development processes; A.6.2.7 Technical documentation | CC8.1 Change management; CC2.3 Communication of changes | In hand | — |

## What Scale does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Scale gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- The audit-trail, pre-production testing, and evaluation-dataset claims are vendor statements on Scale's GenAI Portfolio page and the Scale–NVIDIA Post-Training announcement. Confirm in your own deployment that the audit trail is actually enabled and retained for your audit period — Scale's page does not publish a retention period for it.
- Post-Training is a new service (launched 15 October 2026). Its evaluation methodology is Scale-delivered, not a self-serve product feature: the evaluation dataset, training data, and per-version test results exist only if the engagement produced and retained them. Ask Scale for the retained artifacts, not just the headline accuracy figures.
- Scale's own certifications (SOC 2 Type II, ISO 27001, FedRAMP High, DoD IL4 provisional, as listed on its GenAI Portfolio page) cover Scale, not your deployment or your use of the agents.

## Sources

- Scale AI — GenAI Portfolio: https://scale.com/genai-portfolio
- Scale AI — "Scale Partners With NVIDIA on Post Training" (15 Oct 2026): https://scale.com/blog/scale-partners-with-nvidia
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
