# Clause Mistakes and Fixes — ISO 42001 Clauses 4–10

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title — the AI governance owner] |
| **Scope** | [Which AI systems, teams, and business units are in the AI management system] |
| **ISO 42001 mapping** | Clauses 4–10 (the management system) |
| **Control** | AI-07 |
| **Companion files** | `05-iso-42001-readiness-checklist.md` (the phased path), `01-ai-governance-policy.md`, `02-ai-system-inventory.md`, `03-ai-impact-assessment-template.md`, `04-ai-data-and-model-change-control.md` |

## 1. Purpose

This guide is the companion to the readiness checklist. The checklist tells you the order to build in. This guide tells you where teams actually fail at each clause — with a concrete example of the mistake, what the auditor writes about it, and the fix that closes it.

Every example below is a real failure pattern: a scope, a policy, a risk register, or a review that looked finished on paper and fell apart when an auditor tested it. Read the clause you are working on before you build it, not after the audit finds it.

How to use this guide:

1. Pick the clause you are about to implement.
2. Read its mistakes first. Check whether any of them already describe your company honestly.
3. Apply the fixes in order. Each fix names the evidence it produces — if you cannot produce that evidence, the fix is not done.
4. Run the self-test at the end of each clause. It is the question an experienced auditor asks that a checklist auditor does not.

A note on what this guide is not: it is not the standard. ISO/IEC 42001:2023 is a paid document — read it alongside this guide, and have your certification body confirm scope and timing for your situation. What this guide does is stop you paying for the same findings other teams already paid for.

## 2. Clause 4 — Context of the organisation (4.1–4.4)

**What the clause requires.** Understand your internal and external context as it relates to AI (4.1); identify interested parties and their needs (4.2); determine the scope of the AI management system (4.3); and establish, implement, maintain, and continually improve the system itself (4.4). The scope statement is a written document, and every boundary in it needs a reason.

### How teams mess it up

**1. Scope games — the riskiest system sits outside the boundary.**
*Example:* A startup scopes its AIMS to "the customer-support chatbot" and leaves its hiring-screening model and its credit-scoring model outside scope, because those are the hard ones to govern. The auditor walks the AI inventory against the scope statement and asks one question: "Why is this system outside it?" There is no good answer, and the auditor's trust in the whole scope is gone in that moment.
*What the auditor writes:* scope not defensible; exclusions without risk-based justification.

**2. Boilerplate context — the analysis could describe any company.**
*Example:* The 4.1 document reads "we operate in a competitive market with evolving regulation." It names no models, no data, no failure modes, no regulation. It was copied from an ISMS template with "AI" find-and-replaced in.
*What the auditor writes:* context analysis is generic; no AI-specific internal or external issues identified.

**3. Forgotten affected parties — the people the AI decides about are missing.**
*Example:* The interested-party register lists customers, regulators, and employees. It omits the applicants screened by the hiring model, the borrowers scored by the credit model, and the patients triaged by the diagnostic tool — the people with the most at stake in the system's decisions.
*What the auditor writes:* interested parties identified, but their requirements were not translated into AIMS objectives or controls.

**4. A register that is a list, not governance.**
*Example:* The register exists and looks complete, but nobody ever spoke to the affected people. It was built in a conference room, with no outside conversation. No party on it maps to a requirement the system must meet.
*What the auditor writes:* same finding as mistake 3 — identification without translation.

**5. Context written once and never revisited.**
*Example:* The context analysis was written at implementation, then a new regulation landed, a new model deployed, and a new risk emerged. None of it made it back into the analysis. The document is a photograph of a company that no longer exists.

### How to fix it

1. **Run a real context workshop with leadership in the room.** Internal AI reality on one wall — which models you deploy, what data they touch, what could go wrong. External pressures on the other — the EU AI Act, sector rules, customer requirements, public expectations. The workshop output *is* the 4.1 evidence.
2. **Give every interested party a requirement.** Add a column to the register most templates skip: "requirement this creates for our AIMS." Every party maps to at least one requirement, or they are not on the register.
3. **Write the scope with explicit boundaries and lifecycle stages.** Which AI systems, which business units, which stages (development, deployment, both, one product line). Get leadership to sign it — the signature is Clause 5 evidence too.
4. **Set a review trigger.** Revisit the context analysis whenever the world changes: a new regulation, a new deployment, a new risk. Record the review, even when nothing changed.

