**For MetroPT-3 results section**

The formal MetroPT-3 hypothesis tests prioritize the strongest and most interpretable temperature and pressure signals identified during the window-length sweep: `Oil_temperature`, `TP2`, and `H1`. Electrical and load-related behavior was explored through `Motor_current` in the scratchpad analysis but showed inconsistent direction across the retained failure events at every tested window length. This finding is consistent with the operating-regime transition documented in Notebook 02 and indicates that `Motor_current` reflects general
operational variation rather than pre-failure behavior in this dataset. This negative result is reported transparently rather than excluded from consideration.




**For Hydraulic system**

## Hydraulic system: summary of formal results

Three condition labels were tested formally in the hydraulic dataset, with results that vary substantially in strength.

`cooler_condition` produced the strongest formal evidence in the entire project. Both `TS1_mean` and `TS1_std` separated the three cooler levels overwhelmingly (Kruskal-Wallis $p < 10^{-300}$), with rank-biserial effect sizes above 0.95 in five of the six pairwise comparisons. The signal is graded across all three degradation states, and the separation is physically interpretable as the thermal consequence of reduced cooler efficiency.

`pump_leakage` produced a robust but weaker result. `EPS1_mean` distinguished healthy from severe leakage with $p \approx 5 \times 10^{-89}$ and a large effect size of 0.62. The direction (severe > healthy in motor power) is consistent with the physical expectation that a degraded pump prompts higher motor load. The middle leakage state was not formally tested.

`stable_flag` produced statistically significant results that are operationally weak. Both `TS1_std` and `VS1_std` distinguished stable from unstable cycles ($p < 10^{-3}$), with the predicted direction (unstable > stable in within-cycle variability), but the rank-biserial effect sizes (0.19 and 0.10) indicate that individual unstable cycles overlap heavily with the stable distribution. The result confirms the descriptive Notebook 02 finding that cycle stability is a weak-to-moderate distinguisher.

Taken together, the three labels span a clear gradient of signal strength: the cooler-condition signal is dominant, the pump-leakage signal is robust, and the stable-flag signal is detectable but weak. All three results support Hypothesis 1 for the hydraulic dataset, though the operational meaningfulness of that support varies considerably across labels.


