# Vendor Management Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual; vendor reviews per §4 |
| **SOC 2 mapping** | CC9.2 (Risk Mitigation), CC6.1 (Logical Access) |

## 1. Purpose

Vendors that touch customer data are part of our security posture. This
policy ensures no vendor is adopted on convenience alone, and no vendor is
kept on inertia alone.

## 2. Scope

Any third-party service, contractor, or tool that stores, processes, or
transmits customer data, or that has access to production systems — including
free tiers. Internal tools with no customer-data access are out of scope but
should still be listed.

## 3. Vendor tiers

| Tier | Definition | Example |
|---|---|---|
| Critical | Holds or processes customer data, or can reach production | Cloud hosting, databases, analytics on customer data |
| Important | Touches internal data or supports delivery, limited customer data | Support tooling, CI/CD, error tracking |
| Low | No customer data, no production access | Marketing tools, internal docs |

Tier is set by the policy owner at adoption and reviewed when the vendor's
usage changes.

## 4. Adoption — before any customer data flows

1. **Register it.** The vendor is added to `tools/vendor-review-tracker.md`
   with tier, data accessed, owner, and contract status.
2. **Assess it.** Proportionate to tier:
   - Critical: current SOC 2 report, ISO 27001 certificate, or equivalent
     evidence reviewed and filed; security questionnaire completed or
     reviewed; DPA signed.
   - Important: security documentation reviewed; DPA signed where personal
     data is processed.
   - Low: basic review (reputation, terms, data handling) recorded.
3. **Approve it.** The policy owner approves adoption in writing. If required
   evidence is missing, adoption is conditional with a dated remediation
   plan — not silent acceptance.
4. **Limit it.** Access granted is the minimum the job requires, via SSO
   where available, with MFA enforced.

## 5. Ongoing review

| Tier | Review cadence | Review covers |
|---|---|---|
| Critical | Annual | Fresh SOC 2 / ISO evidence, breach history, data-access scope, contract + DPA currency |
| Important | Annual | Evidence currency, continued need, access scope |
| Low | Every 2 years | Continued need, any change in data handling |

Reviews are recorded in the tracker with reviewer, date, and outcome
(continue / remediate / offboard). A missed review is escalated to the
policy owner within [30 days].

## 6. Offboarding

When a vendor is no longer used: revoke its access and API keys, confirm
data return or deletion in writing, close the tracker row with an offboard
date, and retain the record per the retention policy. Offboarding is
completed within [30 days] of the decision to stop using the vendor.

## 7. Incidents involving vendors

A vendor breach or incident affecting our data is handled under the
incident response policy. The vendor owner notifies the policy owner the
same day the vendor's notice is received, and the tracker row records the
incident and its outcome.

## 8. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 9. Evidence this policy produces (Control VM-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Completed vendor-review tracker (every vendor, tier, review date, outcome) | [tracker location] | Current + [1 retention cycle] |
| Vendor security evidence on file (SOC 2 report, ISO certificate, questionnaire) | [vendor file] | Until superseded + [1 year] |
| Signed DPAs and contracts | [contract store] | Contract term + [1 year] |
| Offboarding confirmations (access revoked, data returned/deleted in writing) | [tracker offboarded section] | [1 retention cycle] |

## 10. Where startups fail this control

1. **The empty tracker, and the shadow vendors.** Free tiers, side tools,
   and "just testing it" services that touch customer data but never got a
   row. Auditors find them in expense reports and SSO logs — register
   every tool before it touches data, not after.
2. **Stale evidence treated as current.** A SOC 2 report from two years
   ago is not current evidence. Check the report's period end date, not
   just that a report exists — and record the date in the tracker.
3. **Offboarding with no confirmation.** The contract ended, the login
   still works, the data is still there. A vendor relationship is not
   closed until access revocation and data deletion are confirmed in
   writing.

---

*What this template does not do: it does not contain your vendor list —
that is the tracker, and an empty tracker is the most common gap auditors
find. Fill it in, review it on schedule, and the policy starts to mean
something.*
