---
name: academic-paper-reading
description: Read biomedical and AI papers from primary evidence with structured methods analysis and deep figure-by-figure teaching.
tags: ["自习"]
---

# Academic paper reading

Use this skill to turn a paper into an auditable teaching map rather than a shallow summary. The default audience understands machine learning fundamentals but may need explicit pathology, oncology, biology, statistics, and clinical-context explanations.

## Core contract

- Read the primary paper evidence before explaining it. In a local project, prefer the original PDF, extracted full text, and page-level evidence over prior summaries.
- Separate four voices: paper-reported fact, faithful translation, teaching interpretation, and project-specific inference.
- Never turn a review's cited result into the review's own experiment. Never turn an association into mechanism, a prediction into a measurement, or a cohort result into an individual prognosis.
- Treat every important figure as a small lesson. A figure explanation must connect the visual elements to the paper's question, methods, results, limitations, and next reading step.
- Explain the unit of analysis every time it changes: patient, cohort, specimen, block, slide, WSI, ROI, patch, tissue region, cell, nucleus, spot, graph node, or clinical encounter.
- Preserve the source of truth. In repositories with Markdown plus generated HTML, edit Markdown/configuration sources and regenerate HTML; do not hand-edit generated HTML.
- Finish with the relevant checks and a versioned commit when project files changed. Do not create an empty commit for reading-only discussion.

## When to use

Use for:

- First-pass or deep reading of a biomedical, pathology, oncology, digital pathology, spatial omics, or medical-AI paper.
- Explaining a pasted paragraph, screenshot, table, figure, abstract, methods section, or result.
- Translating a cropped screenshot while recovering clipped text from the full source.
- Building or extending a structured reading note.
- Reviewing a paper's figure explanations for missing panels, weak evidence boundaries, or overinterpretation.
- Converting a reading conversation into a durable Q&A supplement for one paper.

Do not use as a substitute for patient diagnosis, staging, treatment selection, or individualized medical advice.

## Procedure

### 1. Preflight and identity

1. Check the project instructions and current Git state before editing:

```powershell
git status --short
git log -3 --format="%h %s"
```

2. Identify the paper's stable identity:
   - article number and reading order
   - title, authors, journal, year, DOI
   - article type: review, original research, clinical trial, commentary, dataset, or methods paper
   - source PDF and extracted evidence directory
   - prerequisite papers and intended role in the reading route
3. Do not infer identity from a filename alone. Confirm against the record, first PDF page, DOI, and article title.
4. State the evidence boundary early:
   - Does the paper have its own cohort
   - Does it train a new model
   - Does it have patient-level labels
   - Does it have internal, external, prospective, workflow, or outcome validation
   - Which numbers belong to cited prior work rather than this paper

### 2. Build a chapter map before detail

Read the abstract, introduction, section headings, figure list, conclusion, and limitations first. Produce a compact map:

```text
clinical or biological problem
    -> data and observation unit
    -> task and target
    -> model or analytical pipeline
    -> intermediate representation
    -> evaluation and validation
    -> biological or clinical interpretation
    -> limitations and transfer boundary
```

Then answer:

- What is the paper trying to make possible
- What does it actually measure or predict
- What is the central comparison
- What would count as a convincing result
- What remains unproven

For a review, replace “the model” with “the body of work summarized by the review.” For an original study, distinguish the authors' data from external reference data. For a clinical trial, distinguish the intervention, randomization unit, primary outcome, process outcomes, and patient outcomes.

### 3. Read in evidence order

For each section, use this sequence:

1. Locate the exact paragraph in the full evidence text or PDF.
2. Read the surrounding paragraph and its cited figure/table.
3. Record the observation unit, denominator, comparison group, and validation level.
4. Translate only after resolving clipped text, abbreviations, and cross-references.
5. Explain the method and its implication in Chinese.
6. State what the evidence supports and what it cannot support.

For a screenshot with a cropped edge:

- recover missing words from the full PDF or page evidence
- say which part was recovered rather than silently inventing it
- preserve the PDF physical page number
- distinguish a screenshot used for locating text from an independently verified result

### 4. Explain the paper at the right depth

A useful explanation should let the reader reconstruct the paper's reasoning. Cover these layers as relevant:

#### Scientific and medical object

Explain the tissue, disease, cell type, lesion, biomarker, treatment context, and clinical endpoint before discussing the model. For pathology, distinguish:

