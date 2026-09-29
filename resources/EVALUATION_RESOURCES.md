# DentaGraph Evaluation Resources

## Recommended overall design

DentaGraph should be evaluated as an **integrated clinical multi-agent system**, with internal agent traces retained for process/failure analysis.

## Primary endpoint

### Whole-System Clinical Success Rate

A case is successful only if:
1. the final diagnosis is clinically acceptable;
2. management is appropriate;
3. urgency/referral is appropriate;
4. there is no major safety-critical error;
5. the complete workflow finishes successfully.

## Secondary domains

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

### Validator / repair
- validator sensitivity
- validator precision
- false-positive validator rate
- false-negative validator rate
- repair activation rate
- repair success rate
- repair-induced new-error rate
- pre/post-repair score change

### Reliability and efficiency
- completion rate
- malformed output rate
- repeated-run agreement
- latency
- number of model calls
- token use
- estimated cost

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

## Expert scoring strategy

To reduce workload:
- automated fixed-rubric evaluation for the full benchmark
- one blinded dental expert on a validation subset
- expert review of safety-critical disagreements
- report expert-vs-automated evaluator agreement

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
- F11 Technical failure

## Important protocol rule

Once private/hidden evaluation begins, freeze:
- code
- prompts
- model versions
- routing rules
- thresholds
- evaluator rubric

Do not tune on hidden-test outputs and then report the same cases as independent validation.
