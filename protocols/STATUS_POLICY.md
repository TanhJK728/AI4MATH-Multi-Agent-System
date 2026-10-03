# Claim Status Policy

## What each status means

| Status | Meaning |
| --- | --- |
| `REAUDIT_PENDING` | A claim from another source is waiting for review. |
| `OPEN` | A question is clear, but a complete claim has not yet been stated. |
| `CONJECTURED` | The statement, definitions, assumptions, quantifiers, and supporting claims are explicit. |
| `COMPUTATIONALLY_SUPPORTED` | Reproducible finite checks support the claim within the checked range. |
| `PROVED_PENDING_AUDIT` | A complete written proof is available, but independent review is unfinished. |
| `ESTABLISHED` | The independent review, checks of supporting claims, applicable attempts to find counterexamples, and checks of outside theorems have passed. Director has recorded acceptance. |
| `REFUTED` | A valid counterexample or contradiction defeats the stated claim. |

`ESTABLISHED` means the claim passed this review process. It does not mean the
proof was checked by a proof assistant or that the reviewers cannot be wrong.
Finite checks support only the range and cases actually checked.

## Allowed status changes

These changes apply while the mathematical statement stays the same. A new
statement version starts a new review as described below; it does not rewrite
the status history of the earlier version.

```text
REAUDIT_PENDING -> OPEN | CONJECTURED | PROVED_PENDING_AUDIT | REFUTED
OPEN -> CONJECTURED | REFUTED
CONJECTURED -> COMPUTATIONALLY_SUPPORTED | PROVED_PENDING_AUDIT | REFUTED
COMPUTATIONALLY_SUPPORTED -> PROVED_PENDING_AUDIT | REFUTED
PROVED_PENDING_AUDIT -> ESTABLISHED | CONJECTURED | REFUTED
ESTABLISHED -> CONJECTURED | REFUTED
REFUTED -> no transition
```

If an accepted claim loses that status, review what went wrong and whether a
substantial change needs a human decision. A repaired claim gets a new identifier;
the refuted claim keeps its status and remains unchanged.

## Before a claim can be accepted

No agent may approve its own result. To mark a claim `ESTABLISHED`, all of the
following are required:

1. A saved, unchanged copy of the exact statement and its content hash.
2. Recorded definitions and explicit assumptions.
3. A complete written proof.
4. An independent Verifier report reviewing the same statement.
5. Acceptance of every supporting claim on which the proof depends.
6. Applicable attempts to find counterexamples through computation.
7. Exact citations for outside theorems and an explanation of how their
   assumptions match the present use.
8. Resolution of any substantial decision affecting the claim.
9. Director's written decision and reasons.

## When the statement changes

A mathematical change increases `statement_version`. Changes to quantifiers,
allowed objects, the way observations are defined, the domain, or the conclusion
normally return the claim to `CONJECTURED` and may require a human decision.
In particular, a new version cannot inherit `COMPUTATIONALLY_SUPPORTED` from
checks of the old statement. A refuted claim always needs a new identifier for
its repair, rather than a status reset on the refuted record.
Wording changes that leave the mathematics unchanged do not change the version.

## Refutation and repair

A counterexample must satisfy every assumption of the claim it refutes. Keep the
refuted record unchanged. Give a repaired claim a new identifier or a child
identifier, and link it to the earlier record using `supersedes`.
