# Assumption #1 Feasibility Analysis

## Executive Summary

| Item                  | Result                                                    |
| --------------------- | --------------------------------------------------------- |
| Assumption            | AI can extract factually correct findings from chess PGNs |
| Dataset               | 9 beginner-level chess games                              |
| Findings Evaluated    | 47                                                        |
| Correct Findings      | 38                                                        |
| Incorrect Findings    | 5                                                         |
| Unverifiable Findings | 4                                                         |
| Accuracy              | 80.9%                                                     |
| Success Threshold     | 70%                                                       |
| Outcome               | Validated                                                 |

**Conclusion:** The experiment achieved 80.9% accuracy, exceeding the predefined feasibility threshold of 70%. This provides strong evidence that AI can extract factually correct findings from individual chess PGNs and supports proceeding to validation of the next product assumption.

---

## Assumption Under Validation

**Supporting Assumption #1**

> AI can extract factually correct findings from chess PGNs.

This assumption forms the foundation of the Chess Progress Tracker workflow:

**PGNs → Findings → Concepts → Parent Insights**

If findings cannot be extracted accurately, concept mapping and insight generation cannot be meaningfully validated.

---

## Objective

The objective of this feasibility analysis is to determine whether AI can:

* Identify valid findings from chess PGNs
* Support findings with observable evidence
* Produce findings that can be independently verified

The purpose of this analysis is to establish whether AI can reliably perform the first layer of reasoning required by the product.

---

## Initial Investigation

Before validating AI-generated findings, a benchmark was required to determine whether findings were factually correct.

The initial investigation focused on Stockfish as a potential benchmark.

Stockfish provides metrics such as:

* Inaccuracies
* Mistakes
* Blunders
* Average Centipawn Loss
* Accuracy

These metrics appeared most relevant to blunder identification.

However, the investigation revealed an important mismatch:

* The product requires parent-facing learning patterns and recurring findings.
* Stockfish primarily provides move-level annotations.

For example:

**Product finding**

> Lost a bishop due to leaving pieces undefended in multiple games.

**Stockfish output**

> Move 14: Blunder

While Stockfish provides evidence that a mistake occurred, it does not directly provide the type of finding required by the product.

This raised concerns about whether Stockfish could serve as a benchmark for evaluating finding correctness.

---

## Key Discovery

The investigation revealed that finding correctness could not be evaluated until a clear definition of a valid finding and its supporting evidence had been established.

Without this bridge, it was impossible to determine whether an AI-generated finding was correct, regardless of whether the benchmark was:

* Stockfish
* A chess coach
* Chess learning material

This led to the creation of a finding taxonomy and evaluation framework before proceeding with experimentation.

---

## Finding Taxonomy

A finding taxonomy was created using beginner-focused chess learning material.

The taxonomy serves as an evaluation artifact and is not used as an input to the AI.

The taxonomy defines:

* Valid findings
* Observable criteria supporting each finding
* Consequences of the finding
* Traceability between findings and game evidence

Each taxonomy entry contains:

| Field               | Description                              |
| ------------------- | ---------------------------------------- |
| Category            | Type of mistake or learning pattern      |
| Finding             | Recurring chess pattern being identified |
| Observable Criteria | Evidence required for validation         |
| Consequence         | Likely impact on the position or game    |

The taxonomy intentionally focuses on beginner-level concepts that are observable, traceable, and understandable to parents.

---

## Finding Evaluation Framework

The objective of the evaluation framework is to determine whether AI-generated findings are factually correct.

For each PGN:

1. Generate findings and supporting evidence.
2. Review the finding and evidence.
3. Verify whether the evidence supports the claim.
4. Classify the finding.

### Evaluation Definitions

| Classification | Definition                                                    |
| -------------- | ------------------------------------------------------------- |
| Correct        | Supported by observable evidence and independently verifiable |
| Incorrect      | Not supported by the evidence                                 |
| Unverifiable   | Cannot be verified from the evidence provided                 |

The framework was designed to provide a consistent method for evaluating finding correctness.

---

## Experiment Design

### Scope

The experiment focused on single-game finding extraction.

Multi-game aggregation was intentionally excluded and will be evaluated separately after single-game extraction has been validated.

### Dataset

9 beginner-level chess PGNs.

The dataset included games likely to contain:

* Opening mistakes
* Tactical blunders
* Middlegame mistakes
* Endgame mistakes

### Process

For each PGN:

1. Provide the PGN to the AI.
2. Generate findings and supporting evidence.
3. Record the output.
4. Evaluate each finding using the Finding Evaluation Framework.

---

## Success Criteria

The assumption would be considered validated if at least 70% of generated finding-evidence pairs were determined to be factually correct.

| Accuracy | Interpretation                           |
| -------- | ---------------------------------------- |
| >80%     | Strong evidence capability exists        |
| 70–80%   | Moderate evidence capability exists      |
| <70%     | Capability not sufficiently demonstrated |

The objective of the experiment was feasibility validation rather than production readiness.

---

## Results

| Outcome      | Count |
| ------------ | ----- |
| Correct      | 38    |
| Incorrect    | 5     |
| Unverifiable | 4     |

**Finding Accuracy = 38 / 47 = 80.9%**

The observed accuracy exceeded the predefined feasibility threshold of 70% and falls within the category:

> Strong evidence capability exists

---

## Key Learnings

The experiment revealed an important distinction between **finding correctness** and **evidence traceability**.

Although 38 findings (80.9%) were ultimately determined to be factually correct, 18 findings (38.3%) could not be fully verified from the evidence package alone and required escalation to full PGN analysis.

Several recurring evaluation challenges were observed:

* Chess-specific concepts whose definitions were not directly established by the evidence
* Causal statements where the evidence established correlation but not causation
* Subjective terminology requiring operational definitions before evaluation
* Findings where the conclusion was correct but the supplied evidence did not fully support every explicit claim

Most failures were evidence-traceability failures rather than chess-reasoning failures.

In many cases, the AI reached the correct conclusion, but the supporting evidence was insufficient for an independent evaluator to verify the claim without additional PGN analysis.

This led to several refinements to the evaluation framework:

* Definition-first evaluation of chess terminology
* Anti-substitution evaluation rules
* Explicit separation of Evidence Verification and Finding Validation
* Mandatory escalation to PGN analysis when evidence is incomplete

A key outcome of the experiment was the discovery that finding correctness and evidence traceability should be treated as separate quality dimensions in future evaluations.

---

## Decision

**Supporting Assumption #1 is considered validated.**

The experiment achieved **80.9% accuracy**, exceeding the predefined feasibility threshold of **70%**.

The results provide strong evidence that AI can extract factually correct findings from individual chess PGNs.

The project can now proceed to validation of the next supporting assumption:

> AI can correctly map findings to relevant chess concepts.
