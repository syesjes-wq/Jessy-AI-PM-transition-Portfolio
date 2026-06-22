# Failure Log

This document captures major AI reasoning, evaluation, and framework failures discovered during development of the Chess Progress Tracker.

---

# Assumption #1: Finding Extraction & Evaluation

| ID     | Failure Type                 | Observation                                                                                               | Root Cause                                                                      | Framework Change                                                                           |
| ------ | ---------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| FL-001 | Evidence-to-Claim Conversion | 8 of 36 evaluated findings (22%) contained claims extracted from evidence rather than the finding itself. | Evaluator blurred the distinction between claims and supporting evidence.       | Claims must be extracted exclusively from the finding.                                     |
| FL-002 | Cognitive Closure Bias       | Evaluator inferred missing steps when evidence formed a plausible narrative.                              | Evaluator prioritized plausibility over verification.                           | Introduced explicit escalation rules and prohibited inference when evidence is incomplete. |
| FL-003 | Missing Exit Condition       | Evaluator escalated to PGN analysis even after all claims were verified.                                  | Framework defined escalation criteria but not stopping criteria.                | Added explicit termination conditions.                                                     |
| FL-004 | Evidence Hierarchy Bias      | Verification explanations were ignored when move notation appeared insufficient.                          | Evaluator treated move sequences as stronger evidence than explanations.        | Introduced structured evidence review across all evidence sources.                         |
| FL-005 | Corroboration Bias           | Claims were marked Partial despite being fully established by one evidence source.                        | Evaluator required independent corroboration across evidence sources.           | Added evidentiary sufficiency rule allowing any source to independently verify a claim.    |
| FL-006 | Concept Definition Failure   | Chess concepts were verified using consequences rather than definitions.                                  | Evaluator relied on semantic association instead of formal concept definitions. | Introduced Definition-First Evaluation.                                                    |

### Key Learning

Most failures were not caused by incorrect chess reasoning. They were caused by weaknesses in claim extraction, evidence processing, escalation logic, and concept verification.

The evaluation framework evolved from a simple correctness check into a governed evaluation process with explicit controls over scope, evidence handling, and verification.

---

# Assumption #2: Concept Mapping

| ID     | Failure Type                       | Observation                                                                                          | Root Cause                                                                                          | Framework Change                                                                    |
| ------ | ---------------------------------- | ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| FL-007 | Concept Level Error                | "Place Rooks on Open Files" mapped to Piece Activity instead of Rook Activity.                       | Hierarchy validation was missing; broader concepts were selected despite a closer concept existing. | Added hierarchy validation and closest-concept verification.                        |
| FL-008 | Piece Identity Anchoring           | Judge preferred "Do Not Bring the Queen Out Too Early" instead of "Don't Move the Same Piece Twice." | Evaluation began with piece identity rather than behavior identification.                           | Introduced Behavior-First Evaluation.                                               |
| FL-009 | Sub-Principle Generalization Error | Generic piece-safety principles were selected when queen-specific principles existed.                | Bottom-up concept generation was not enforced.                                                      | Added anchor sub-principle identification and specificity validation.               |
| FL-010 | Outcome-Oriented Finding           | Findings describing game outcomes were forced into concept mappings.                                 | Framework assumed every finding was suitable for concept mapping.                                   | Added Finding Qualification gate to distinguish behaviors from outcomes.            |
| FL-011 | Cross-Pipeline Detection Failure   | Concept mapping exposed structurally flawed findings generated upstream.                             | Assumption #1 validation did not verify whether findings represented behaviors.                     | Added a feedback loop between concept mapping and finding generation.               |
| FL-012 | Sub-Principle Scope Error          | Piece-specific principles were selected even when generic principles explained more of the finding.  | Tiebreaker rules existed but were not enforced during concept selection.                            | Added mandatory largest-proportion comparison before selecting a sub-principle.     |
| FL-013 | Question Substitution              | Model answered a simpler qualification question than the one specified in the workflow.              | The model replaced a difficult reasoning task with an easier surface-level check.                   | Restructured qualification outputs to require explicit reasoning before proceeding. |
| FL-014 | Concept Hallucination              | Model invented instructional principles not grounded in chess learning material.                     | No validation existed to confirm concepts or sub-principles were recognized chess concepts.         | Added Textbook Validation and concept grounding checks.                             |

### Key Learning

Most concept-mapping failures were not caused by a lack of chess understanding. They were caused by hierarchy-selection errors, prompt-execution failures, behavior-identification failures, and concept-grounding failures.

The framework evolved from a concept-labeling exercise into a structured decision process with qualification gates, hierarchy validation, specificity checks, and textbook validation.
