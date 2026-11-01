# Incident Response Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual, and after every incident; tabletop exercise at least annually |
| **SOC 2 mapping** | CC7.3, CC7.4 (System Operations) |

## 1. Purpose

To detect, contain, recover from, and learn from security incidents quickly
and consistently — so that a bad hour does not become a bad quarter, and so
that customers hear about incidents from us first.

## 2. Scope

All suspected or confirmed security events affecting company or customer
data, production systems, or third-party services used to deliver our
product. This includes suspected data exposure even when compromise is not
yet confirmed.

## 3. Definitions

| Term | Meaning |
|---|---|
| Event | Any observable occurrence (alert, report, anomaly) |
| Incident | An event confirmed or reasonably suspected to affect security or data |
| Severity 1 (Critical) | Customer data exposed or production unavailable with security impact |
| Severity 2 (High) | Credible threat to customer data or a major system, contained |
| Severity 3 (Low) | Isolated, contained, no customer-data impact |

## 4. Response phases

### Phase 1 — Detect and report (immediately)

Anyone who suspects an incident reports it to [security contact / channel]
immediately, by the fastest available means. Do not investigate alone first,
do not delete evidence, and do not notify customers before the incident
commander authorizes it. Good-faith reporting is protected.

### Phase 2 — Triage and declare (within 1 hour)

The incident commander [role / name] confirms whether an incident exists,
assigns severity, and opens an incident record with a timeline. Severity 1
incidents notify [founder / CEO] within 1 hour.

### Phase 3 — Contain

Stop the bleeding before finding the root cause: revoke compromised
credentials, isolate affected systems, block malicious sources, suspend
affected integrations. Containment actions and their times are logged in the
incident record. Do not destroy logs or forensic evidence during
containment.

### Phase 4 — Eradicate and recover

Remove the cause, restore affected systems from known-good state, rotate
exposed secrets, and verify monitoring is watching for recurrence before
returning to normal operations. Recovery is declared by the incident
commander, not by the system "looking fine."

### Phase 5 — Communicate

- **Internal:** status updates to leadership at least every [4 hours] during
  a Severity 1 incident.
- **Customers:** affected customers are notified by [role] within [72 hours]
  of confirmed impact, or sooner where law or contract requires, with what
  happened, what data was affected, and what we did. Never delay notification
  to complete the investigation if customers need to protect themselves.
- **Regulators / partners:** notified where law, contract, or a vendor
  agreement requires it, on the timeline that obligation sets.

### Phase 6 — Learn (within 14 days)

A written post-incident review covers: timeline, root cause, what worked,
what failed, and action items with owners and due dates. Action items are
tracked to completion. The review is shared with leadership and, in
anonymized form, used in security training.

## 5. Preparation

- An incident contact list (names, phones, out-of-band channel) is maintained
  and tested quarterly. It does not live only in the system that might be down.
- Backups are tested at least quarterly; a backup that has never been
  restored is assumed broken.
- A tabletop exercise is run at least annually, with a written record of
  participants, scenario, and lessons.

## 6. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 7. Evidence this policy produces (Control IR-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Incident records with timelines (every declared incident) | [ticketing system] | [3 years] |
| Post-incident reviews with action items tracked to completion | [docs / tracker] | [3 years] |
| Tabletop exercise record (participants, scenario, lessons) | [docs location] | [3 years] |
| Backup restore test records | [infra docs] | [1 year] |
| Customer notification records (who, when, what was said) | [support / CRM] | [3 years] |
| Incident contact list, tested quarterly | [out-of-band location] | Current version |

## 8. Where startups fail this control

1. **A plan that has never been tested.** An untested incident plan is a
   draft, not a control. The tabletop exercise is the cheapest evidence in
   this library — one hour, once a year — and its absence is a routine
   finding.
2. **The 72-hour notification clock with no definition of "confirmed."**
   If "confirmed impact" is undefined, the clock never starts on paper and
   always starts late in practice. Define who confirms impact, and the
   notification decision is theirs, same day.
3. **Post-incident actions tracked nowhere.** The review gets written, the
   action items live in someone's head, the same incident recurs. Auditors
   sample one incident and follow its action items to completion — or to
   the gap where they died.

---

*What this template does not do: it does not name your incident commander,
your alerting tools, or your notification templates, and it is not a tested
plan until you have run the tabletop. Fill in the names, run the exercise,
and file the record.*
