# Decision Log

## Decision 001

### Question

How should AI-generated chess findings be validated?

### Observation

No benchmark existed for determining whether a finding was factually correct.

### Action

Investigated Stockfish as a potential benchmark.

### Outcome

Stockfish provides move-level annotations such as blunders, mistakes, and accuracy scores, but the product requires parent-facing findings and recurring learning patterns.

For example:

**Product finding**

> Lost a bishop due to leaving pieces undefended in multiple games.

**Stockfish output**

> Move 14: Blunder

While Stockfish can identify individual mistakes, it cannot directly validate the higher-level findings required by the product.

### Decision

Stockfish could not serve as the primary benchmark for finding correctness.

---

## Decision 002

### Question

How can valid chess findings be defined?

### Observation

A shared definition of a valid beginner-level finding did not exist.

### Action

Created a Finding Taxonomy based on beginner chess learning material.

### Outcome

The taxonomy defined:

* Valid findings
* Observable criteria
* Expected consequences

This provided a structured reference for beginner-level chess concepts and potential evaluation criteria.

### Decision

Use the taxonomy as the initial evaluation benchmark.

---

## Decision 003

### Question

Can the Finding Taxonomy be used as the primary evaluation mechanism?

### Observation

During early testing, fewer than 10% of AI-generated findings mapped cleanly to taxonomy entries.

Many findings were:

* Variations of taxonomy findings
* More specific than taxonomy entries
* Combinations of multiple taxonomy concepts
* Expressed using different wording

### Outcome

More than 90% of findings required interpretation beyond direct taxonomy matching.

The taxonomy successfully defined concepts but failed to provide sufficient coverage for practical evaluation.

### Decision

Abandon taxonomy matching as the primary evaluation mechanism.

Retain the taxonomy as a supporting reference artifact.

---

## Decision 004

### Question

How can findings be evaluated when taxonomy matching fails?

### Observation

Human reviewers could determine correctness even when findings did not map directly to taxonomy entries.

### Action

Introduced an LLM-as-Judge approach.

### Outcome

Findings could now be evaluated based on evidence and game context rather than taxonomy matching.

This enabled evaluation of a much broader range of generated findings.

### Decision

Use a second LLM as an independent evaluator of finding correctness.

---

## Decision 005

### Question

How can judge evaluations be made consistent and repeatable?

### Observation

Repeated manual evaluations revealed inconsistencies in how the judge:

* Extracted claims
* Processed evidence
* Interpreted chess terminology
* Escalated to PGN analysis

The same finding could be evaluated differently depending on how the judge interpreted evidence and terminology.

### Action

Created a Finding Evaluation Framework.

### Outcome

Evaluation became structured and repeatable through:

* Explicit claim decomposition
* Evidence verification rules
* Finding validation rules
* Escalation criteria
* Operational definitions

### Decision

Standardize evaluation through a formal framework rather than relying on evaluator discretion.

---

## Decision 006

### Question

How should finding correctness be distinguished from evidence quality?

### Observation

During evaluation, 18 of 47 findings (38.3%) required escalation to full PGN analysis because the evidence package alone was insufficient for independent verification.

Many of these findings were ultimately determined to be correct after reviewing the complete game record.

### Outcome

Finding correctness and evidence traceability emerged as separate quality dimensions.

A finding could be:

* Correct but poorly supported
* Correct and well supported
* Incorrect despite plausible evidence
* Incorrect and poorly supported

### Decision

Separate Evidence Verification from Finding Validation within the evaluation framework.

---

## Decision 007

### Question

How should evaluator failures be handled?

### Observation

Framework implementation exposed recurring evaluator failure modes.

The most common observed failure was Evidence-to-Claim Conversion.

During review of 36 evaluated findings, 8 findings (22%) contained claims that had been incorrectly extracted from supporting evidence rather than from the finding itself.

Examples included:

* Board locations promoted into claims
* Move sequences promoted into claims
* Verification details promoted into claims

### Outcome

The evaluator was blurring the distinction between:

* Claims being evaluated
* Evidence used to evaluate those claims

This created evaluation drift and inconsistent verdicts.

### Action

Introduced a Claim Extraction Rule.

Claims must be extracted exclusively from the wording of the finding and never from:

* Key Moves
* Verification Explanations
* Chess knowledge
* Evaluator inference

### Decision

Treat evaluator failures as framework design problems rather than model capability problems.

Framework improvements should be driven by observed failure modes rather than assumptions about evaluator behavior.

---

## Decision 008

### Question

How should unresolved uncertainty be handled during evaluation?

### Observation

Multiple evaluator failures were caused by attempts to complete plausible narratives when evidence was incomplete.

Examples included:

* Assuming piece positions from the last known move
* Inferring causal relationships from correlated events
* Treating consequences as proof of chess concepts

### Outcome

The evaluator occasionally reached the correct conclusion for the wrong reason.

This increased the risk of inconsistent and non-repeatable evaluations.

### Action

Introduced:

* Definition-first evaluation
* Anti-substitution rules
* Anti-inference rules
* Explicit escalation requirements

### Decision

The evaluator's responsibility is verification, not inference.

When evidence is insufficient, uncertainty must remain unresolved until additional information becomes available.