**Evidence this produces:** workshop output and attendance; interested-party register with a requirement per party; signed scope statement with boundaries, lifecycle stages, and reasons for exclusions.

**Auditor asks:** "Show me the scope statement — and show me the riskiest AI system you run. Is it inside it?"

**Self-test:** Look at what sits *outside* your scope. Was the boundary drawn by risk, or by convenience? If the hard system is outside, the scope is the finding.

## 3. Clause 5 — Leadership (5.1–5.3)

**What the clause requires.** Top management must *demonstrate* commitment to the AIMS (5.1) — owning the policy, providing resources, holding people accountable. The AI policy must be approved at the top, aligned with the security policy, privacy policy, and code of ethics, communicated, and reviewed on a schedule (5.2). Roles, responsibilities, and authorities must be assigned to named individuals with actual authority (5.3).

### How teams mess it up

**1. Signature leadership — the CEO signs and vanishes.**
*Example:* The CEO signed the AI policy at launch and has not attended a review since. Everything was delegated to IT. Delegation of everything is not leadership commitment, and the auditor knows it in the first management interview.
*What the auditor writes:* leadership commitment not demonstrated; no evidence of top-management engagement beyond signature.

**2. Department roles — responsibility assigned to a team, not a person.**
*Example:* The role register says "the engineering team is responsible for AI governance." No name, no authority, no time. When the auditor asks who can stop a launch, the room looks at each other.
*What the auditor writes:* roles assigned but individuals lacked authority or time to execute them.

**3. Paper roles with no power — including a structural conflict.**
*Example:* The AI governance owner reports to the CTO whose team ships the models. The person who can stop a launch answers to the person incentivised to launch. The role exists; the veto does not. It has never been tested, because it cannot be.
*What the auditor writes:* usually nothing — most auditors do not map reporting lines. That is exactly why this one hurts: it passes the audit and fails in real life.

**4. A policy nobody wrote or read.**
*Example:* A consultant wrote the AI policy. The CEO signed it without reading it and cannot defend its contents without notes. The policy also contradicts the privacy policy on data use — nobody compared them.
*What the auditor writes:* policy approved but not understood by leadership; alignment with other policies not demonstrated.

**5. Leadership cannot articulate the system — the most under-prepared moment in the audit.**
*Example:* The auditor interviews top management. The CEO cannot explain, in their own words, the AI policy, the organisation's top AI risks, or their personal role in the system. No amount of paperwork saves the clause after that interview.

### How to fix it

1. **Assign roles as a RACI with names, authority levels, and time allocation.** If the AI governance owner has no hours budgeted, the role is fiction. Name who owns AI governance overall, who owns each system, who approves a launch, and who can pull the plug.
2. **Check the reporting line before the auditor does.** The governance owner must not report to the person shipping the models. Fix the conflict, or document why the structure still gives the owner a direct line to leadership that bypasses the delivery chain.
3. **Test the veto.** Ask the role-holder: have you ever said no? Do you have budget? Do you have a direct line to leadership? A role without a tested veto is decoration.
4. **Prepare leadership for the interview like a board meeting.** The CEO should be able to answer three questions cold: what is our AI policy, what are our top three AI risks, and what is my personal role in the system? Rehearse it.
5. **Keep the policy alive.** Approved at the top, aligned with security, privacy, and ethics policies, communicated to everyone it applies to, reviewed on a schedule — with review records to prove it.

**Evidence this produces:** signed policy with version history and review records; RACI with names, authority, and time allocation; meeting minutes showing leadership engagement; resource and budget records; communication records (who was told what, when).

**Auditor asks:** "Show me a decision top management made about AI governance — and let me ask them about it."

**Self-test:** Ask the governance owner to explain, without notes, what the AI systems decide, what data they were trained on, and where they can fail. Then ask whether they have ever stopped a launch. If either answer is no, Clause 5 is paper.

## 4. Clause 6 — Planning (6.1–6.3)

**What the clause requires.** Plan actions to address risks and opportunities (6.1): assess AI risk at organisation level (6.1.2), treat it by selecting controls and comparing them against Annex A to produce the Statement of Applicability (6.1.3), and assess the impact of each AI system on individuals, groups, and society (6.1.4). Set measurable AI objectives with owners, resources, and deadlines (6.2). Plan changes to the AIMS before they happen (6.3).

