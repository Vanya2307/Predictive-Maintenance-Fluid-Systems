# Notebook 03 - Planning Document

## Purpose
Notebook 03 moves from exploratory analysis to formal statistical comparison. Patterns identified in Notebook 02 are tested for statistical support when compared across failure-related or degradation-related groups. The two datasets are analyzed separately first and then interpreted together in light of the overall project question: whether condition-related and pre-failure sensor signatures can be identified across two different fluid-power systems.

---

## Hypotheses

The three hypotheses below define the scope of confirmatory testing in Notebook 03. They were committed to in writing before any formal hypothesis test was run, and they are not modified by the exploratory findings from Notebook 02.

Notebook 02 identified candidate signals through exploratory analysis (distributions, correlations, condition-stratified comparisons). Notebook 03 examines whether these candidates reach statistical significance and quantifies effect sizes. Variable selection within each hypothesis is informed by which signals the exploratory analysis flagged as worth testing.

### Hypothesis 1 - Failure-related sensor change within each dataset
Selected sensor variables differ measurably between normal and failure-related conditions within each dataset when the datasets are analyzed separately. 

In MetroPT-3, this hypothesis refers to differences between normal operating periods and pre-failure time windows before known failure events. In the hydraulic dataset, it refers to differences between feature values across labeled degradation states or between stable and unstable cycles.

### Hypothesis 2 - Cross-dataset similarity in physical behavior

The metro air compressor (MetroPT-3) and the hydraulic test rig show analogous failure-related behavior in their shared physical sensing concepts - especially pressure, temperature, and electrical load-related variables - even though the two systems differ in design, monitoring structure, and operating context. 

Because failure is represented differently in the two datasets, this hypothesis is tested by conceptual analogy rather than by direct one-to-one equivalence. In MetroPT-3, failure-related behavior is inferred from time windows preceding known incidents. In the hydraulic dataset, it is inferred from condition labels and cycle-level degradation structure.

### Hypothesis 3 - Reliability metrics as supporting evidence

Reliability-oriented measures such as MTBF and MTTR provide contextual support for the interpretation that sensor behavior does not change randomly, but is associated with meaningful periods of degradation, instability, or failure-related transition. These metrics are not treated as primary proof of the hypotheses above, but as supporting evidence that helps interpret the timing and operational significance of the detected sensor patterns.

---

## Planned interpretation rule

Support for the hypotheses will be evaluated from the combination of:

- statistical significance
- direction and size of effect
- consistency with the physical interpretation of the sensors
- convergence of evidence across the two datasets

The notebook should therefore not become only a list of p-values. 

Statistical results must be interpreted together with domain meaning and the earlier exploratory findings.

---

## Overall strategy

The notebook will not test every available variable. Instead, it will focus on a smaller set of variables and features selected from Notebook 02 based on:

- physical relevance
- clarity of separation in EDA
- interpretability
- usefulness for cross-dataset comparison

This notebook will be prepared first in a scratchpad workflow, where experiments are developed and refined before being moved into the final clean notebook.

---

## Dataset 1: MetroPT-3

### Analytical idea

MetroPT-3 is a continuous time-series dataset with known failure timestamps but without row-level degradation labels. The main strategy will be to compare selected variables in pre-failure windows against normal-operation windows.

### Candidate variables

- `TP2`
- `H1`
- `DV_pressure`
- `Oil_temperature`
- `Motor_current`
- optionally one binary or event-like variable such as `LPS` or `DV_eletric`

### Planned comparisons

- define fixed pre-failure windows before known failure events
- define comparison windows representing normal operation
- compare the selected variables statistically between the two groups

### Open decisions for scratchpad

- final pre-failure window length (for example: 1h, 6h, 12h, or 24h)
- exact definition of "normal" windows
- whether binary variables should be tested as proportions or activation rates rather than raw values
- whether continuous variables should be aggregated within windows before testing

### Expected statistical tests

- Mann-Whitney U test for two-group comparisons
- effect size reporting alongside p-values
- Bonferroni correction for multiple comparisons across tested variables

---

## Dataset 2: Hydraulic system

### Analytical idea

The hydraulic dataset is cycle-based and includes explicit condition labels. The main strategy will be to test whether the strongest feature–condition relationships identified in Notebook 02 remain statistically supported.

### Selected feature-condition pairs

#### Cooler condition
- `TS1_mean`
- `TS1_std`

#### Pump leakage
- `EPS1_mean`
- optionally `PS1_mean`

#### Stable vs unstable cycles
- `TS1_std`
- `VS1_std`
- optionally `PS1_std`
- optionally `EPS1_std`

### Lower-priority or weaker EDA results

- `valve_condition`
- `accumulator_pressure`

These may be included as weaker or contrastive findings, but they should not dominate the notebook.

### Open decisions for scratchpad

- testing strategy for multi-level condition labels: best-vs-worst contrast only, grouped binary contrast (`healthy` vs `degraded`), or omnibus test plus post-hoc pairwise comparisons
- whether weaker feature pairs should remain in the final notebook
- which effect-size metric is most appropriate

