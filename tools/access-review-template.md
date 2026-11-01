# Access Review Template

Run this quarterly. The reviewer must be someone other than the person whose
access is being reviewed. Every decision is signed and dated — this signed
record is the evidence auditors ask for.

**Review period:** [Q_ YYYY] — from [YYYY-MM-DD] to [YYYY-MM-DD]
**Reviewer:** [Name, Title]
**Approved by:** [Name, Title]

## Instructions

1. Export the current user list from every in-scope system (production,
   cloud, repositories, and any third-party service holding customer data).
2. For each person, confirm: still employed / contracted, still in the same
   role, and still needs each access listed.
3. Mark each row Keep or Remove. Removals are actioned within [5 business
   days] and the action date is recorded.
4. Pay special attention to: privileged accounts, break-glass accounts,
   service accounts and API keys, and anyone who changed roles or left
   since the last review.
5. The reviewer and approver sign at the bottom. File the completed review
   where audit evidence lives.

## Review table

| Person | Role | System | Access level / role | Still required? (Yes / No) | Decision (Keep / Remove) | Removal actioned (date) | Notes |
|---|---|---|---|---|---|---|---|
| [Example: A. Lee] | Backend engineer | Production cloud | Admin | Yes | Keep | — | |
| [Example: A. Lee] | Backend engineer | Old analytics tool | Admin | No — no longer used | Remove | [YYYY-MM-DD] | Account deleted |
| | | | | | | | |
| | | | | | | | |
| | | | | | | | |

## Service accounts and API keys

| Account / key name | System | Purpose | Owner | Last rotated | Rotation due | Decision (Keep / Rotate / Delete) | Notes |
|---|---|---|---|---|---|---|---|
| | | | | | | | |
| | | | | | | | |

## Break-glass accounts

| Account | System | Last used | Use justified and reviewed? | Decision |
|---|---|---|---|---|
| | | | | |

## Leavers and movers since last review

| Person | Change (left / role changed) | Date | Old access revoked? (date) | New access granted? (date) | Verified by |
|---|---|---|---|---|---|
| | | | | | |

## Reviewer independence attestation

By signing below, the reviewer attests they did **not** review their own
access in this review, and that every Keep/Remove decision was made on the
evidence of current role and need — not on familiarity or convenience.
This attestation is the part auditors sample first: a review signed by the
person whose access it covers is not a review.

## Sign-off

| | Name | Signature | Date |
|---|---|---|---|
| Reviewer | | | |
| Approver | | | |

**Summary:** [ ] accounts reviewed · [ ] removals actioned · [ ] privileged
accounts reviewed · [ ] break-glass accounts reviewed · [ ] leavers/movers
verified