The single most important sentence in this clause: **risk criteria must be defined *before* the assessment happens.** Criteria written after the assessment are rigged — the assessor already knows which risks they want to accept and sets the threshold to match.

### How teams mess it up

**1. Methodology after the fact — the ruler drawn around the answer.**
*Example:* The team assesses risks, finds three it would rather not treat, then writes the acceptance threshold so those three fall just inside "acceptable." The threshold was set so high that nothing ever needs treatment — "acceptable" means "anything short of a lawsuit."
*What the auditor writes:* risk criteria exist, so this often passes. The failure is real anyway: the whole assessment is theatre, and the expert's first question exposes it — who set the threshold, and what would have to happen for a risk to be unacceptable?

**2. The one-off workshop — a spreadsheet, never revisited.**
*Example:* One risk workshop at implementation, one spreadsheet, filed away. No schedule, no re-assessment when the world changes. Risk assessment is a process, not an event, and the register is already stale.
*What the auditor writes:* incomplete or undocumented risk assessments — the most-cited nonconformity in ISO 42001 audits, and the most common reason engagements stall at Stage 1.

**3. Impact assessments after launch — written to justify a deployment that already happened.**
*Example:* The hiring model went live in March. Its impact assessment is dated May, and reads like a defence of the launch decision. The assessment exists, but it was a diary, not a control.
*What the auditor writes:* "AI system impact assessment not performed prior to deployment."

**4. A Statement of Applicability disconnected from risk.**
*Example:* A consultant wrote the SoA. An auditor pulls one line — a control claimed as implemented — and asks which risk treatment decision it traces to. Nothing is attached. A control in the SoA with no risk behind it, or a risk with no treatment, breaks the chain.
*What the auditor writes:* risk treatment plan exists, but the SoA does not trace to risk treatment decisions; residual risk acceptance not documented or approved by management.

**5. Control shopping — risk written to justify the controls you already have.**
*Example:* The team already has a data-loss-prevention tool, so the risk assessment is written to conclude that data loss is the main AI risk. Fairness, autonomy, and societal impact never appear — because the methodology cannot see them. The assessment found exactly the risks the existing controls solve, and none of the ones they do not.
*What the auditor writes:* often nothing — the paperwork is complete. The expert checks what the methodology is blind to: Annex C lists risk sources most frameworks never consider, including explainability gaps, automation bias, environmental impact, and concentration of power.

**6. Unmeasurable objectives and orphaned risks.**
*Example:* The objective is "promote responsible AI." No metric, no owner, no date. The risk register names owners who have never seen the register. Residual risk on a high risk was accepted by someone without the authority — or the information — to accept it, and nobody can show who, when, or on what basis.

### How to fix it

1. **Define risk criteria first, in writing, with leadership sign-off.** Likelihood scale, impact scale, acceptance threshold. Before a single risk is assessed. This document is the foundation; everything else stands on it.
2. **Run the org-level risk assessment as a structured process, not a brainstorm.** Use Annex C's risk sources as a checklist so the methodology cannot be blind to fairness, transparency, and societal impact. Document the methodology itself, not just the results.
3. **Do impact assessments per system, before deployment decisions.** Use a template that forces the assessor to name who is affected, how severely, and what mitigations exist — see `03-ai-impact-assessment-template.md`. Date-stamp everything; the date is evidence.
4. **Build the risk register as a living document.** Every risk has an owner who knows they own it, a treatment plan, and a residual-risk sign-off by someone with authority. Review it on a schedule, not when the audit approaches.
5. **Write the SoA as the output of the treatment process, not a standalone exercise.** Every applicable control traces to a risk treatment decision; every exclusion traces to a documented reason. An auditor should be able to follow any line in the SoA back to a risk.
6. **Set objectives that are measurable, owned, and dated.** Each with a monitoring cadence. Review them at management review (Clause 9.3) and record the review.

**Evidence this produces:** signed risk criteria; risk assessment records and risk register; risk treatment plan; Statement of Applicability with traceability to risk decisions; per-system impact assessments with dates; objectives with owners, metrics, and review dates; residual-risk acceptance sign-offs.

