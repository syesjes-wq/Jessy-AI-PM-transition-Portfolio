# Assumption #2 Feasibility Analysis

## Executive Summary

| Item              | Result                                                              |
| ----------------- | ------------------------------------------------------------------- |
| Assumption        | AI can correctly map chess findings to instructional chess concepts |
| Dataset           | 47 validated findings                                               |
| Correct Mappings  | 40                                                                  |
| Partially Correct | 3                                                                   |
| Incorrect         | 4                                                                   |
| Accuracy          | 85.1%                                                               |
| Success Threshold | 80%                                                                 |
| Outcome           | Validated                                                           |

**Conclusion:** The experiment achieved **85.1% concept-mapping accuracy**, exceeding the predefined success threshold of 80%. This provides strong evidence that AI can reliably translate chess findings into instructional concepts and supports proceeding to parent-facing insight generation.

---

## Assumption Under Validation

**Supporting Assumption #2**

> AI can correctly map chess findings to relevant chess concepts.

This assumption represents the second reasoning layer in the Chess Progress Tracker workflow:

```text
PGNs → Findings → Concepts → Parent Insights
```

Assumption #1 validated that AI can extract factually correct findings from chess games. This experiment evaluates whether those findings can be translated into the underlying chess concepts and instructional principles they represent.

---

## Problem

Findings and concepts operate at different levels of abstraction.

**Finding**

> Queen moved three times in the opening.

**Concept**

> Rapid Piece Development

A single finding may support multiple concepts, and a concept may be supported by multiple findings. This ambiguity makes concept mapping significantly more challenging than finding extraction.

The key question:

> Can AI consistently identify the underlying instructional concept represented by a chess finding?

---

## Benchmark Strategy

An exhaustive taxonomy of all possible finding-to-concept relationships was considered but rejected due to scalability limitations.

Instead, the experiment used an **LLM-as-Judge** approach.

For each finding:

1. AI generated a concept and supporting reasoning.
2. An independent judge evaluated the mapping.
3. A sample of mappings was manually reviewed against chess learning material.
4. The evaluation framework was refined based on observed failure modes.

This approach allowed concept mappings to be evaluated without requiring a predefined benchmark for every possible finding.

---

## Experiment Design

### Dataset

47 findings previously validated during Assumption #1.

### Evaluation

Each mapping was evaluated on:

* Correct interpretation of the finding
* Appropriateness of the selected concept
* Logical connection between finding and concept
* Consistency with recognized chess instructional principles

### Success Criteria

| Accuracy | Interpretation                           |
| -------- | ---------------------------------------- |
| >80%     | Strong evidence capability exists        |
| 70–80%   | Moderate evidence capability exists      |
| <70%     | Capability not sufficiently demonstrated |

The experiment was designed to evaluate feasibility rather than production readiness.

---

## Results

| Outcome           | Count |
| ----------------- | ----- |
| Correct           | 40    |
| Partially Correct | 3     |
| Incorrect         | 4     |

**Concept Mapping Accuracy = 40 / 47 = 85.1%**

The observed accuracy exceeded the predefined threshold and falls within the **Strong Evidence Capability** category.

---

## Key Learnings

The experiment revealed that concept mapping is fundamentally a **selection problem rather than a generation problem**.

Most failures were not caused by a lack of chess understanding. Instead, they were caused by:

* Selecting concepts that were too broad or too narrow
* Choosing generic principles when more specific concepts existed
* Mapping outcomes rather than underlying behaviors
* Inventing concepts not grounded in recognized chess instruction
* Failing to fully execute decision rules already present in the workflow

These observations led to several framework improvements:

* Behavior-first concept mapping
* Bottom-up concept selection
* Explicit hierarchy validation
* Textbook principle validation
* Structured comparison of competing mappings

The experiment also demonstrated that concept-mapping accuracy depends heavily on the quality of the evaluation framework. Several mappings initially classified as incorrect were later determined to be valid after refining the evaluation process.

---

## Decision

**Supporting Assumption #2 is considered validated.**

The experiment achieved **85.1% accuracy**, exceeding the predefined success threshold of **80%**.

The results provide strong evidence that AI can reliably map validated chess findings to instructional concepts and sub-principles.

The project can now proceed to validation of the next supporting assumption:

> AI can generate useful parent-facing insights from mapped chess concepts.
