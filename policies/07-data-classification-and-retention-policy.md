# Data Classification and Retention Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual |
| **SOC 2 mapping** | CC6.1, CC6.5 (Logical Access) |

## 1. Purpose

To ensure every piece of data is handled according to its sensitivity, and
kept only as long as it is needed — because data you do not hold cannot leak,
and data you cannot classify cannot be protected.

## 2. Data classes

| Class | Definition | Examples |
|---|---|---|
| Public | Disclosure causes no harm | Marketing site content, public docs |
| Internal | Disclosure would embarrass or disadvantage the company, but does not expose customers | Roadmaps, internal metrics, employee directories |
| Confidential | Disclosure would harm customers or breach obligations | Customer data, credentials, contracts, security assessments |
| Restricted | Disclosure would cause serious harm or legal exposure | Production secrets, encryption keys, unredacted personal data, credentials |

When in doubt, classify up, not down. The data owner decides the class; the
policy owner arbitrates disputes.

## 3. Handling rules by class

| Rule | Internal | Confidential | Restricted |
|---|---|---|---|
| Storage | Company systems only | Company systems only, encrypted at rest | Approved vaults/secrets manager only |
| Transmission | Company email/chat OK | Encrypted channels only | Encrypted channels + need-to-know approval |
| Sharing outside the company | With approval | With approval + NDA/DPA where required | Prohibited except through approved, logged channels |
| AI tools | Approved tools only | Approved tools only, and only where the tool's data handling is approved for that class | Prohibited in public AI tools, always |
| Devices | Screen lock required | Disk encryption required | Disk encryption + access logging required |

Public data has no handling restrictions beyond normal acceptable use.

## 4. Retention and disposal

| Data | Retain | Then |
|---|---|---|
| Customer production data | For the contract term + [90 days] | Delete or return per contract |
| Logs and audit trails | [1 year] minimum | Archive or delete per legal hold status |
| Backups | [90 days] rolling | Expire automatically |
| Employee records | Per [applicable law / HR policy] | Secure deletion |
| Security incident records | [3 years] | Archive |
| Financial records | Per [applicable law] | Secure deletion |

Deletion means deletion: from production, backups within their retention
window, and vendor systems (confirmed in writing). Data under legal hold is
never deleted until the hold is released in writing.

## 5. Personal data

Personal data is processed only for a stated purpose, minimized to what that
purpose requires, and handled under applicable privacy law and any DPA in
force. Data-subject requests (access, deletion, correction) are routed to
[privacy contact] and answered within the legally required window.

## 6. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 7. Evidence this policy produces (Control DC-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Data inventory with a class assigned to every store | [inventory location] | Current + prior versions [1 year] |
| Retention and deletion records (including backup-window expiry) | [ops docs] | Per retention schedule |
| Data-subject request log (request, response, date) | [privacy tracker] | [3 years] |
| Signed DPAs for every processor of personal data | [contract store] | Contract term + [1 year] |

## 8. Where startups fail this control

1. **Classes defined, nothing classified.** The four classes look great
   on paper and mean nothing until every data store carries one. The
   inventory exercise — list your stores, assign each a class — is the
   control; this document is just its rulebook.
2. **"Deleted" data living on in backups.** Deletion that covers
   production but not the backup window is not deletion. Your retention
   schedule must state how long backups hold deleted data, and that window
   must be defensible to a customer asking for erasure.
3. **Personal data hiding in logs and analytics.** The database is
   classified; the logs full of emails, the analytics events full of user
   IDs, are not. Auditors ask about the data you forgot, not the data you
   remembered.

---

*What this template does not do: it does not classify your actual data —
that exercise, done once with your team, is worth more than this document.
Sit down, list your data stores, assign each a class, and the handling rules
start enforcing themselves.*