**Auditor asks:** "Pick a risk. Show me the chain: identification, treatment, control, SoA entry. Then show me who accepted the residual risk."

**Self-test:** Ask a named risk owner what they are doing about their risk. Ask the person who signed off a high residual risk what they thought they were signing. Ask whether the impact assessment predates the launch it was supposed to gate. Any "I don't know" is the finding.

## 5. Clause 7 — Support (7.1–7.5)

**What the clause requires.** Determine and provide the resources the AIMS needs (7.1). Ensure people doing work that affects the AIMS are competent — proven ability, on the basis of education, training, or experience — and evaluate whether training actually worked (7.2). Ensure people are aware of the AI policy, their contribution, and the implications of not conforming (7.3). Determine what to communicate, to whom, when, and how — internally *and* externally (7.4). Control documented information: identification, format, review, approval, distribution, access, retrieval, storage, preservation, retention, and disposition (7.5).

### How teams mess it up

**1. Training as a checkbox — attendance recorded, effectiveness never evaluated.**
*Example:* Everyone completed the AI awareness course. The records show attendance. Nobody was tested on anything, and Clause 7.2 explicitly requires evaluating whether the action worked. The records are attendance logs, not competence proof.
*What the auditor writes:* "Competence requirements not defined for roles affecting the AIMS" — and training records with no assessment of effectiveness.

**2. Competence assumed from a title.**
*Example:* "She's a senior engineer, so she's competent on AI governance." The person who approves model deployments has no machine-learning background; the person who signs off on data quality has never seen a training dataset. Competence is specific to the work, not the seniority.
*What the auditor writes:* a CV on file is not competence evidence for *this* role on *these* systems.

**3. Awareness as a single email.**
*Example:* The policy was sent once, attestations collected, awareness declared complete. Ask a support agent what they do when the AI gives a wrong or biased answer and they do not know. Awareness that only exists on a signature page is not awareness.

**4. Document sprawl — the real procedure lives outside the system.**
*Example:* The controlled system holds version 3 of the deployment procedure. The team follows a PDF saved on a desktop from 2024, a printed procedure taped to a monitor, and a Slack message that replaced the official process. A procedure nobody can find, or a stale procedure people still follow, is a finding.
*What the auditor writes:* "Documented information not controlled — outdated versions in use."

**5. Internal-only communication, and resources that exist only on paper.**
*Example:* The communication plan covers staff and forgets customers, regulators, and affected users entirely — the people the AI decides about were never informed, in language they understood. Separately, the budget was approved and the role was funded, but the money was never spent and the role was never filled. Allocation is not expenditure.

### How to fix it

1. **Build a competence matrix per role.** For each role affecting the AIMS, define the required competence — including AI-specific knowledge of model limitations, data bias, and failure modes — assess the current person against it, and close gaps with training or hiring. Record the assessment, not just the training.
2. **Train with assessment, not just attendance.** Every training ends with a check: a quiz, a practical exercise, a scenario. The evaluation of effectiveness is the evidence; the attendance sheet is the cover page.
3. **Run awareness as a programme, not an event.** Real scenarios from the client's own AI systems, short refreshers, and spot-checks — ask people what they would do. Record the spot-checks; they are the strongest awareness evidence an auditor can see.
4. **Set up document control before the documents pile up.** Version numbers, approval workflow, access rules, retention schedule. One controlled repository, not five shared drives. If a document is not in the system, it does not exist.
5. **Write a communication plan that includes external parties.** Who gets told what, when, and how — including affected users and regulators. Record the communications that actually happened.
6. **Check that resources are real.** Show the money actually spent and the hours actually worked, not just the budget approved.

**Evidence this produces:** competence matrix with assessments per role; training records with effectiveness evaluations; awareness spot-check records; communication plan and records of communications sent; controlled-document register with versions, approvals, access, and retention; resource expenditure records.

**Auditor asks:** "Show me a training record — and show me how you know the training worked. Then let me ask a member of staff what the AI policy says."

**Self-test:** Ask the person who approves deployments to explain the model's failure modes. Pull a procedure at random — is it the current version, and is anyone actually following it? Were affected users actually informed, or was communication internal-only?

## 6. Clause 8 — Operation (8.1–8.4)

