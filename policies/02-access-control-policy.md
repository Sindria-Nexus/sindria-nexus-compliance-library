# Access Control Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Quarterly access review; policy review annually |
| **SOC 2 mapping** | CC6.1, CC6.2, CC6.3, CC6.6 (Logical Access) |

## 1. Purpose

To ensure only authorized people can reach company and customer data, and that
every grant of access can be traced to a person, a role, and an approval.

## 2. Scope

All accounts on production systems, cloud infrastructure, code repositories,
and any third-party service that stores or processes customer data. This
includes human accounts, service accounts, and API keys.

## 3. Policy statements

### Accounts

1. Every person gets one unique account per system. Shared accounts are
   prohibited, except for break-glass emergency accounts (see §6), which are
   sealed, logged, and reviewed after every use.
2. Accounts are provisioned only from an approved request: a ticket or
   onboarding record naming the person, the system, the role, and the
   approver. Verbal grants are not access control.
3. Access follows the role, not the person. When someone changes roles, old
   access is revoked and new access is granted — the two actions are
   separate tickets, and neither is skipped.

### Authentication

4. Multi-factor authentication (MFA) is required for all production, cloud,
   repository, and administrative access. No exceptions for seniority.
5. Passwords must be at least [14] characters and unique per system. A
   company-provided password manager is required for storing credentials;
   credentials in chat, email, docs, or code are a reportable incident.
6. Sessions time out after [15 minutes] of inactivity on administrative
   consoles, and [30 days] maximum on workforce SSO sessions.

### Least privilege

7. Standing administrative access is minimized. Day-to-day work uses
   standard accounts; elevated access is requested, time-boxed, and logged.
8. Production data access is restricted to roles that require it. Engineers
   debug with anonymized or synthetic data wherever possible; direct
   production database access requires approval and is logged.
9. Service accounts and API keys hold the minimum scope their job requires,
   are stored in [secrets manager], and are rotated at least every [90 days]
   and immediately on suspected exposure or staff departure.

### Joiner / mover / leaver

10. **Joiner:** access is granted only after identity verification and the
    approved onboarding ticket. No access before day one.
11. **Mover:** role changes trigger an access review within [5 business
    days]. Access tied to the old role is revoked even if the person "might
    still need it."
12. **Leaver:** all access is revoked on the last working day, and within
    [1 hour] for involuntary departures or suspected compromise. The leaver
    checklist is signed by [IT / engineering lead] and filed.

### Reviews

13. Access is reviewed quarterly using `tools/access-review-template.md`.
    The reviewer is someone other than the person whose access is being
    reviewed, and every removal or retention decision is signed and dated.
14. Privileged and break-glass accounts are reviewed monthly.

## 4. Break-glass accounts

Emergency accounts exist for [list systems]. They are sealed in [secrets
manager], their use triggers an immediate alert to [security contact], and
every use is reviewed within [1 business day] with a written justification.

## 5. Enforcement

Unauthorized access attempts are logged and reviewed. Sharing credentials,
circumventing MFA, or granting unapproved access is grounds for disciplinary
action up to termination.

## 6. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 7. Evidence this policy produces (Control AC-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Onboarding tickets (person, system, role, approver) | [ticketing system] | Duration of employment + [1 year] |
| MFA enrollment report (all in-scope systems, 100% enrolled) | [IdP report] | [1 year] |
| Quarterly access reviews, signed and dated | [evidence location] | [1 year] minimum |
| Leaver checklists with revocation timestamps | [ticketing / HR system] | Duration of employment + [1 year] |
| Break-glass use log with post-use justifications | [secrets manager / log] | [1 year] |
| Service account and API key rotation log | [secrets manager] | [1 year] |

## 8. Where startups fail this control

1. **The reviewer reviewed their own access.** The most common access
   finding. The reviewer must be someone other than the person whose access
   is on the row — in a tiny team, that means founders review each other,
   never themselves.
2. **Leaver access revoked days or weeks late.** Auditors sample leavers
   and compare last working day to revocation timestamp. "We got around to
   it" is a failed control, even if nothing bad happened.
3. **Service accounts owned by nobody, rotated never.** API keys created
   by departed staff, with no owner and no rotation date, are a standing
   finding. Every key needs an owner and a rotation due date — the review
   template has columns for both.

---

*What this template does not do: it does not list your actual systems,
roles, or approvers, and a written policy is not the review record. Run the
quarterly review, keep the signed template, and that record becomes your
evidence.*
