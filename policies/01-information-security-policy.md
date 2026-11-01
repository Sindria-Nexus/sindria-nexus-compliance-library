# Information Security Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual, and after any material change or security incident |
| **SOC 2 mapping** | CC1 (Control Environment), CC2 (Communication & Information), CC7 (System Operations) |

## 1. Purpose

This policy establishes [Company Name]'s information security program: how we
protect customer data and company systems, who is responsible, and how security
decisions are made. It is the parent policy — every other security policy in
this library sits under it.

## 2. Scope

This policy applies to all employees, contractors, and systems that store,
process, or transmit [Company Name] or customer data, including production
infrastructure, employee devices, and third-party services used to deliver
our product.

## 3. Policy statements

1. **Security is a business function, not an IT task.** The policy owner
   reports on the security program to [founder / leadership team] at least
   quarterly, covering open risks, incidents, and the status of planned
   controls.
2. **Least privilege by default.** Nobody — including founders and senior
   engineers — holds standing access beyond what their role requires.
   (See `02-access-control-policy.md`.)
3. **Defense in depth.** No single control is load-bearing. Access control,
   encryption, logging, and monitoring overlap so that one failure does not
   become a breach.
4. **Customer data is classified and handled by class.** (See
   `07-data-classification-and-retention-policy.md`.) Staff handle data only
   at the classification level their role permits.
5. **Security training is mandatory.** All staff complete security awareness
   training on hire and annually thereafter. Engineers with production access
   complete secure-development training annually. Completion is recorded.
6. **Incidents are reported, not hidden.** Any suspected security event is
   reported to [security contact / channel] immediately, without fear of
   blame for reporting. (See `04-incident-response-policy.md`.)
7. **Vendors are part of our security posture.** Any vendor that touches
   customer data is reviewed before adoption and on a recurring basis.
   (See `05-vendor-management-policy.md`.)
8. **Changes ship through review.** No change reaches production without
   review, testing proportionate to risk, and a rollback path. (See
   `06-change-management-policy.md`.)

## 4. Roles and responsibilities

| Role | Responsibility |
|---|---|
| [Founder / CEO] | Accountable for the security program and its resourcing |
| Policy owner | Maintains this policy, runs the quarterly security review |
| All staff | Follow this policy; report suspected incidents immediately |
| Engineering lead | Owns production access, change management, and logging |

## 5. Exceptions

Exceptions to this policy require written approval from the policy owner,
a stated expiry date (no more than 90 days), and a compensating control.
Expired exceptions are reviewed, not silently renewed.

## 6. Enforcement

Violations are addressed through [Company Name]'s disciplinary process, up to
and including termination of employment or contract. Suspected violations
involving customer data are escalated to the policy owner the same day.

## 7. Review

This policy is reviewed annually and after any material change to our
systems, vendors, or business, or after any security incident. Each review is
dated and recorded below.

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 8. Evidence this policy produces (Control IS-01)

An auditor will not ask whether this policy exists. They will ask for proof
it operates. Keep these on file, current, and findable within an hour:

| Evidence | Where it lives | Retention |
|---|---|---|
| Quarterly security review minutes (risks, incidents, control status) | [docs / drive location] | [3 years] |
| Security training completion records, all staff + engineers | [LMS / tracker] | Duration of employment + [1 year] |
| Policy approval signatures and version history | [docs location] | [3 years] |
| Exception log (approval, expiry, compensating control) | [tracker] | [3 years] |

## 9. Where startups fail this control

1. **The policy is approved but the training records do not exist.**
   Auditors test operation, not paper. A training requirement with no
   completion records is a finding, not a pass.
2. **"Quarterly review" with no minutes.** If the policy promises a
   quarterly review, the first thing sampled is the minutes. A cadence you
   cannot keep is worse than a slower cadence you hold — set it honestly.
3. **The founder holds standing admin everywhere.** The least-privilege
   statement applies to founders first. Auditors notice when the exception
   to your own rule is the person who wrote it.

---

*What this template does not do: it does not describe your actual systems,
vendors, or data flows, and it is not evidence that any of these statements
are practiced. Tailor it, approve it, and operate it — see
`TAILORING-GUIDE.md`.*