**What the clause requires.** Plan, implement, and control the processes needed to meet AIMS requirements, with criteria for those processes and records proving they ran as planned (8.1). Perform AI risk assessments at planned intervals and whenever significant changes occur (8.2). Perform AI system impact assessments before deployment and whenever the system changes in a way that could affect its impacts (8.3). Maintain documented information about the AI systems in operation — what the system is, what data it uses, what decisions it makes, how it is monitored, what changed and when (8.4).

The structural point most teams miss: **Clause 6 plans the processes, Clause 8 operates them.** The risk assessment process defined in 6.1.2 gets *performed* in 8.2. The impact assessment process defined in 6.1.4 gets *performed* in 8.3. Auditors test both: did you design it right, and did you actually do it?

### How teams mess it up

**1. Assessments as a launch ritual, never revisited.**
*Example:* The impact assessment was done once at deployment. Since then the model was retrained twice, the training data changed, and the user population doubled. No re-assessment. A model retrained on new data is, in governance terms, a new system — new behaviour, new risks, new impacts — but the team treats it as the same system with a version bump.
*What the auditor writes:* "Changes to the AI system (retraining on new data) did not trigger re-assessment."

**2. Monitoring uptime, not behaviour.**
*Example:* The dashboard is full of latency and error rates. Nothing measures output quality, drift, or fairness. Performance has drifted over months and outputs have slowly skewed, and the monitoring would never catch it — it is a smoke detector that only checks whether the house is still standing.

**3. System documentation as marketing copy.**
*Example:* The "system documentation" is a paragraph describing what the product does for customers. It says nothing about data provenance, model version, decisions made, or change history. A stranger — a new engineer, an auditor, an investigator — could not reconstruct what the system does and why from these records alone. Documentation that only makes sense to the person who wrote it is a diary, not a control.

**4. Change without re-assessment.**
*Example:* A new data source was added and the use case expanded to a new population. Both were treated as routine maintenance. The standard says re-assess when significant changes occur; the team sampled its last ten changes and could not show that any of them had been evaluated for whether they triggered re-assessment.

**5. The untested gate — and the flagship system nobody governs.**
*Example:* The deployment gate has never stopped anything, so nobody knows if it works. And the system the organisation is proudest of — the flagship product, the revenue-critical model — is the least governed, because nobody wants to slow down the thing that makes money. The auditor samples a few systems; the expert checks the ones the auditor did not pick.

### How to fix it

1. **Set an operational cadence in writing.** Assessment schedule — risk assessments annually, impact assessments per system before deployment and on change — with named triggers for out-of-cycle re-assessment: retraining, new data, new population, new regulation, any incident.
2. **Make the deployment gate real.** No system goes live, or goes live again after a change, without a completed impact assessment, a risk assessment on file, and system documentation in place. Record the gate decisions, including the ones that say no. If nothing has ever been stopped at the gate, the gate is decorative.
3. **Build system documentation as a template.** Your inventory (`02-ai-system-inventory.md`) plus a per-system record: purpose, data used and its provenance, model version, decisions made, monitoring in place, change history. Model-card format, not marketing format.
4. **Monitor behaviour, not just uptime.** Drift metrics, output sampling, fairness checks on a schedule. The monitoring records are 8.4 evidence; the monitoring *design* is what separates a governed system from a watched one.
5. **Log changes as governance events.** Every retraining, data change, and use-case expansion gets a change record and an explicit re-assessment decision — yes, with a new assessment, or no, with a reason. The decision log is the evidence that change control works.

**Evidence this produces:** operational cadence and trigger list; deployment-gate records including refusals and delays; per-system documentation (model-card format); monitoring records for drift, output quality, and fairness; change log with re-assessment decisions.

**Auditor asks:** "Pick a system in production. Show me the chain: risk assessment, impact assessment, documentation, monitoring — end to end. And show me the dates."

**Self-test:** Pick the system the organisation is proudest of. Does monitoring measure model behaviour, or just uptime? Was a deployment ever blocked by a failed assessment? Could a stranger rebuild the system from its documentation?

## 7. Clause 9 — Performance evaluation (9.1–9.3)

**What the clause requires.** Determine what to monitor and measure — including AI system performance — the methods, when to do it, when to analyse the results, and who evaluates them (9.1). Conduct internal audits at planned intervals, with defined criteria, scope, frequency, and methods, by auditors who are impartial (9.2). Top management reviews the AIMS at planned intervals for continuing suitability, adequacy, and effectiveness, considering prescribed inputs and producing decisions (9.3).

