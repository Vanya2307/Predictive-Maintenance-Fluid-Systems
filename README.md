# Cross-Dataset Predictive Maintenance of Fluid-Power Systems

**Author:** Vanya Videva  
**Course:** Data Science, SoftUni  
**Date:** April 2026  

---

## Research Question

Can similar pre-failure or degradation-related sensor patterns be identified across two different fluid-power systems: a real metro train air compressor and a controlled hydraulic test rig?

## Project Overview

This project investigates predictive maintenance in two fluid-power systems with different monitoring structures. The first dataset, MetroPT-3, contains real operational sensor data from a metro train air compressor with documented failure intervals. The second dataset, Condition Monitoring of Hydraulic Systems, contains controlled cycle-based measurements with explicit degradation labels.

The project combines data cleaning, exploratory data analysis, formal nonparametric hypothesis testing, reliability-oriented context, and cross-dataset interpretation. The main goal is to determine whether condition-related sensor patterns can be detected within each system and whether any of the underlying physical concepts, especially temperature, pressure, and electrical or load-related behavior, show meaningful agreement across both datasets.

## Data Sources

- **Dataset 1: MetroPT-3**  
  Sensor data from a metro train air compressor in Porto, Portugal  
  UCI repository: https://archive.ics.uci.edu/dataset/791/metropt+3+dataset

- **Dataset 2: Condition Monitoring of Hydraulic Systems**  
  Multi-sensor condition-monitoring data from a hydraulic test rig  
  UCI repository: https://archive.ics.uci.edu/dataset/447/condition+monitoring+of+hydraulic+systems

## Repository Structure

- `notebooks/01_data_loading_and_cleaning.ipynb`  
  Data loading, validation, cleaning, and preprocessing

- `notebooks/02_exploratory_data_analysis.ipynb`  
  Exploratory analysis of distributions, correlations, temporal behavior, and condition-level patterns

- `notebooks/03_hypothesis_testing_and_reliability.ipynb`  
  Formal nonparametric testing, reliability context, and cross-dataset interpretation

- `notebooks/04_project_synthesis_and_reflection.ipynb`  
  Project-level synthesis, limitations, methodological reflection, and future directions

- `data/raw/`  
  Original downloaded datasets

- `data/processed/`  
  Cleaned and engineered datasets used in the notebooks

- `drafts/`  
  Planning notes and scratchpad materials used during development

## Setup

1. Download both datasets from the links above.
2. Place the MetroPT-3 files in `data/raw/MetroPT-3 Train Dataset/`
3. Place the hydraulic-system files in `data/raw/Predictive Maintenance Of Hydraulics System/`
4. Run the notebooks in order, starting with `notebooks/01_data_loading_and_cleaning.ipynb`

The later notebooks depend on processed outputs created in Notebook 01.

## Main Findings

**Hypothesis 1** - sensor variables differ measurably between normal and failure-related conditions - is supported in both datasets, but with substantially different strength. The hydraulic dataset produces strong formal evidence across all three tested condition labels. `cooler_condition` yields the strongest results in the entire project, with rank-biserial effect sizes above 0.95 across five of six pairwise comparisons. `pump_leakage` produces a robust result (`r = 0.62`), and `stable_flag` produces significant but operationally weak separation (`r = 0.19` and `0.10`). In MetroPT-3, formal tests do not reach significance because only three matched failure events survive the coverage filter, but `Oil_temperature` shows a clear directional pre-failure pattern and `H1` provides weaker supporting evidence.

**Hypothesis 2** - analogous behavior across both systems - is partially supported. Temperature is the strongest shared concept, showing condition-related shifts in both datasets. Pressure shows partial concordance. Electrical and load-related behavior is divergent between the two systems.

**Hypothesis 3** - reliability context supports the interpretation - is supported mainly through MetroPT-3. MTTR of approximately 21 hours and MTBF of approximately 28 days show that failures were infrequent but operationally meaningful.

## Methods Summary

Both datasets are analyzed using nonparametric statistical methods throughout, because sensor distributions vary substantially in shape across operating regimes and normality cannot be assumed.

Two-group comparisons use the Mann-Whitney U test. Multi-level comparisons use the Kruskal-Wallis omnibus test, followed by pairwise Mann-Whitney comparisons when the omnibus result is significant. Effect sizes are reported as rank-biserial correlations. The family-wise error rate is controlled by the Bonferroni correction.

For MetroPT-3, pre-failure windows are anchored to documented failure start times and compared against matched normal-operation windows. Because sensor rows within each window are temporally dependent, testing is conducted at the event-summary level using per-failure medians rather than individual rows.

## Limitations

The most significant constraint is the small number of matched failure events in MetroPT-3. After applying the coverage filter, only three failure events are retained, reducing formal inference to `n = 3` vs `n = 3` at the event level. This provides very low statistical power and means MetroPT-3 results should be treated as directional and exploratory-supportive rather than confirmatory.

Cross-dataset comparison is conducted by conceptual analogy rather than direct equivalence. MetroPT-3 is a continuous operational record with sparse failure annotations, while the hydraulic dataset is a controlled cycle-based experiment with explicit condition labels. This structural asymmetry limits the strength of generalizability conclusions.

## References

- Veloso, B., Ribeiro, R. P., Gama, J., & Pereira, P. M. (2022). *The MetroPT dataset for predictive maintenance*. Scientific Data, 9, 764.
- Helwig, N., Pignanelli, E., & Schütze, A. (2015). *Condition monitoring of a complex hydraulic system using multivariate statistics*. Proceedings of the 2015 IEEE International Instrumentation and Measurement Technology Conference (I2MTC), 210-215.
- Mann, H. B., & Whitney, D. R. (1947). *On a test of whether one of two random variables is stochastically larger than the other*. The Annals of Mathematical Statistics, 18(1), 50-60.
- Kruskal, W. H., & Wallis, W. A. (1952). *Use of ranks in one-criterion variance analysis*. Journal of the American Statistical Association, 47(260), 583-621.
