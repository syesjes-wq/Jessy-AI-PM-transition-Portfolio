# Evaluation Framework Failure Log

## Executive Summary

During implementation of the Finding Evaluation Framework, multiple evaluator failure modes were discovered while reviewing AI-generated chess findings.

These failures did not primarily reflect weaknesses in chess reasoning. Instead, they exposed weaknesses in evaluation workflow design, evidence processing, scope control, and decision logic.

Each failure resulted in modifications to the evaluation framework and additional evaluator guardrails.

The most significant outcome was the realization that building an evaluation system requires governing how an evaluator reasons, not just defining what correctness means.

---

## Failure #1: Evidence-to-Claim Conversion

### Frequency

Observed in **8 of 36 evaluated findings (22%)**.

### Description

The evaluator introduced claims that were not explicitly present in the finding.

Instead of extracting claims from the finding itself, the evaluator promoted details from supporting evidence into evaluation targets.

Examples included:

* Board locations promoted into claims
* Move sequences promoted into claims
* Verification details promoted into claims

Example:

**Finding**

> King became exposed in the center after queenside castling.

**Incorrect Claim Added**

> King ended up on c8.

The added claim originated from supporting evidence rather than the finding.

### Root Cause

The evaluator blurred the distinction between:

* Claims being evaluated
* Evidence used to evaluate those claims

Evidence details were incorrectly promoted into evaluation targets.

### Framework Improvement

**Claim Extraction Rule**

Claims must be extracted exclusively from the wording of the finding.

Claims may not be extracted from:

* Key Moves
* Verification Explanations
* Chess knowledge
* Evaluator inference

### Key Learning

Evaluation quality depends as much on controlling evaluation scope as on assessing correctness.

Without explicit scope controls, evaluators naturally expand the evaluation target using context, explanations, and domain knowledge.

---

## Failure #2: Cognitive Closure Bias

### Description

When evidence formed a plausible narrative but did not conclusively establish a claim, the evaluator inferred the missing step and treated the conclusion as verified.

Example:

**Evidence**

* 8...Qf5
* 12.gxf5

**Evaluator Conclusion**

> Queen was captured by a pawn.

The evidence package did not establish that the queen remained on f5 until move 12.

The evaluator completed the narrative without performing the PGN analysis required by the framework.

### Root Cause

**Cognitive Closure Bias**

The tendency to replace unresolved uncertainty with the most plausible explanation.

### Framework Improvement

If evidence is insufficient and PGN analysis cannot be performed, evaluation must stop until the required game record is available.

### Key Learning

The evaluator's responsibility is verification, not inference.

---

## Failure #3: Missing Exit Condition

### Description

The evaluator continued to later evaluation stages even after all claims had already been verified.

Observed pattern:

Claim Decomposition

↓

Evidence Verification

↓

All Claims Verified

↓

PGN Analysis Executed Anyway

The final conclusion remained correct, but the workflow violated the intended protocol.

### Root Cause

The framework defined escalation conditions but did not define termination conditions.

The evaluator interpreted PGN analysis as a mandatory validation step rather than a conditional escalation step.

### Framework Improvement

**Escalation Decision Rule**

If all claims are verified:

* Evidence Verification = Verified
* Finding Validation = Correct

STOP

Do not proceed to PGN analysis.

### Key Learning

Evaluation systems require both escalation conditions and termination conditions.

Without explicit stopping criteria, evaluators tend to over-validate, increasing cost and complexity without improving accuracy.

---

## Failure #4: Evidence Hierarchy Bias

### Description

The evaluator treated move notation as primary evidence and verification explanations as secondary commentary.

As a result, valid evidence contained within explanations was ignored or discounted.

Observed pattern:

Key Moves Reviewed

↓

Evidence Appears Insufficient

↓

Verdict Assigned

↓

Verification Explanation Not Incorporated

### Root Cause

The evaluator implicitly assigned higher evidentiary weight to move notation than to verification explanations.

### Framework Improvement

Structured evidence review:

1. What do the Key Moves establish?
2. What does the Verification Explanation establish?
3. Combine both sources.
4. Assign the verdict.

Evidence Verification cannot be completed until both evidence sources have been reviewed.

### Key Learning

Evaluation failures are not always caused by missing information.

Sometimes the information exists but is not processed consistently.

---

## Failure #5: Corroboration Bias

### Description

The evaluator required multiple evidence sources to independently establish a claim before assigning a Verified outcome.

Observed pattern:

Key Moves = Partial

Verification Explanation = Verified

↓

Combined Result = Partial

Instead of:

Key Moves = Partial

Verification Explanation = Verified

↓

Combined Result = Verified

### Root Cause

The evaluator incorrectly treated the Verification Explanation as evidence that required independent corroboration from the Key Moves.

### Framework Improvement

**Evidentiary Sufficiency Rule**

Either component of the evidence package may independently verify a claim.

Claims do not require corroboration across evidence sources.

### Key Learning

Evidence sources should be treated as additive rather than corroborative.

The goal is to determine whether the evidence package establishes the claim, not whether every evidence source independently proves the same fact.

---

## Failure #6: Concept Definition Failure

### Description

The evaluator verified chess concepts using their consequences rather than their definitions.

Example:

**Claim**

> The pawn was a passed pawn.

**Evidence**

> White could not stop the pawn's advance.

The evaluator treated an unstoppable pawn as evidence of a passed pawn.

### Root Cause

The evaluator relied on semantic association rather than verifying the conditions required by the concept definition.

This reversed the logical relationship between a concept and one of its common consequences.

### Framework Improvement

**Definition-First Evaluation**

For any chess-specific concept:

1. State the definition.
2. Identify the required conditions.
3. Evaluate evidence against those conditions.

Evidence that establishes a consequence does not establish the concept itself.

### Key Learning

Domain-specific concepts must be verified against their definitions rather than their typical outcomes.

Evidence that makes a claim plausible is not the same as evidence that proves the claim.

---

## Overall Learning

The primary lesson from framework development was that evaluation quality depends not only on the correctness criteria being applied, but also on the rules governing evaluator behavior.

Many observed failures occurred even when the evaluator possessed sufficient information to reach the correct conclusion.

The failures emerged from:

* Scope expansion
* Premature inference
* Missing decision gates
* Inconsistent evidence processing
* Incorrect evidentiary standards
* Undefined concept boundaries

The resulting framework evolved from a simple correctness-checking process into a governed evaluation system with explicit controls over claim extraction, evidence processing, escalation, and verification.

This proved critical to achieving consistent and repeatable evaluation outcomes.