- cell versus tissue region
- nucleus versus whole cell
- epithelium versus stroma
- gland versus lumen versus crypt
- atypia versus malignancy
- differentiation or grade versus stage
- invasion versus metastasis
- H&E morphology versus IHC, IF, sequencing, and spatial transcriptomics
- TIL quantity versus immune subtype or functional state

Use the local medical foundation note when available, but do not replace paper-specific definitions with generic textbook wording.

#### Data and sampling

State:

- source and number of cohorts, if reported
- patient, specimen, slide, WSI, patch, cell, or spot counts
- inclusion and exclusion rules
- train, validation, test, external, and prospective splits
- whether multiple slides or patches from one patient can leak across splits
- stain, scanner, magnification, resolution, and preprocessing
- whether the data are 2D samples of 3D tissue

Never treat patches, spots, or cells as independent patients unless the paper explicitly establishes that design.

#### Task and model

For each task, write the input, target, intermediate representation, and output. Explain:

- supervised, weakly supervised, self-supervised, or unsupervised signal
- segmentation, detection, classification, regression, ranking, survival, generation, or retrieval
- WSI to patch to embedding to aggregation when relevant
- graph nodes, edges, neighborhoods, and distance rules when relevant
- multimodal alignment, registration, or paired data when relevant
- which outputs are measured labels and which are model predictions

Do not write “the model extracts features” without naming what the features represent and how they reach the final endpoint.

#### Evaluation and evidence

Read metrics in context:

- discrimination versus calibration versus clinical utility
- AUC, sensitivity, specificity, precision, recall, F1, confusion matrix
- OS, DFS, PFS, recurrence, progression, metastasis, censoring, and hazard ratio
- confidence intervals, uncertainty, subgroup analysis, and class imbalance
- internal testing versus scanner, institution, temporal, or external validation
- association versus causal effect
- prognosis versus treatment-benefit prediction

For each impressive number, ask: whose data, which unit, which denominator, which reference standard, which split, and which validation layer.

### 5. Figure-centered teaching protocol

Treat a figure as a compact argument, not as decoration. Before writing, inspect the complete PDF figure and complete figure legend, not only a crop. Then read the body-text paragraphs that introduce, cite, and interpret the figure.

For every figure, cover the following in proportion to its complexity.

#### Figure role

State why the figure exists:

- background or conceptual framework
- dataset and sampling design
- model architecture or workflow
- qualitative pathology recognition
- quantitative measurement
- spatial or graph analysis
- molecular or multimodal integration
- primary result
- ablation, subgroup, external validation, error analysis, or clinical translation

Say whether it is the authors' new experiment, a review synthesis, a reused example, or an adapted illustration.

#### Reading map

Tell the reader where to start and how to scan the figure. For example:

- workflow: input -> processing -> intermediate representation -> output -> validation
- multi-panel result: panel A defines the cohort or feature, panels B-C show performance or comparison, panel D checks robustness
- pathology image: tissue region -> cellular objects -> labels -> spatial relationship -> clinical association
- survival figure: start time -> event -> grouping -> curve or hazard estimate -> censoring and risk set

Do not invent panel roles that are not visible or supported by the legend.

#### Panel and element interpretation

For every panel that matters, identify:

- observation unit
- input and output
- comparison groups
- axes, units, scale, legend, color, symbols, line, band, marker, threshold, and annotation
- sample size and denominator if shown
- processing or statistic behind the visual
- the specific pattern the reader should notice

Explain why the element is present instead of merely transcribing its label.

#### Method connection

Connect the figure to the exact methods and results text:

- how labels were obtained
- how regions, cells, nuclei, spots, patches, or graphs were defined
- how aggregation or normalization was performed
- what reference standard was used
- what train/test or external cohort generated the panel
- how an endpoint or score was calculated

Do not import a common method from the field unless the paper actually used it.

#### Claim boundary

Explicitly separate:

1. directly visible observation
2. author's stated interpretation
3. reasonable teaching inference
4. claims requiring further evidence

Apply these guardrails:

- spatial adjacency or graph edges are not automatically biological interaction
- attention heatmaps are not complete mechanisms
- virtual staining or predicted expression is not measured IHC, IF, RNA, or DNA
- pseudotime is not real longitudinal lineage tracing
- a review's cited result is not the review's own experiment
- internal testing is not external or clinical validation
- prediction in a treated cohort is not proof of differential treatment benefit
- a significant association is not a causal effect

#### Figure takeaway and linkage

End with:

- one or two things the reader should remember
- how this figure connects to the previous and next figure or section
- what can genuinely transfer to the reader's project
- what cannot be transferred without new data or validation

