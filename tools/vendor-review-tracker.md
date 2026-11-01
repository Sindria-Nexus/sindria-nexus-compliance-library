# Vendor Review Tracker

Track every vendor that touches your data or your production systems. One row
per vendor. A vendor with no row is a vendor you cannot defend.

**How to use it:** copy this file, fill in one row per vendor, and review on
the cadence in `policies/05-vendor-management-policy.md` (Critical and
Important annually, Low every 2 years). A review is not done until the
Reviewer and Review date columns are filled.

## Tracker

| Vendor | Tier (Critical / Important / Low) | What it does | Data it touches | Owner (your side) | Contract / DPA signed? | Security evidence on file (SOC 2 / ISO 27001 / questionnaire + date) | Last review | Next review due | Reviewer | Outcome (Continue / Remediate / Offboard) | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| [Example: Acme Cloud] | Critical | Production hosting | Customer data, all classes | [Name] | Yes / [date] | SOC 2 Type II, [date] | [YYYY-MM-DD] | [YYYY-MM-DD] | [Name] | Continue | |
| | | | | | | | | | | | |
| | | | | | | | | | | | |
| | | | | | | | | | | | |

## Offboarded vendors

Keep offboarded vendors here for one retention cycle — an auditor will ask
what you used to use, and "we deleted the list" is not an answer.

| Vendor | Tier | Offboard date | Access revoked? | Data returned / deleted confirmed? | Confirmed by |
|---|---|---|---|---|---|
| | | | | | |

## Evidence freshness rule

A SOC 2 report is evidence for the **period it covers**, not forever.
When you file vendor evidence, record the report's period end date — a
report whose period ended two years ago is stale, even if the vendor still
links it on their trust page. If the evidence is older than 12 months,
ask the vendor for the current report before marking the review complete.

## Vendor has no SOC 2? Ask for this instead

Many AI vendors — especially the newest ones — have no SOC 2 report yet.
That is not an automatic disqualification, but it is not a free pass
either. For a Critical vendor without a report, collect all of these
before approving, and record them in the Notes column:

- [ ] Completed security questionnaire (theirs or yours)
- [ ] Most recent penetration test summary, with critical/high findings
      and their remediation status
- [ ] Signed DPA, including subprocessor terms
- [ ] Breach and incident history for the last 24 months
- [ ] Written commitment: SOC 2 report or equivalent evidence by [date],
      with the review re-opened if that date slips

If the vendor will not provide any of the above, that is itself the
assessment — and the honest outcome is Remediate (find an alternative or
isolate the vendor's data access) rather than a quiet Continue.

## Review checklist (per vendor)

- [ ] Is the tier still right for what this vendor actually touches today?
- [ ] Is the security evidence current (not expired, not from two years ago)?
- [ ] Has the vendor had a breach or incident since the last review? If yes,
      is it recorded in the Notes column with the outcome?
- [ ] Is the access scope still the minimum the job requires?
- [ ] Is the contract / DPA still signed and current?
- [ ] Do we still need this vendor at all?

## Overdue reviews

Any review past its due date is escalated to the policy owner within 30 days
and stays visible here until completed:

| Vendor | Due date | Days overdue | Escalated to | Status |
|---|---|---|---|---|
| | | | | |
