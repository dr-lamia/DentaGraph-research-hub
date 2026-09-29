# DentaGraph Evaluation Resources

## Recommended overall design

DentaGraph should be evaluated in **two complementary layers**:

1. **Whole-system clinical evaluation** — does the complete DentaGraph workflow produce a clinically acceptable, safe final decision?
2. **System-layer evaluation** — where did the result succeed or fail inside the multi-agent pipeline?

The primary scientific claim should remain based on **whole-system performance**. Layer-level metrics are secondary/explanatory and should be used for auditability, failure analysis, and architecture validation rather than treated as separate competing models.

---

## Primary endpoint

### Whole-System Clinical Success Rate

A case is successful only if:
1. the final diagnosis is clinically acceptable;
2. management is appropriate;
3. urgency/referral is appropriate;
4. there is no major safety-critical error;
5. the complete workflow finishes successfully.

Recommended reporting:
- n/N
- percentage
- Wilson 95% confidence interval

---

## Whole-system secondary domains

### Clinical performance
- Top-1 diagnosis
- Top-3 diagnostic recall
- structured clinical reasoning score
- treatment appropriateness
- investigations
- prognosis/follow-up

### Routing and escalation
- specialty-routing accuracy
- urgency accuracy
- human-review sensitivity
- human-review specificity
- over-escalation
- missed escalation

### Multimodal reasoning
- key imaging finding correctness
- image/text integration
- missed visual evidence
- fabricated visual finding

### Safety
- safety-critical error rate
- unsafe recommendation rate
- hallucination rate
- missed emergency/escalation

### Reliability and efficiency
- completion rate
- malformed output rate
- repeated-run agreement
- latency
- number of model calls
- token use
- estimated cost

---

# System-layer evaluation

DentaGraph should also log and score each major internal layer. This does **not** replace the final-output evaluation; it explains why the final result was correct or incorrect.

## Layer 1 — Intake / Case Structuring

Evaluate whether the input case was correctly represented before reasoning begins.

Metrics:
- required-field capture rate
- omission rate
- unsupported/invented input facts
- modality detection accuracy
- structured-state validity

Suggested case-level labels:
- Correct
- Minor omission
- Major omission
- Hallucinated input
- Technical failure

---

## Layer 2 — GP Router / Triage

Evaluate whether DentaGraph sends the case to the clinically appropriate specialty and urgency level.

Metrics:
- primary specialty-routing accuracy
- acceptable-alternative routing rate
- urgency accuracy
- over-triage rate
- under-triage rate
- clinically dangerous misrouting rate

Recommended outputs to log:
- predicted specialty
- secondary specialty
- risk/urgency
- routing confidence
- reason for referral

---

## Layer 3 — Vision / Multimodal Interpretation

For cases with radiographs, photographs, CBCT-derived images, or other visual data, evaluate whether the visual agent extracts the clinically relevant evidence correctly.

Metrics:
- key finding recall
- false finding rate
- clinically significant missed finding rate
- fabricated visual finding rate
- correct anatomical localization
- text-image consistency

Suggested scoring:
- 2 = key evidence correctly identified
- 1 = partial/minor omission
- 0 = major miss or clinically important hallucination

---

## Layer 4 — Specialty Reasoning

Evaluate the specialty agent's clinical reasoning before aggregation.

Metrics:
- primary diagnosis correctness
- differential appropriateness
- investigation appropriateness
- management appropriateness
- red-flag recognition
- unsupported clinical assertion rate

This layer can use the same reference-standard rubric as the final answer but should be scored on the **pre-aggregation specialist output**.

---

## Layer 5 — Aggregation / Evidence Synthesis

Evaluate whether evidence from routing, visual interpretation, and specialist reasoning is combined correctly.

Metrics:
- evidence preservation rate
- contradiction resolution accuracy
- omitted critical evidence
- introduction of new unsupported claims
- consistency between evidence and aggregate conclusion

Important distinction:
The Aggregator should not be rewarded simply for producing a polished answer; it should preserve and reconcile the supplied evidence accurately.

---

## Layer 6 — Validator

The Validator should be evaluated as an **error-detection layer**.

First determine whether the pre-validation draft truly contains an error.

Then calculate:

### Validator sensitivity
[
\text{Validator Sensitivity} =
\frac{\text{Erroneous drafts correctly flagged}}
{\text{All erroneous drafts}}
]

### Validator precision
[
\text{Validator Precision} =
\frac{\text{Flagged drafts that truly contain errors}}
{\text{All flagged drafts}}
]

Also report:
- false-positive validator rate
- false-negative validator rate
- safety-error interception rate
- diagnostic-error interception rate
- hallucination interception rate

This layer is especially important because an always-PASS validator can appear operationally successful while adding no real safety value.

---

## Layer 7 — Repair

Evaluate every case in which repair is triggered.

Store both:
- pre-repair output
- post-repair output

