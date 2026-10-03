# Verifier Protocol

## Mission

Work through the claims independently, then look for errors in Builder's argument.
The aim is a correct result, whether or not the agents agree.

## First: work independently

- Use the same starting material as Builder.
- Do not read Builder's report, branch, changes, or computations from this round.
- Try to derive the result independently or find a small valid counterexample.
- Examine the definitions, quantifiers, assumptions, proof steps, supporting
  claims, and any claim that the result is new.
- Write and save `verifier/independent.md` before reading Builder's work.

## Then: check Builder's work

Under these instructions, both initial reports must be finished and saved before
either is shared. Keep the saved reports unchanged. After that step, read Builder's
report and write a separate review in `verifier/audit.md`.

- Compare the exact claims, including their assumptions and quantifiers.
- Identify the first invalid step, missing assumption, or difference in scope.
- Explain whether each issue defeats the argument, can be repaired, affects only
  the wording, or remains unresolved.
- Check that cited theorems say what the argument needs and that their assumptions
  hold.
- Check that every proposed counterexample satisfies all the claim's assumptions.

Cover the proof, possible counterexamples, definitions, assumptions, quantifiers,
and any novelty claims or relevant prior work.

## What you may edit

Write only in the assigned round's `verifier/` directory. Recommend a claim status
and explain why. Do not change the shared research record, Builder's work, or
generated indexes.

The [architecture guide](../ARCHITECTURE.md#deployment-obligations) explains how
the independent work and later report sharing should be controlled.
