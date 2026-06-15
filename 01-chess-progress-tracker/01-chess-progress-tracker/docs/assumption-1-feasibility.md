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

The initial evaluation strategy relied on the Finding Taxonomy.

The expectation was that AI-generated findings could be evaluated by mapping them directly to predefined beginner chess findings and observable criteria.

A taxonomy containing 17 beginner-level chess finding categories was created from chess learning material and intended to serve as the primary evaluation benchmark.

However, early testing revealed that fewer than 10% of AI-generated findings mapped cleanly to taxonomy entries.

Most findings were:

* Variations of taxonomy findings
* More specific than taxonomy entries
* Combinations of multiple taxonomy concepts
* Expressed using different wording than the taxonomy

As a result, taxonomy coverage was insufficient to serve as the primary evaluation mechanism.

This led to a shift in evaluation strategy.

Instead of evaluating findings through taxonomy matching, a second LLM was introduced as a judge to independently assess finding correctness.

Initial evaluations were performed manually.

Repeated review of these evaluations exposed inconsistencies in how the judge:

* Extracted claims
* Processed evidence
* Interpreted chess terminology
* Escalated to PGN analysis
* Distinguished evidence quality from finding correctness

These observations ultimately led to the development of a formal Finding Evaluation Framework.

The framework evolved iteratively through evaluation of real findings and was refined through multiple rounds of failure analysis before being used in the final feasibility study.

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

The most significant discovery was that a theoretically complete benchmark does not automatically translate into a practical evaluation mechanism.

The initial evaluation strategy relied on a finding taxonomy containing beginner-level chess concepts and observable criteria. However, early testing revealed that fewer than 10% of AI-generated findings mapped cleanly to taxonomy entries. While the taxonomy remained useful for defining concepts, it proved insufficient as the primary evaluation mechanism.

This led to the introduction of an LLM-as-Judge approach and the development of a dedicated Finding Evaluation Framework.

During framework implementation, multiple evaluator failure modes were discovered, including:

* Converting evidence into evaluation claims
* Completing plausible narratives when evidence was incomplete
* Escalating analysis even after all claims had been verified
* Prioritizing certain evidence sources over others
* Requiring unnecessary corroboration across evidence sources
* Verifying chess concepts using consequences rather than definitions

These failures highlighted that designing an evaluation system requires more than defining correctness criteria. It also requires explicit controls over how evaluators process evidence, resolve uncertainty, and determine when evaluation should stop.

The final experiment revealed an important distinction between **finding correctness** and **evidence traceability**.

Although 38 findings (80.9%) were ultimately determined to be factually correct, 18 findings (38.3%) could not be fully verified from the evidence package alone and required escalation to full PGN analysis.

Most failures were evidence-traceability failures rather than chess-reasoning failures. In many cases, the AI reached the correct conclusion, but the supporting evidence was insufficient for an independent evaluator to verify the claim without additional analysis.

These observations led to several refinements to the evaluation framework, including:

* Definition-first evaluation of chess terminology
* Explicit claim decomposition rules
* Anti-substitution evaluation rules
* Structured evidence processing requirements
* Separation of Evidence Verification and Finding Validation
* Explicit escalation and termination criteria
* Mandatory PGN analysis when evidence is incomplete

A key outcome of this feasibility study was the discovery that evaluation quality depends not only on the accuracy of the underlying AI system, but also on the design of the evaluation process itself.

Finding correctness and evidence traceability should therefore be treated as separate quality dimensions in future evaluations.

---

## Decision

**Supporting Assumption #1 is considered validated.**

The experiment achieved **80.9% accuracy**, exceeding the predefined feasibility threshold of **70%**.

The results provide strong evidence that AI can extract factually correct findings from individual chess PGNs.

The project can now proceed to validation of the next supporting assumption:

> AI can correctly map findings to relevant chess concepts.
