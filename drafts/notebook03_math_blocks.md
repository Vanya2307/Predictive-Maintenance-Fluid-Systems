### Mann-Whitney U test

The Mann-Whitney U test is a non-parametric test of whether two
independent samples are drawn from the same distribution. Given samples $X = \{x_1, \ldots, x_{n_1}\}$ and $Y = \{y_1, \ldots, y_{n_2}\}$, all $n_1 + n_2$ observations are pooled and ranked. The test statistic is:

$$U_1 = \sum_{i=1}^{n_1} \sum_{j=1}^{n_2} S(x_i, y_j)$$

where $S(x_i, y_j) = 1$ if $x_i > y_j$, $0.5$ if $x_i = y_j$, and $0$ otherwise. The complementary statistic $U_2 = n_1 n_2 - U_1$, and the reported test statistic is $U = \min(U_1, U_2 $.

The null hypothesis $H_0$ states that $X$ and $Y$ are drawn from the same distribution. Under $H_0$, $U$ follows a known distribution from which the two-sided p-value is computed.

The Mann-Whitney U test does not assume normality and is robust to outliers, which makes it appropriate for sensor data where the distributional shape varies across operating regimes.


### Effect size: rank-biserial correlation

Statistical significance alone does not indicate the size of a
difference. The rank-biserial correlation $r$ is the natural effect size for Mann-Whitney U:

$$r = 1 - \frac{2U}{n_1 n_2}$$

where $U$ is the test statistic and $n_1, n_2$ are the group sizes. The value $r$ ranges from $-1$ to $+1$, where $0$ indicates no difference between groups, positive values indicate that the first group's values tend to exceed the second's, and negative values indicate the reverse.

Common interpretation thresholds: $|r| < 0.1$ negligible, $|r| < 0.3$ small, $|r| < 0.5$ medium, $|r| \geq 0.5$ large.



### Multiple-comparison correction

When $k$ hypothesis tests are conducted simultaneously at significance level $\alpha$, the family-wise error rate increases. The Bonferroni correction adjusts the per-test threshold to:

$$\alpha_{\text{corrected}} = \frac{\alpha}{k}$$

For the $k$ tests planned across both datasets, the corrected threshold replaces $\alpha = 0.05$ as the decision criterion for individual results.



### Kruskal-Wallis omnibus test

The Kruskal-Wallis test is a non-parametric extension of Mann-Whitney U to more than two independent groups. Given $k$ groups with sample sizes $n_1, n_2, \ldots, n_k$ and total sample size $N = \sum_{i=1}^{k} n_i$, all observations are pooled and ranked. The test statistic is:

$$H = \frac{12}{N(N+1)} \sum_{i=1}^{k} \frac{R_i^2}{n_i} - 3(N+1)$$

where $R_i$ is the sum of ranks for group $i$.

The null hypothesis $H_0$ states that all $k$ groups are drawn from the same distribution. Under $H_0$, $H$ approximately follows a chi-squared distribution with $k - 1$ degrees of freedom, from which the p-value is computed.

Like Mann-Whitney U, Kruskal-Wallis does not assume normality and is robust to outliers, which makes it appropriate for sensor features that vary across cycle-level operating regimes.


### Multiple-comparison correction

When $k$ hypothesis tests are conducted simultaneously at significance level $\alpha$, the family-wise error rate increases above $\alpha$. The Bonferroni correction adjusts the per-test threshold to:

$$\alpha_{\text{corrected}} = \frac{\alpha}{k}$$

Equivalently, raw p-values can be compared against the original $\alpha$ threshold after multiplying by $k$, with values exceeding 1 clamped at 1. For the $k = 5$ primary hydraulic tests planned in this notebook, the corrected threshold is $\alpha_{\text{corrected}} = 0.010$.

The Bonferroni correction is conservative - it controls the family-wise error rate strictly but reduces statistical power. It is appropriate when the cost of false positives is high relative to false negatives, which is the standard expectation for a confirmatory analysis.


### Reliability metrics

For a system with observed failure events indexed by $i = 1, \ldots, n$, each with start time $t_i^{\text{start}}$ and end time $t_i^{\text{end}}$:

$$\text{MTTR} = \frac{1}{n} \sum_{i=1}^{n} (t_i^{\text{end}} - t_i^{\text{start}})$$

$$\text{MTBF} = \frac{1}{n-1} \sum_{i=1}^{n-1} (t_{i+1}^{\text{start}} - t_i^{\text{end}})$$

MTTR (Mean Time To Repair) measures the average duration of failure events. MTBF (Mean Time Between Failures) measures the average gap between consecutive failures.
