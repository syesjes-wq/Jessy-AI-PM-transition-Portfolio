# Experiment Results

This document summarizes the feasibility experiments conducted during development of the Chess Progress Tracker.

---

# Assumption #1: Finding Extraction

| Metric             | Value                        |
| ------------------ | ---------------------------- |
| Dataset            | 9 beginner-level chess games |
| Findings Evaluated | 47                           |
| Correct            | 38                           |
| Incorrect          | 5                            |
| Unverifiable       | 4                            |
| Accuracy           | 80.9%                        |
| Success Threshold  | 70%                          |
| Result             | ✅ Validated                  |

**Key Learning**

18 of 47 findings (38.3%) required escalation to full PGN analysis despite ultimately being correct. This revealed that finding correctness and evidence traceability are separate quality dimensions.

---

# Assumption #2: Concept Mapping

| Metric                     | Value       |
| -------------------------- | ----------- |
| Concept Mappings Evaluated | 47          |
| Correct                    | 40          |
| Partially Correct          | 3           |
| Incorrect                  | 4           |
| Accuracy                   | 85.1%       |
| Success Threshold          | 80%         |
| Result                     | ✅ Validated |

**Key Learning**

Most failures were caused by hierarchy-selection errors, behavior-identification failures, concept-definition failures, and prompt-execution failures rather than a lack of chess understanding.

---

# Overall Outcome

| Assumption         | Status      |
| ------------------ | ----------- |
| Finding Extraction | ✅ Validated |
| Concept Mapping    | ✅ Validated |

The experiments provide evidence that AI can reliably extract chess findings from PGNs and map those findings to instructional chess concepts, supporting progression to parent-facing insight generation.