The operational fact that matters most: **you cannot pass a Stage 2 certification audit without a completed internal audit *and* a completed management review first.** Certification bodies require at least one full cycle of both before they will test the system in operation. Clients who rush to Stage 2 without them get turned away at Stage 1. This is the single most common scheduling mistake in ISO 42001 engagements.

### How teams mess it up

**1. The self-audit — the builder auditing their own build.**
*Example:* In a small team, the person who built the AIMS audited it. Or the internal auditor reports to the person whose work they are auditing. Independence on paper, dependence in practice. "I audited my own work" is a finding.
*What the auditor writes:* internal audit impartiality not demonstrated.

**2. The rehearsal audit — findings suppressed, scope narrowed, zero findings.**
*Example:* The internal audit was treated as a dress rehearsal for the real audit. The scope was narrowed to the tidy parts, uncomfortable findings were softened out of the report, and the audit found nothing — despite known issues in the area audited. An internal audit that finds nothing is suspicious, not reassuring. Zero findings means the auditor was blind, the scope was rigged, or the organisation is perfect — and only one of those is plausible.
*What the auditor writes:* "Internal audit conducted, but no nonconformities raised despite known issues in [area]."

**3. The rubber-stamp review — minutes with no decisions.**
*Example:* Management review happened on the calendar, minutes were written, and no decisions were made. Or decisions were recorded — owners assigned, dates set — and then nothing happened. Auditors check the minutes exist. The failure is that nobody checked whether the decisions were executed. A review that produces decisions nobody implements is a performance, not governance.

**4. No AI performance monitoring — the system is monitored, the AI is not.**
*Example:* Monitoring covers the management system — reviews held, training done. The AI systems themselves are not monitored for performance, drift, or output quality. The dashboards stay green while the models degrade.

**5. Metrics that can never go red.**
*Example:* Every metric is green, every quarter. The metrics were chosen to look good, or the thresholds were set so they can never fail. A metric that is always green measures nothing.

### How to fix it

1. **Build the audit programme before you need it.** Schedule, criteria, scope, and an impartial auditor named in advance. A one-person startup has to solve impartiality honestly — external auditor, peer review, or a qualified contractor. Plan the first full cycle (internal audit + management review) to complete *before* Stage 2 is booked. This is a timeline decision, not a paperwork decision.
2. **Run the internal audit like a real audit.** Competent auditor, meaningful sampling, honest findings. A good internal audit finds things. If it finds nothing, widen the scope or change the auditor.
3. **Run management review as a decision meeting.** Prescribed inputs on the table — status of actions from previous reviews, changes in internal and external issues, AIMS performance (nonconformities, monitoring results, audit results, fulfilment of AI objectives), opportunities for improvement. Decisions recorded with owners and dates. Previous decisions tracked for completion. The minutes are the evidence; the follow-through is the proof.
4. **Choose metrics that can go red.** Monitor AI system performance (drift, output quality, fairness) alongside management-system health. Record the reds and what was done about them. A metric history with a red in it is more credible to an auditor than a year of green.

**Evidence this produces:** internal audit programme (criteria, scope, frequency, methods, impartial auditor); audit reports with findings; management review minutes with decisions, owners, and dates; monitoring and measurement records including AI system performance; tracking of previous review decisions to completion.

**Auditor asks:** "Show me the internal audit programme, the audit reports, the management review minutes, and the nonconformity log — as one story. Did the audit cover the AIMS, were findings raised, did management review consider them, and did corrective action follow?"

**Self-test:** Show me a metric that went red this year, and what you did about it. Read the last management review minutes — were decisions made, and were they executed? If the internal audit found nothing, was it an audit or a rehearsal?

## 8. Clause 10 — Improvement (10.1–10.2)

**What the clause requires.** When a nonconformity occurs, react to it, evaluate the need for action to eliminate its cause so it does not recur or occur elsewhere, implement the action, review its effectiveness, update the risk assessment if needed, and make changes to the AIMS if needed (10.1). Records are retained of the nonconformity, the action, and the results. Then continually improve the suitability, adequacy, and effectiveness of the AIMS — not periodically, not when the audit approaches, continually (10.2).

