# Dental Agent and Multi-Agent Papers

A curated list of dental agentic-AI papers relevant to DentaGraph.

## 1. DentAgent

**DentAgent: Evidence-Centric Multi-Agent Coordination for Multimodal Dental Reasoning**

ArXiv:
https://arxiv.org/abs/2608.18878

Architecture:
- Orchestrator
- five modality-specific specialists
- Evidence Blackboard
- iterative evidence sufficiency verification
- bounded specialist tool use
- structured evidence normalization, linking, coverage tracking, and conflict resolution

Modalities:
- text
- panoramic radiographs
- intraoral photographs
- cephalometric radiographs
- 3D intraoral scan meshes

Evaluation:
- DentalBench
- MMOral-Bench
- DentVLM reader-study benchmark
- IOSVQA

Representative metrics:
- accuracy
- BERTScore
- model-judge score
- multi-label hit rate

Important difference from DentaGraph:
DentAgent is primarily organized around **modality specialists and evidence acquisition**, while DentaGraph is designed around **clinical specialty routing, patient-level case synthesis, explicit validation/repair, and clinician escalation**.

---

## 2. OralAgent

**OralAgent: Integrating Reasoning, Tools, and Knowledge for Interactive Dental Image Analysis**

ArXiv:
https://arxiv.org/abs/2605.27378

Official code:
https://github.com/isjinghao/OralAgent

Key features:
- multimodal reasoning
- tool-based decision-making
- dental knowledge retrieval
- 22 visual analysis tools
- retrieval resource built from 368 widely used dental textbooks
- autonomous planning and multi-step tool use

Evaluation:
- MMOral-Uni
- MMOral-OPG
- OralQA-ZH

Role in literature:
A major early dental-specialized agent for interactive dental image analysis.

---

## 3. OPGAgent

**OPGAgent: An Agent for Auditable Dental Panoramic X-ray Interpretation**

MICCAI 2026:
https://papers.miccai.org/miccai-2026/0735-Paper0308.html

ArXiv:
https://arxiv.org/abs/2603.00462

Official code:
https://github.com/Zhaolin-Yu/OPGAgent

Architecture:
- hierarchical evidence gathering
- global, quadrant, and tooth-level analysis
- specialized perception toolbox
- expert zoo
- Consensus Subagent
- anatomically constrained conflict resolution

Evaluation:
- OPG-Bench
- MMOral-OPG

Notable contribution:
Introduces structured reporting with **(Location, Field, Value)** triples and explicitly evaluates false positives/hallucinations.

---

## 4. OrthoAgent

**OrthoAgent: A knowledge-enhanced multi-agent framework for multimodal orthodontic diagnosis and treatment planning**

Journal:
Dental Research, 2026

DOI:
https://doi.org/10.1016/j.dtrs.2026.100039

Key features:
- hierarchical multi-agent architecture
- multimodal orthodontic perception
- 2D images
- CBCT
- intraoral scans
- retrieval-grounded treatment reasoning

Clinical evaluation:
- 69 real-world orthodontic cases
- 12 classification tasks
- 17 continuous measurements
- blinded expert review
- clinician-rated reusability
- time-tracked human-AI workflow
- paired ablation study

Reported examples:
- mean accuracy 90.5% across 12 classification tasks
- expert report score 3.43/5
- safety score 4.19/5
- estimated editing-burden reduction 46.8%
- end-to-end time reduction 41.74%

Why it is especially relevant to DentaGraph:
It is one of the clearest dental examples of a multi-agent system evaluated on **real clinical cases** rather than only QA benchmarks.

---

## 5. OralGPT-Plus

**OralGPT-Plus: Learning to Use Visual Tools via Reinforcement Learning for Panoramic X-ray Analysis**

CVPR 2026:
https://openaccess.thecvf.com/content/CVPR2026/html/Fan_OralGPT-Plus_Learning_to_Use_Visual_Tools_via_Reinforcement_Learning_for_CVPR_2026_paper.html

ArXiv:
https://arxiv.org/abs/2603.06366

Related code:
https://github.com/isjinghao/OralGPT

Key features:
- agentic vision-language model
- iterative visual-tool use
- symmetry-aware reinspection
- reinforcement learning for multi-step diagnostic verification

Resources introduced:
- DentalProbe: 5,000-image diagnostic-trajectory dataset
- MMOral-X: 300 open-ended panoramic diagnostic questions

---

## 6. JADE-Plus

**JADE-Plus: A Multimodal Agentic Retrieval-Augmented Generation Large Language Framework for Diagnostic Support in Jawbone Lesions**

Journal:
Journal of Imaging Informatics in Medicine, 2026

PubMed:
https://pubmed.ncbi.nlm.nih.gov/42440194/

DOI:
https://doi.org/10.1007/s10278-026-02086-9

Focus:
- jawbone-lesion diagnostic support
- multimodal RAG
- agentic verification

Clinical evaluation:
- 40 retrospectively selected clinical cases
- real panoramic radiographs
- reference diagnosis based on pathology where available or specialist consensus/follow-up

Evaluation:
- Top-1 diagnostic accuracy
- Top-3 diagnostic accuracy
- ablation analysis
- intra-model reproducibility
- response time

Why it matters:
A useful precedent for clinically oriented dental agent evaluation.

---

## 7. DGADS

**DGADS: A graph-based agentic decision support system for precision dental question answering**

Journal:
Journal of Dentistry, 2026

DOI:
https://doi.org/10.1016/j.jdent.2026.106875

Architecture:
- DentalKG knowledge-graph builder
- graph-based RAG
- agentic RAG

Evaluation:
- 500 internal multiple-choice questions
- 260 external multiple-choice questions
- open-ended dental questions

Metrics:
- MCQ accuracy
- 5-point open-ended scores
- comparison with LLM and conventional RAG baselines

Role:
Strong evidence for agentic dental QA and hallucination mitigation, but not a whole-patient multispecialty clinical validation study.

---

## 8. AI agent-based system for interpretable panoramic dental X-ray analysis

Journal of Dentistry, 2026 conference abstract

DOI:
https://doi.org/10.1016/j.jdent.2026.106368

Architecture:
- Vision Agent
- report-generation agent
- validator agent

Human-expertise integration:
- trained using expert gaze maps from the Tufts dental database

Evaluation:
- correlation with expert gaze
- intersection over union (IoU)
- comparison of four Vision Agent configurations

Role:
Relevant precedent for a modular dental system containing an explicit **validator agent**.

---

# Key lesson for DentaGraph

Current dental agent papers tend to evaluate one or more of:

- benchmark accuracy
- open-ended model-judge scores
- image-specific metrics
- report quality
- ablation studies
- repeated-run stability
- clinical expert scoring
- runtime/cost
- real-case workflow efficiency

DentaGraph can contribute a broader **patient-level whole-system evaluation** across specialties, while retaining agent-level process metrics for routing, validation, repair, safety, and escalation.
