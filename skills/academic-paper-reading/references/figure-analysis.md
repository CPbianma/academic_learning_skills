# Figure-by-figure teaching checklist

Use this reference whenever a paper figure, table, graphical abstract, or screenshot is central to the user's question. The main Skill gives the workflow; this file gives the concrete depth bar.

## The minimum complete figure lesson

A complete explanation answers six questions:

1. **Why is this figure here** — which claim or transition in the paper does it support.
2. **How should it be read** — panel order, visual hierarchy, and what to inspect first.
3. **What exactly is shown** — unit, input, output, group, axis, legend, color, scale, statistic, and denominator.
4. **How was it produced** — labels, preprocessing, model step, aggregation, normalization, reference standard, and cohort split.
5. **What does it prove and not prove** — visible result, author interpretation, reasonable inference, and unsupported leap.
6. **What should the reader carry forward** — connection to the next figure, method, limitation, or project.

## Figure reading matrix

| Figure type | Must identify | Common overclaim to block |
| --- | --- | --- |
| Conceptual overview | hierarchy, arrows, categories, examples, whether synthesis or new method | treating a review framework as a validated unified model |
| Data and cohort design | cohort, sampling unit, inclusion, split, external set, time order | treating patches, spots, or slides as independent patients |
| Histology image | stain, magnification, tissue region, cell or region label, scale bar, real versus schematic | treating color or visual similarity as molecular identity |
| Segmentation or detection | object definition, mask, instance, class, annotation source, error type | calling every detected nucleus a fully identified cell |
| Model architecture | input, encoder, embedding, aggregator, supervision, output, inference path | saying “feature extraction” without explaining the information flow |
| WSI and MIL | patch selection, tile coordinates, bag, attention, slide aggregation, patient-level label | treating attention as a causal explanation or patch label as ground truth |
| Quantitative morphology | numerator, denominator, region, normalization, count, density, threshold | reporting a ratio without its denominator or spatial scope |
| Spatial or graph analysis | node, edge, radius, neighborhood, distance, region, graph-level output | treating graph edges as proven biological interaction |
| Multi-omics or virtual staining | measured modality, paired or registered data, predicted modality, reference assay | calling a prediction a real IHC, RNA, DNA, or protein measurement |
| ROC, PR, confusion matrix | positive class, threshold, reference standard, prevalence, confidence interval | treating AUC as calibration, clinical utility, or patient benefit |
| Survival and forest plot | start time, event, censoring, risk set, reference group, HR, CI | treating HR as survival probability or causal treatment effect |
| Ablation and subgroup | what changed, what stayed fixed, subgroup definition, multiplicity, interaction | treating one improved score as proof of mechanism |
| External validation | institution, scanner, time, disease spectrum, protocol, pre-specified endpoint | calling any held-out split external validation |
| Clinical workflow or trial | intervention, comparator, randomization unit, primary endpoint, process endpoint, patient outcome | treating documentation or workflow improvement as outcome improvement |

## Panel-by-panel method

For each panel, write one compact record before prose:

```text
Panel: A/B/C...
Unit: patient / slide / patch / cell / spot / graph / encounter
Input: what enters the analysis
Output: what is plotted or annotated
Groups: comparison and reference group
Visual grammar: axes, colors, symbols, line, band, scale bar, threshold
Statistic: count, ratio, density, AUC, HR, CI, p value, or qualitative map
Source: figure legend plus body paragraph and methods location
Observation: what can be seen directly
Boundary: what cannot be inferred
```

Then convert the records into Chinese teaching prose. Do not expose a blank template in the final note; fill it with evidence or omit fields that do not apply.

## For pathology and spatial figures

Always distinguish these layers:

```text
stain or modality
    -> tissue region
        -> cell or nucleus object
            -> label or phenotype
                -> spatial relation
                    -> slide or patient endpoint
```

A colored region may be a segmentation class, a tissue compartment, a predicted heatmap, or a display overlay. State which one the paper actually means. H&E morphology does not automatically identify a protein, immune subtype, transcript, or functional state. A cell neighborhood must include the operational rule used to define neighborhood.

## For charts and endpoints

Before reading a chart, write the data-generating question:

- composition: what fraction of what
- abundance: how many in what area
- discrimination: can the score rank positive above negative
- calibration: do predicted probabilities match observed frequencies
- survival: from what origin to which event, with what censoring
- treatment prediction: does the marker modify the contrast between treatments

For survival plots, explicitly check whether the x-axis is time, whether tick marks indicate censoring, whether numbers at risk are shown, and whether the endpoint is OS, DFS, PFS, recurrence, or another definition. For forest plots, identify the reference group and whether the interval crosses the null.

## For screenshots and clipped figures

1. Locate the full PDF page and complete legend.
2. Recover cropped panel letters, axis labels, units, legend entries, and footnote symbols.
3. Translate the complete caption before interpreting the crop.
4. Mark recovered text as source-completed when the screenshot itself did not show it.
5. Never use an unreadable color or missing edge as a reason to invent a label.

## Teaching layer and depth bar

The reader should be able to answer after reading:

- What biological or clinical object was analyzed.
- What the model or statistic did to it.
- What unit generated the plotted point, mask, line, or risk estimate.
- Which part came from actual measurement and which part came from prediction.
- What result changed the paper's argument.
- What validation is still missing.

Use a toy calculation only when it clarifies a denominator, aggregation rule, or metric. Label it exactly as `教学示例，非论文数据`. Do not create numerical examples for a paper's cohort, AUC, hazard ratio, or clinical effect unless the number is explicitly reported in the source.