### Expected statistical tests

- Mann–Whitney U test for binary contrasts
- Kruskal–Wallis test for multi-level comparisons, if applicable
- post-hoc pairwise Mann–Whitney tests only if justified by the omnibus result
- effect-size reporting alongside p-values
- Bonferroni correction for multiple comparisons across tested variables

---

## Cross-dataset comparison

After the MetroPT-3 and hydraulic hypothesis tests are completed separately, the final part of Notebook 03 will compare the statistically supported findings across the two datasets. The comparison focuses on shared physical concepts - especially pressure, temperature, and electrical load-related behavior - rather than on exact variable equivalence.

The goal is to determine whether both systems show analogous condition-related or failure-related sensor changes, even though one dataset is time-series based and the other is cycle-based with explicit condition labels.

The comparison will be presented as a structured summary of which physical concepts show concordant findings, which diverge, and what those agreements or divergences suggest about the generalizability of pre-failure sensor behavior in fluid-power machinery.

---

## Reliability analysis

### Purpose

Reliability metrics will not be the primary evidence, but will provide supporting context for the interpretation of degradation and failure patterns.

### Planned metrics

- MTBF
- MTTR

### Notes

- MetroPT-3: based on known failure timestamps and maintenance events
- Hydraulic dataset: requires careful interpretation, because it is a controlled condition-monitoring dataset rather than a naturally occurring failure log

### Open question

Determine whether reliability metrics are fully meaningful for the hydraulic dataset, or whether they should be presented more cautiously as contextual rather than directly comparable measures.

---

## Statistical reporting plan

For each final test, report:

- variable or feature name
- comparison groups
- test used
- p-value
- corrected p-value (Bonferroni)
- effect size
- direction of difference
- short interpretation (one sentence)

Possible output format:

- one summary result table for MetroPT-3
- one summary result table for the hydraulic dataset
- one short cross-dataset interpretation block at the end

---

## Multiple-comparison handling
Where several variables or features are tested together, Bonferroni correction will be applied to control the family-wise error rate.

---

## Reminder

Notebook 03 should contain only finalized analyses.

All experimental code, trial windows, rough tests, discarded comparisons, and debugging should remain in the scratchpad notebook.

---


## Updates log

If any deviation from the plan becomes necessary during scratchpad testing, the change will be recorded here before inclusion in the final notebook.


**April 26** - Failure timestamps for MetroPT-3 obtained from the original UCI dataset documentation. Four "Air leak / High stress" events are reported with start and end times, replacing the earlier working assumption of using temporal gaps as failure proxies. The homogeneous failure mode (all four are the same type) is favorable for hypothesis testing because expected sensor signatures should be consistent across events.

The failure intervals will be stored as a separate project data file and loaded explicitly in Notebook 03 to ensure reproducible window construction.

**April 26** - Window-coverage diagnostic distinguished two causes of row-count variation: sampling-rate variation (full time coverage at slower sampling) and genuine truncation due to missing data. A coverage-threshold rule was added to the methodology: a failure event is included in a given window-length test only if both its pre-failure window and its normal window cover at least 90% of the requested duration. Under this rule at the 6h window length, Failure 4 is excluded because its normal window covers only 74.7% of the requested 6h. The number of retained failure events at each window length will be reported as part of the test results.

**April 26** - Per-event median summary at the 6h window length showed that pre-failure vs normal direction is not uniform across failure events for several MetroPT-3 variables. Oil_temperature shows the most consistent shift; TP2 shows partial consistency; H1, DV_pressure, and Motor_current show inconsistent direction across events. Because n=3 events per group leaves the event-level Mann-Whitney U with very limited statistical power, the planned interpretation rule applies directly: significance is one of four criteria, alongside direction consistency, effect magnitude, and physical plausibility. The event-level Mann-Whitney U will be computed and reported as supporting evidence rather than as a decisive test.

**April 26** - Window-length sweep across 1h/6h/12h/24h, applied to all five MetroPT-3 candidate variables, identified 6h as the working window length. Oil_temperature at 6h is the only (variable, window) combination showing perfect per-event direction consistency across all three retained failures.

Motor_current and DV_pressure show no robust pre-failure signature at any tested window length and are dropped from
primary testing. 

H1 shows partial consistency at shorter windows with a direction flip in one failure and is reported as a secondary finding.

TP2 shows two-of-three consistency with one flat case at 6h and is reported as a secondary finding. 

The 24h window shows direction inversion for Oil_temperature, indicating window dilution rather than amplification.

**April 26** - Final variable selection for MetroPT-3 formal Mann-Whitney testing: Oil_temperature, TP2, and H1. 

Motor_current was retained in the exploratory sweep but excluded from formal testing because its direction across failure events is inconsistent at every tested window length, suggesting it captures operating-regime variation rather than
pre-failure behavior. This decision keeps Hypothesis 2's coverage of both temperature and pressure physical concepts while reporting the electrical/load-related result transparently as a secondary finding.

