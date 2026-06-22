# Experiment Results

This document summarizes the feasibility experiments conducted during development of the Chess Progress Tracker.

---

# Assumption #1: Finding Extraction

## Experiment Summary

| Metric             | Value                                                     |
| ------------------ | --------------------------------------------------------- |
| Assumption         | AI can extract factually correct findings from chess PGNs |
| Dataset            | 9 beginner-level chess games                              |
| Findings Evaluated | 47                                                        |
| Correct            | 38                                                        |
| Incorrect          | 5                                                         |
| Unverifiable       | 4                                                         |
| Accuracy           | 80.9%                                                     |
| Success Threshold  | 70%                                                       |
| Result             | Validated                                                 |

### Key Observation

Although overall finding accuracy reached **80.9%**, 18 of 47 findings (38.3%) required escalation to full PGN analysis because the evidence package alone was insufficient for independent verification.

This revealed that **finding correctness** and **evidence traceability** are separate quality dimensions and led to the development of the Finding Evaluation Framework.

---

# Assumption #2: Concept Mapping

## Experiment Summary

| Metric                     | Value                                                          |
| -------------------------- | -------------------------------------------------------------- |
| Assumption                 | AI can correctly map chess findings to relevant chess concepts |
| Concept Mappings Evaluated | 47                                                             |
| Correct                    | 40                                                             |
| Partially Correct          | 3                                                              |
| Incorrect                  | 4                                                              |
| Accuracy                   | 85.1%                                                          |
| Success Threshold          | 80%                                                            |
| Result                     | Validated                                                      |

### Key Observation

The majority of incorrect mappings were not caused by a lack of chess understanding. Most failures were caused by hierarchy-selection errors, behavior-identification failures, concept-definition failures, and prompt-execution failures.

This led to the creation of the Concept Mapping Framework and the Concept Mapping Evaluation Framework, introducing behavior-first reasoning, hierarchy validation, specificity checks, and textbook validation.

---

# Overall Outcome

| Assumption                         | Result      |
| ---------------------------------- | ----------- |
| Assumption #1 – Finding Extraction | ✅ Validated |
| Assumption #2 – Concept Mapping    | ✅ Validated |

The feasibility studies provide evidence that AI can:

1. Extract factually correct findings from chess PGNs.
2. Map validated findings to instructional chess concepts.

These results support progression to the next stage of validation: generating parent-facing chess improvement insights.
