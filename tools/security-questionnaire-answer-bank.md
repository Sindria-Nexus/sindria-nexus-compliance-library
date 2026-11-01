# Security Questionnaire Answer Bank

Starter answers for the questions enterprise buyers ask first. These are
templates, not copy-paste answers: every `[bracket]` must be replaced with
your true answer, and any answer you cannot back up with evidence should be
rewritten as "not yet — here is our plan and date" rather than faked.

**Honesty rule that protects deals:** a buyer who catches one inflated
answer stops trusting the other 139. "Not yet, planned for [date]" closes
more deals than a confident lie that collapses in diligence.

## How to use this bank

1. Replace every bracket with your company's true answer.
2. Attach evidence references where noted (policy file, tracker row, ticket).
3. Keep a changelog: when an answer changes, note the date and why.
4. Never send the whole bank — answer the questionnaire you received, using
   these as your source of truth so answers stay consistent across buyers.

---

## Company and program

**Do you have a SOC 2 report?**
[Yes — SOC 2 Type (I/II), period ending (date), available under NDA. / Not
yet — currently in readiness, target audit period (dates). Our readiness
program is described at (link).]

**Do you have an information security policy?**
Yes. Our Information Security Policy is owned by [name, title], approved on
[date], and reviewed annually. [Available under NDA on request.]

**Who is responsible for security?**
[Name, title] owns the security program and reports to [founder / leadership]
quarterly. Security responsibilities are defined in our Information Security
Policy.

**Do you carry out risk assessments?**
Yes, annually, with a risk register reviewed quarterly. Risks are scored by
impact × likelihood, assigned an owner and a due date. (See our Risk
Assessment Policy.)

## Access control

**How do you control access to customer data?**
Access is role-based and least-privilege by default. Accounts are unique per
person, provisioned only from an approved request, and reviewed quarterly —
the signed review is retained as evidence. Leavers lose access on their last
working day, within 1 hour for involuntary departures.

**Is MFA enforced?**
Yes, MFA is required for all production, cloud, repository, and
administrative access, with no exceptions for seniority.

**How do you handle joiners, movers, and leavers?**
Joiners receive access only after identity verification and an approved
onboarding ticket. Role changes trigger an access review within 5 business
days, with old-role access revoked. Leavers are processed from a checklist
signed by [IT / engineering lead].

## Encryption and infrastructure

**Is data encrypted in transit and at rest?**
Yes. Data in transit uses TLS [1.2+] and data at rest is encrypted with
[AES-256 / cloud-provider default]. Encryption keys are managed in [key
management service], with access restricted to [roles].

**Where is data hosted, and where are backups?**
Production runs on [provider, region(s)]. Backups are [encrypted, region],
retained for [90 days] rolling, and restore-tested at least quarterly.

**Do you have logging and monitoring?**
Yes. [System] collects logs from production, cloud, and authentication
systems. Alerts route to [security contact / on-call], and logs are retained
for [1 year].

## AI and model data

These are the questions enterprise buyers ask AI startups first — and the
ones most teams fumble, because the honest answer is often "we hadn't
decided." Decide, write it down, and the answer becomes a strength.

**Do you use AI/LLM features, and what customer data do they process?**
Yes. Our product uses [model/provider] for [feature]. Customer data sent
to the model is limited to [data classes]; [no customer data is sent to
third-party model providers / data sent is limited to (scope) under our
vendor agreement with (provider)]. Our AI tool rules are defined in our
Acceptable Use Policy, and approved tools with permitted data classes are
listed in our approved-tools register.

**Do you train models on customer data?**
[No. Customer data is never used to train models, including third-party
foundation models — our contracts prohibit it, and training data comes
from [licensed / synthetic / public sources]. / Yes, only under (terms):
training uses [scope of data], under (customer consent / contract clause),
and customers may opt out via (mechanism).]

**How do you prevent customer data leaking through AI tools?**
Staff may use only approved AI tools, listed in our approved-tools
register with the data classes each tool may receive. Customer data,
credentials, and non-public company information are prohibited in public
AI tools, always. [We monitor for this via (endpoint controls / egress
filtering / policy + training).]

**What are your SLAs for remediating vulnerabilities by severity?**
Critical vulnerabilities are remediated within [7 days], High within [30
days], Medium within [90 days]. Findings are tracked to closure in
[tracker], and overdue items are escalated to [policy owner / leadership].
[Our most recent scan summary is available under NDA. / Not yet tracked
formally — planned for (date).]

## Incidents

**What is your incident response process?**
Incidents are reported to [security contact] immediately, triaged within 1
hour, contained, and reviewed in a written post-incident report within 14
days. Affected customers are notified within [72 hours] of confirmed impact,
or sooner where law or contract requires. (See our Incident Response Policy.)

**Have you had a security breach?**
[No known breach affecting customer data as of (date). / Yes — (date, scope,
remediation, customer notification). Post-incident review available under NDA.]

## Vendors

**How do you assess third-party vendors?**
Vendors are tiered by data access (Critical / Important / Low). Critical
vendors require a current SOC 2 report or ISO 27001 certificate, a signed
DPA, and annual review. All vendors are tracked in our vendor review tracker
with review dates and outcomes.

**Do you use subprocessors?**
Yes. Our current subprocessor list is at [link / available on request], and
customers are notified of changes [how, and how far in advance].

## Development and change

**How do you manage changes to production?**
All changes go through version control and peer review — the author cannot
approve their own change — with testing proportionate to risk and a recorded
rollback plan. Direct production edits are prohibited except under the
documented emergency process, reviewed the next business day.

**Do you perform penetration testing or vulnerability scanning?**
[Vulnerability scanning runs (frequency) via (tool); findings are triaged by
severity and tracked to remediation. Penetration testing is performed
(frequency) by (provider); the latest summary is available under NDA. / Not
yet — planned for (date).]

## Business continuity

**What is your availability commitment and backup plan?**
Our availability target is [X%]. Backups run [frequency], are encrypted, and
are restore-tested quarterly. Our recovery objective is [RTO / RPO].

## Privacy

**How do you handle personal data?**
Personal data is processed only for a stated purpose and minimized to what
that purpose requires. We sign DPAs where we process personal data for
customers. Data-subject requests go to [privacy contact] and are answered
within the legally required window.

---

*Changelog: record every answer change below so your answers stay consistent
across questionnaires.*

| Date | Question changed | Old answer | New answer | Reason |
|---|---|---|---|---|
| | | | | |