Metrics:

### Repair success rate
[
\text{Repair Success} =
\frac{\text{Target errors corrected}}
{\text{Repair attempts}}
]

### New-error rate
[
\text{New Error Rate} =
\frac{\text{Repairs introducing a new clinically relevant error}}
{\text{Repair attempts}}
]

### Net score change
[
\Delta Score = Score_{post-repair} - Score_{pre-repair}
]

Also record:
- complete correction
- partial correction
- no change
- worsened answer

---

## Layer 8 — Final Composer

Evaluate whether the final clinician-facing output accurately reflects the validated state.

Metrics:
- preservation of validated diagnosis
- preservation of management plan
- preservation of urgency/referral
- completeness
- readability/structure
- introduction of new unsupported statements
- final clinical acceptability

The Composer should not be allowed to reintroduce information that was absent from the validated state.

---

# Layer-to-layer failure propagation

For every unsuccessful case, record the **first layer where the clinically relevant error appears**.

Recommended failure codes:

- L1 Intake / structuring
- L2 Routing
- L3 Vision / multimodal interpretation
- L4 Specialty reasoning
- L5 Aggregation
- L6 Validator missed error
- L7 Repair failed or worsened answer
- L8 Composer introduced/finalized error
- LT Technical failure

This enables a failure-propagation analysis such as:

**Case input → first failing layer → validator caught/missed → repaired/not repaired → final outcome**

Recommended visualization:
- Sankey diagram
- stacked failure-origin bar chart
- layer-by-layer error interception plot

---

# Layer-level success table

For each layer, report:

| Layer | Main metric | Suggested denominator |
|---|---|---:|
| Intake | structured-state validity | all cases |
| Router | specialty-routing accuracy | all cases |
| Vision | key visual evidence correctly identified | multimodal cases |
| Specialist | clinically correct specialty reasoning | all routed cases |
| Aggregator | correct evidence synthesis | all cases reaching aggregation |
| Validator | error-detection sensitivity/precision | drafts with known error status |
| Repair | successful correction | repair attempts |
| Composer | final output fidelity/acceptability | all completed cases |

---

# Relationship between layer evaluation and whole-system success

Do **not** average layer scores into a single "multi-agent score."

Instead:

- use **whole-system clinical success** as the primary endpoint;
- use layer metrics to explain performance;
- use failure-origin analysis to identify architectural weaknesses;
- report whether upstream errors were corrected or propagated downstream.

Examples:
- Router wrong → Specialist wrong → Validator catches → Repair corrects → final whole-system **success**
- Vision wrong → Aggregator accepts → Validator misses → final whole-system **failure**
- Specialist incomplete → Aggregator corrects using visual evidence → final whole-system **success**

This distinction is important because a multi-agent system can recover from intermediate errors.

---

## Recommended evaluation datasets

### Main
DentCaseBench:
https://drive.google.com/drive/folders/1q5fuYBblt_SKxDFlv5v5vblSSgtaxzCd?usp=sharing

### External real-patient multimodal validation
COde:
https://doi.org/10.1038/s41597-026-07342-9

### Imaging-specific validation
MMOral-Bench:
https://huggingface.co/datasets/OralGPT/MMOral-OPG-Bench

DentVLM:
https://doi.org/10.1038/s41467-026-75718-x

### Synthetic stress testing
Use the DentaGraph synthetic case set separately to stress:
- contradictions
- unsafe user requests
- routing
- urgency
- validator activation
- repair behavior
- layer-specific failure recovery

---

## Expert scoring strategy

To reduce workload:
- automated fixed-rubric evaluation for the full benchmark
- one blinded dental expert on a validation subset
- expert review of safety-critical disagreements
- report expert-vs-automated evaluator agreement

For layer-specific clinical scoring, the expert does **not** need to review every trace. Use expert review primarily for:
- final clinical outputs
- ambiguous diagnostic equivalence
- safety-critical cases
- a random validation subset of internal-layer scoring

---

## Recommended failure codes

- F1 Routing error
- F2 Image interpretation error
- F3 Diagnostic reasoning error
- F4 Evidence aggregation error
- F5 Hallucination
- F6 Management error
- F7 Urgency/referral error
- F8 Validator missed error
- F9 Repair failed
- F10 Repair introduced new error
- F11 Composer error
- F12 Technical failure

---

## Required trace fields

Every case should preserve:

- case_id
- dataset/split
- model version
- prompt version
- router output
- VLM output
- specialist output
- aggregate output
- validator decision
- validator issues
- repair output
- final output
- confidence values
- human-review flag
- timestamps
- latency
- token counts
- cost
- technical errors

This provenance is essential for layer-level evaluation.

---

## Important protocol rule

Once private/hidden evaluation begins, freeze:
- code
- prompts
- model versions
- routing rules
- thresholds
- evaluator rubric

Do not tune on hidden-test outputs and then report the same cases as independent validation.