For medical-AI figures, explain both the biomedical object and the algorithmic object. For example, a “tumor region” is not the same unit as a “tumor cell,” and a “spot” is not automatically a single cell.

#### Teaching additions

Use these only when they improve understanding:

- a small comparison table
- a formula in plain text or Unicode
- a numerical toy example explicitly labeled `教学示例，非论文数据`
- a simple static flowchart or SVG schematic
- a glossary card for a first-use term

Do not use teaching examples to fill missing paper results. Never present invented numbers as paper data.

### 6. Translate and explain screenshots

Use this output order:

1. screenshot location and PDF physical page
2. clipped-text recovery note
3. faithful Chinese translation
4. sentence-by-sentence explanation
5. figure or paragraph role in the paper
6. terms and hidden assumptions
7. evidence boundary and connection to the paper's main argument

For a figure legend, translate the legend fully before expanding its panels. For a conclusion paragraph, identify the limitations and future directions separately from the positive claims.

### 7. Write durable reading notes

For a paper note, prefer this structure:

- identity and article type
- one-sentence thesis
- research question and scope
- methods, data, and validation design
- figure-by-figure teaching
- main results and how to read them
- critical appraisal and limitations
- relation to the current project
- glossary
- reader Q&A supplement after the existing main sections

When adding a reader Q&A supplement in the local literature project:

- edit only the Markdown source
- append after section 9 and before the original evidence-directory footer
- use `<a id="10_qa"></a>` and `## 10. 读者问答补充（精读深挖）`
- keep the supplement focused on that paper and the current reading conversation
- do not add new images to a paper note unless the project rules explicitly allow it
- do not overwrite existing Q&A content
- regenerate that paper's HTML after editing

### 8. Project-specific commands

For the repository described by `CLAUDE.md`:

```powershell
# Render one changed article Markdown into HTML
python -c "import sys; sys.path.insert(0, 'tools'); from pathlib import Path; from finalize_literature_project import render_html; render_html(Path('阅读讲解_最终/XX_文件名.md'))"

# Audit the whole literature project
python tools/audit_literature_project.py

# Read the generated audit result in PowerShell
Get-Content 阅读讲解_最终/quality_report.json -Raw -Encoding UTF8
```

Do not run the full rebuild or `literature_project_tools.py prepare` casually. Full rebuild can erase hand-written Q&A supplements and `prepare` can remap article IDs.

### 9. Versioning and delivery

After any project-file modification:

1. inspect `git status` and `git diff`
2. run the relevant renderer, tests, and audit
3. stage only files belonging to the task
4. create a new Chinese commit with a clear message and the required co-author trailer
5. report the commit ID, checks performed, and whether the worktree is clean

Use incremental commits for long reading projects. Commit before risky bulk regeneration so hand-written explanations can be restored.

## Pitfalls

- Explaining from a screenshot alone when the crop hides the axis, legend, panel label, or full sentence.
- Expanding a caption without reading the body paragraph that cites the figure.
- Calling every large image a WSI, every local crop a biological region, or every patch an independent sample.
- Treating “quantitative” as self-explanatory without identifying the denominator, area, normalization, or count rule.
- Treating H&E morphology as a direct measurement of DNA, RNA, protein, immune function, or treatment response.
- Confusing a model's attention or heatmap with an explanation that has been mechanistically validated.
- Calling a statistically significant association a clinical effect or a causal mechanism.
- Writing a review's cited AUC, cohort size, or platform adoption as the review's own result.
- Using generic medical definitions when the paper defines a task-specific region or phenotype differently.
- Adding a long figure explanation to generated HTML while leaving the Markdown/configuration source unchanged.
- Running a destructive full rebuild before committing manual Q&A or figure explanations.
- Claiming validation or a commit without actually running the command and checking its output.

## Verification

A reading task is complete only when the following are true:

- The paper identity and article type are verified from the source.
- The main question, input, target, unit, model, output, and validation layer are explicit.
- Every in-scope figure has a role, reading map, panel explanation, evidence connection, claim boundary, and takeaway appropriate to its complexity.
- Screenshot translations recover clipped text from the source and preserve PDF physical pages.
- Paper-specific facts, teaching inference, and project transfer are labeled separately.
- Markdown/configuration sources and generated HTML agree.
- Local hard constraints pass, including banned-text, ASCII-question-mark, image-order, anchor, and source-reference checks where the repository defines them.
- The relevant audit or test command passes.
- Any file modification is saved in a new, precise Git commit, and the final worktree status is reported.
