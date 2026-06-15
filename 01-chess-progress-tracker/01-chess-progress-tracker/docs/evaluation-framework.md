# Finding Evaluation Framework

## Executive Summary

This framework was created during validation of Supporting Assumption #1:

> AI can extract factually correct findings from chess PGNs.

The framework separates two independent questions:

1. Does the evidence package support the finding?
2. Is the finding actually correct?

A finding may be:

* Correct and well supported
* Correct but poorly supported
* Incorrect despite plausible evidence
* Incorrect and poorly supported

The framework was developed after discovering that finding correctness and evidence traceability are separate quality dimensions and should be evaluated independently.

---

## Objective

The purpose of this framework is to independently evaluate:

1. Whether the evidence provided by the analysis supports the finding.
2. Whether the finding is actually correct when validated against the complete game record.

These assessments must be performed independently.

A finding should not be assumed correct because the explanation appears convincing.

A finding should not be assumed incorrect because the evidence is incomplete.

---

## Evaluation Workflow

For each finding:

1. Decompose the finding into explicit claims.
2. Verify each claim against all components of the evidence package.
3. If evidence is insufficient, analyze the complete PGN.
4. Resolve subjective terminology using operational definitions.
5. Produce independent assessments for evidence quality and finding correctness.

---

## Step 1: Decompose the Finding into Explicit Claims

Break the finding into the minimum set of explicit claims required for the finding to be true.

Evaluate each claim independently.

### Definition Check

For any claim containing a chess-specific term:

* Passed pawn
* Hanging piece
* Fork
* Discovered attack
* Overloaded piece

State the definition of the term before evaluating the claim.

Evidence must establish the definition itself, not merely a consequence of the definition.

### Evaluation Principle

A finding is fully supported only when all explicit claims are supported.

If one or more claims fail, document which claims failed and why.

---

## Step 2: Evidence Verification

Determine whether the evidence package supports each explicit claim.

The evidence package consists of:

* Key Moves
* Verification Explanation

Both are valid sources of evidence.

### Required Evidence Processing Sequence

For each claim:

**Step 2a**

What does the Key Moves notation establish?

**Step 2b**

What does the Verification Explanation establish?

**Step 2c**

What is the final Evidence Verification outcome after considering both?

Both components must be processed before assigning an outcome.

### Evidentiary Sufficiency Rule

Either component alone is sufficient to verify a claim.

If the Verification Explanation directly establishes a claim, the claim is considered Verified even if the Key Moves notation does not independently establish it.

### Anti-Discounting Rule

Do not downgrade a Verified claim simply because another evidence component provides weaker support.

### Anti-Substitution Rule

A consequence of a claim is not proof of the claim itself.

Example:

Incorrect:

> The pawn was unstoppable, therefore it was a passed pawn.

Correct:

The evidence must establish the formal definition of a passed pawn.

---

## Evidence Verification Outcomes

| Outcome    | Definition                                       |
| ---------- | ------------------------------------------------ |
| Verified   | Evidence directly supports the claim             |
| Partial    | Evidence supports only part of the claim         |
| Unverified | Evidence is insufficient                         |
| Incorrect  | Evidence contains a demonstrably false assertion |

### Evaluation Principle

Evidence Verification evaluates the quality of support provided by the analysis.

It does not determine whether the finding is actually correct.

---

## Step 3: Escalation Decision

Escalate to PGN analysis only if at least one claim is:

* Partial
* Unverified
* Incorrect

### Do Not Escalate

If all claims are Verified:

* Evidence Verification = Verified
* Finding Validation = Correct

Stop evaluation.

### Evaluation Principle

Finding Validation exists to resolve uncertainty.

Additional analysis should not be performed when evidence is already conclusive.

---

## Validation Prerequisite

A finding may be classified as Correct or Incorrect only when one of the following conditions has been satisfied:

### Condition A

The evidence package conclusively establishes all claims.

### Condition B

The complete PGN has been analyzed and establishes ground truth for unresolved claims.

If neither condition is satisfied, correctness cannot be determined.

### Evaluation Principle

Verification requires evidence.

Plausibility is not evidence.

---

## When PGN Is Required but Unavailable

If:

* One or more claims remain unresolved
* PGN analysis is required
* The complete PGN is unavailable

Then:

**Finding Validation = Deferred**

Example:

> Deferred — PGN required to verify piece identity on f5 at move 12.

### Anti-Inference Rule

When information is missing:

* Do not infer likely conclusions.
* Do not assume piece positions.
* Do not treat a coherent narrative as confirmation.

Surface the missing information and stop.

---

## Step 4: Resolve Subjective Terminology

Some findings contain interpretation-dependent terms such as:

* Achieved nothing
* Played no further role
* Active piece
* Passive piece
* Unsafe king position

### Rule

Do not evaluate such terms using personal interpretation.

Instead:

1. Check whether an operational definition exists.
2. Request a definition if none exists.
3. Evaluate against the agreed definition.

### Evaluation Principle

Consistency is more important than conventional interpretation.

---

## Final Output

Produce two independent assessments.

### Evidence Verification

Question:

> Does the evidence package support the finding?

Possible outputs:

* Verified
* Partial
* Unverified
* Incorrect

### Finding Validation

Question:

> Is the finding actually correct?

Possible outputs:

* Correct
* Incorrect
* Deferred — PGN required

---

## Guiding Principles

1. Evaluate claims, not narratives.
2. Validate evidence, not conclusions.
3. Separate evidence quality from finding correctness.
4. Define chess-specific terminology before evaluation.
5. Do not treat consequences as proof.
6. Process all evidence components before assigning a verdict.
7. Stop when evidence is conclusive.
8. Do not infer when information is missing.