The critical sequence is cause → action → *verify effectiveness*. A corrective action that was never verified is an assumption, not a fix.

### How teams mess it up

**1. Symptom fixes — the visible problem fixed, the cause untouched.**
*Example:* A biased output reached a customer. The team apologised, corrected that one output, and closed the ticket. The training-data bias that produced it was never investigated. Six weeks later the same nonconformity recurred — the log grew, the system did not learn.

**2. Closed without an effectiveness check.**
*Example:* The nonconformity log is full of closed actions. Pick one and ask: did the fix work? Is there evidence the same issue has not recurred? There is none. The action was recorded and closed; nobody checked whether it worked. The closure was fiction.
*What the auditor writes:* closed nonconformities with no effectiveness verification.

**3. The lesson goes nowhere — the risk assessment never changes.**
*Example:* A nonconformity revealed a risk the risk assessment had missed — a failure mode nobody had scored. The ticket was closed, but the risk register, the controls, and the training were never updated. A nonconformity that teaches the organisation nothing is a wasted failure.

**4. Improvement on paper only — continual means "before the audit."**
*Example:* The log is full, the same issues keep recurring, and the system is exactly where it was last year. Improvement happens in the month before the surveillance audit and nowhere else. That is not continual improvement; it is a snapshot that degrades from the day it was certified.

### How to fix it

1. **Operate the nonconformity log as a learning system.** Every nonconformity gets root-cause analysis, a corrective action, an effectiveness check at a defined interval, and a risk-assessment update where relevant. A closed nonconformity without an effectiveness check is not closed.
2. **Fix the cause, not the symptom.** Then follow the closed item forward: did it come back? If yes, the fix failed — reopen it, do not file it.
3. **Feed the lesson back in.** If a nonconformity reveals a gap, update the risk assessment, the controls, or the training. That is what continual improvement actually means — the system changes because of what it learned.
4. **Keep it going, not just before the audit.** Continually means continually. Review the log on a schedule, track recurrence, and let management review (Clause 9.3) see the pattern, not just the count.

**Evidence this produces:** nonconformity log with root-cause analysis per item; corrective-action records with effectiveness checks and dates; risk-assessment updates triggered by nonconformities; recurrence tracking; management review records showing improvement decisions.

**Auditor asks:** "Pick a closed nonconformity. Show me the fix — and show me the evidence it worked and the issue has not recurred."

**Self-test:** Pick a closed nonconformity and follow it forward. Did it recur? Did the risk register change because of it? If the answer to both is no, the system did not learn. It just filed paperwork.

## 9. Evidence this guide produces (Control AI-07)

| Evidence | Where it lives | Retention |
|---|---|---|
| This guide, adopted with owner and review date | [program location] | Current + prior versions [3 years] |
| Clause self-tests completed, with findings noted | [program location] | [3 years] |
| Risk criteria, risk register, SoA (Clause 6 fixes) | [program location] | Life of certification + [3 years] |
| Competence matrix and training effectiveness records (Clause 7 fixes) | [program location] | [3 years] |
| Deployment-gate records including refusals (Clause 8 fixes) | [program location] | [3 years] |
| Internal audit reports, management review minutes (Clause 9 fixes) | [audit location] | [3 years] |
| Nonconformity log with effectiveness checks (Clause 10 fixes) | [program location] | [3 years] |

## 10. Quick reference — the finding in one line per clause

| Clause | The finding that gives it away |
|---|---|
| 4 — Context | The riskiest AI sits outside the scope. |
| 5 — Leadership | The CEO cannot explain the policy, the top risks, or their role. |
| 6 — Planning | The SoA does not trace to a risk decision. |
| 7 — Support | Training records show attendance; nothing shows anyone learned. |
| 8 — Operation | The impact assessment is dated after the launch it was supposed to gate. |
| 9 — Performance evaluation | The internal audit found nothing. |
| 10 — Improvement | The same nonconformity is back, six weeks after it was "closed." |

---

*What this guide does not do: it does not guarantee certification, and it does not replace the standard itself — read ISO/IEC 42001:2023 alongside this guide, and have your certification body confirm scope and timing for your situation. What it does is stop you paying for the findings in section 10, which other teams already paid for.*
