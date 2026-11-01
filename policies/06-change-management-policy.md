# Change Management Policy

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title] |
| **Approver** | [Name, Title] |
| **Effective date** | [YYYY-MM-DD] |
| **Review cadence** | Annual |
| **SOC 2 mapping** | CC8.1 (Change Management) |

## 1. Purpose

To ship changes quickly without shipping surprises — every production change
is reviewed, tested proportionate to its risk, deployable, and reversible.

## 2. Scope

All changes to production systems, infrastructure, configuration, and
data-handling processes, including vendor configuration changes that affect
customer data.

## 3. Policy statements

1. **No direct production edits.** All changes go through [version control /
   deployment pipeline]. Direct database edits, console changes, and hotfixes
   outside the pipeline are prohibited except under the emergency process
   (§5), and are reviewed the next business day.
2. **Every change is reviewed.** A pull request or change record is reviewed
   and approved by someone other than the author before deployment. The
   author cannot approve their own change.
3. **Risk-proportionate testing.** Changes are tested before deployment:
   automated tests for code, and a staging check for infrastructure and
   configuration changes. Test evidence is attached to the change record.
4. **Segregation of duties.** The person who deploys a change to production
   is not the sole reviewer of that change. In a team of one, the review
   record must show an independent check — a second person, or a documented
   self-review checklist completed before deployment, never after.
5. **Every change is reversible.** Deployments have a rollback plan recorded
   before they ship: previous version, restore procedure, and who can
   trigger the rollback.
6. **Every change is logged.** The deployment log records what changed,
   who approved it, when it shipped, and the rollback outcome if used.
   Logs are retained per the retention policy.
7. **Access to deploy is controlled.** Production deployment rights follow
   the access control policy and are reviewed in the quarterly access
   review.

## 4. Change types

| Type | Definition | Approval |
|---|---|---|
| Standard | Routine, pre-approved pattern (dependency update, config change within approved bounds) | Pipeline checks + peer review |
| Normal | Feature, migration, or infrastructure change | Peer review + owner approval |
| Emergency | Required to restore service or stop an active incident | Incident commander approval, retrospective review within [2 business days] |

## 5. Emergency changes

Emergency changes may bypass normal review to restore service or contain an
incident, but they must still be logged, and they are reviewed within
[2 business days] by someone other than the author. The review record states
whether the change stays, is reverted, or is replaced by a normal change.

## 6. Failed changes

A failed deployment is rolled back, not patched forward in production
without a new reviewed change. The failure and rollback are recorded in the
deployment log and, where customer impact occurred, in the incident record.

## 7. Review

| Version | Date | Author | Change |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial adoption |

## 8. Evidence this policy produces (Control CM-01)

| Evidence | Where it lives | Retention |
|---|---|---|
| Pull requests with reviewer approval (author ≠ approver) | [version control] | [1 year] |
| Deployment log (what, approver, when, rollback outcome) | [deployment system] | [1 year] |
| Emergency change retrospective reviews (within 2 business days) | [ticketing / docs] | [1 year] |
| Failed deployment and rollback records | [deployment log] | [1 year] |

## 9. Where startups fail this control

1. **The author approved their own change.** In a team of one this is the
   whole game: auditors look for the independent check. The documented
   self-review checklist, completed *before* deployment, is what makes a
   solo-founder pipeline defensible — a checklist filled in after the fact
   is not.
2. **Emergency changes never retrospectively reviewed.** The emergency
   process is legitimate; the skipped retrospective is the finding. Every
   emergency change needs its 2-day review, even when it worked perfectly.
3. **"Just this once" direct production edits.** One undocumented console
   change breaks the story that all changes flow through the pipeline.
   Auditors sample the deployment log against production — gaps are
   visible.

---

*What this template does not do: it does not name your pipeline, your
reviewers, or your rollback tooling — and it is not evidence until your
pull requests and deployment logs show the reviews actually happened. Your
git history is your evidence; keep it clean.*
