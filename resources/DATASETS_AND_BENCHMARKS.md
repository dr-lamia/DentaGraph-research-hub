# Dental Datasets and Benchmarks Relevant to DentaGraph

This page prioritizes datasets that can support evaluation of a **multispecialty, multimodal, agentic dental clinical decision-support system**.

## 1. DentCaseBench — primary DentaGraph benchmark

**Best use:** main patient-level clinical reasoning evaluation.

- 226 patient-level cases
- 10 dental specialties
- source-grounded case reports
- multimodal patient-linked images
- frozen publication-level splits
- designed for diagnosis, differential diagnosis, investigations, treatment, prognosis, referral, urgency, safety, and multi-agent tracing

Study folder:
https://drive.google.com/drive/folders/1q5fuYBblt_SKxDFlv5v5vblSSgtaxzCd?usp=sharing

Recommended role in DentaGraph:
- 136 development
- 34 public validation
- 22 private validation
- 34 hidden test

---

## 2. COde — Casangels Oro-dental dataset

**Best use:** secondary real-patient multimodal validation.

Paper:
https://doi.org/10.1038/s41597-026-07342-9

Title:
**A benchmark multimodal oro-dental dataset for large vision-language models**

Key characteristics:
- 8,775 dental checkups
- 4,800 patients
- 2018–2025
- 50,000 intraoral photographs
- 8,056 radiographs
- clinical text including diagnoses, treatment plans, medical history, and follow-up

Why it matters for DentaGraph:
- real-patient multimodal data
- much larger than most dental benchmarks
- useful for testing generalization beyond literature-derived cases
- suitable for multimodal report generation and clinical decision-support experiments

---

## 3. MMOral / MMOral-Bench

**Best use:** panoramic radiograph reasoning and VQA validation.

Paper:
https://proceedings.neurips.cc/paper_files/paper/2025/hash/3797b3a3c939156757857cf1b9afde3c-Abstract-Datasets_and_Benchmarks_Track.html

Dataset:
https://huggingface.co/datasets/OralGPT/MMOral-OPG-Bench

Code:
https://github.com/isjinghao/OralGPT

MMOral:
- 20,563 annotated panoramic radiographs
- about 1.3 million instruction-following instances

MMOral-Bench:
- 100 panoramic images
- 491 closed-ended questions
- 578 open-ended questions
- manually selected and checked

Why it matters:
- strong imaging-specific external benchmark
- already used by dental agent systems including DentAgent and OPGAgent

---

## 4. DentVLM clinical study benchmark

**Best use:** strong external multimodal diagnostic validation.

Paper:
https://doi.org/10.1038/s41467-026-75718-x

Code:
https://github.com/ZJUI-AI4H/DentVLM

Model:
https://huggingface.co/ZJU-AI4H/DentVLM

Clinical-study set:
- 1,946 patients
- 2,642 images
- 3,105 VQA pairs
- 36 diagnostic tasks
- reference standard from 4 senior experts
- high reported inter-rater agreement

Metrics used in the paper:
- multiclass diagnostic accuracy
- multilabel hit rate
- localization IoU
- rationale evaluation

Important access note:
The in-house clinical datasets are described as restricted-access because of privacy requirements; access may require author request.

---

## 5. DentalBench

**Best use:** dental knowledge and text-only reasoning, not patient-level clinical validation.

Paper:
https://arxiv.org/abs/2508.20416

Key characteristics:
- bilingual English/Chinese benchmark
- 36,597 questions
- 4 task types
- 16 dental subfields
- DentalCorpus with 337.35 million tokens

Why it matters:
Useful for testing the text/knowledge component of an agent system, but it should not replace a patient-level benchmark for DentaGraph.

---

## 6. OPG-Bench

**Best use:** structured panoramic-report evaluation.

Introduced with OPGAgent:
https://papers.miccai.org/miccai-2026/0735-Paper0308.html

Key concept:
- structured report protocol based on **(Location, Field, Value)** triples
- derived from real clinical reports
- supports analysis of findings and hallucinations beyond simple VQA

Why it matters:
The structured-report idea is relevant to DentaGraph's final Composer and could inform a radiology-specific evaluation track.

---

## 7. MMOral-X / DentalProbe

**Best use:** agentic panoramic reasoning and reinspection.

Associated paper:
https://openaccess.thecvf.com/content/CVPR2026/html/Fan_OralGPT-Plus_Learning_to_Use_Visual_Tools_via_Reinforcement_Learning_for_CVPR_2026_paper.html

DentalProbe:
- 5,000 panoramic images
- expert-curated diagnostic trajectories

MMOral-X:
- 300 open-ended questions
- region-level annotations
- multiple difficulty levels

Why it matters:
Useful for evaluating iterative inspection and image-focused agentic reasoning.

---

# Recommended DentaGraph dataset strategy

### Primary
**DentCaseBench**

Purpose:
- whole-system clinical validation
- multispecialty patient-level reasoning
- routing
- management
- safety
- escalation
- validator/repair analysis

### Secondary real-patient external validation
**COde**

Purpose:
- external multimodal generalization
- real clinical data
- report and management tasks

### Imaging-specific external validation
**MMOral-Bench and/or DentVLM clinical benchmark**

Purpose:
- panoramic and multimodal image reasoning
- external diagnostic benchmarking

### Synthetic stress testing
**Claude-generated DentaGraph stress-test cases**

Purpose:
- contradictions
- unsafe requests
- escalation
- routing
- validator activation
- repair behavior

Synthetic results should be reported separately from real or literature-derived clinical benchmark results.
