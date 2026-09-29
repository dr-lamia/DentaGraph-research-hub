# Dental Agent Comparison Matrix

| System | Main scope | Multi-agent / agentic structure | Modalities | Real clinical cases? | Main evaluation | Explicit validator / verification | Public code |
|---|---|---|---|---|---|---|---|
| **DentAgent** | General multimodal dental reasoning | Orchestrator + 5 modality specialists + Evidence Blackboard | Text, pano, intraoral photo, ceph, IOS mesh | Benchmark-based; not presented as a single retrospective patient cohort | Accuracy, BERTScore, model-judge, hit rate, ablation | Evidence sufficiency verification + conflict resolution | No official code repository identified in the paper at time of curation |
| **OralAgent** | Interactive dental image analysis | Tool-using dental agent | Multimodal dental images + retrieval | Mainly benchmark-based | MMOral-Uni, MMOral-OPG, OralQA-ZH | Iterative reasoning/tool use | Yes |
| **OPGAgent** | Panoramic interpretation | Hierarchical evidence gathering + toolbox + consensus subagent | Panoramic radiograph | Evaluation on OPG-Bench and MMOral-OPG | Structured report metrics, precision/recall, false positives, VQA | Yes: consensus/conflict resolution | Yes |
| **OrthoAgent** | Orthodontic diagnosis and treatment planning | Hierarchical multi-agent | 2D, CBCT, IOS | **Yes: 69 real-world cases** | Classification accuracy, measurement error, expert review, reusability, workflow time, ablation | Retrieval-grounded reasoning and multi-agent integration | Data/code on reasonable request |
| **OralGPT-Plus** | Panoramic reinspection | Agentic VLM with iterative visual tools | Panoramic | Benchmark/dataset based | MMOral-X + established pano benchmarks | Iterative reinspection | Related OralGPT repo public |
| **JADE-Plus** | Jawbone lesion diagnosis | Agentic multimodal RAG | Clinical text + panoramic radiograph | **Yes: 40 retrospective cases** | Top-1, Top-3, reproducibility, ablation, response time | Agentic verification | Publication resource; code status should be checked before use |
| **DGADS** | Dental question answering | Graph RAG + agentic RAG | Text/knowledge | Not patient-cohort validation | 500 internal MCQ, 260 external MCQ, open-ended scoring | Information-sufficiency checking | Not clearly established as open source in the publication |
| **Interpretable pano multiagent system** | Panoramic report generation | Vision + report + validator agents | Panoramic + expert gaze maps | Expert-derived imaging data | correlation + IoU | **Yes: validator agent** | Conference abstract |
| **DentaGraph** | Multispecialty patient-level clinical decision support | Router → multimodal analysis → specialist reasoning → aggregation → validator → repair → composer | Clinical text + dental images/radiographs | Planned broad validation with DentCaseBench and external real-patient data | **Whole-system clinical success + layer-level evaluation**, diagnosis, management, routing, safety, validator/repair, escalation, reliability, cost | **Dedicated validator + bounded repair + human-review escalation** | Research project |

## Where DentaGraph is positioned

DentaGraph should not claim to be the first dental agent or the first dental multi-agent system.

A more defensible contribution is:

> A multispecialty, patient-level, multimodal dental clinical decision-support workflow that combines clinical specialty routing, evidence integration, explicit safety validation, bounded self-repair, and human-review escalation within an auditable stateful architecture.

## Evaluation gap DentaGraph can address

Many existing systems focus on:
- QA
- one imaging modality
- one specialty
- final-answer benchmark performance

DentaGraph can evaluate:
- the complete clinical case
- multiple dental specialties
- diagnosis and treatment planning
- referral and urgency
- safety
- escalation
- validator interception
- repair success
- **layer-by-layer performance**
- **error interception and recovery across layers**
- failure propagation
- technical reliability

## DentaGraph layer-level evaluation

In addition to final-output performance, DentaGraph can evaluate each architecture layer:

1. Intake / case structuring
2. GP Router / triage
3. Vision / multimodal interpretation
4. Specialty reasoning
5. Evidence aggregation
6. Validator
7. Repair
8. Final Composer

The primary endpoint remains **whole-system clinical success**. Layer-level metrics are secondary and are used to identify:
- where an error first appeared;
- whether a downstream layer intercepted it;
- whether repair corrected it;
- whether the final answer remained clinically acceptable.

This lets DentaGraph study **error propagation and recovery**, not merely final answer accuracy.
