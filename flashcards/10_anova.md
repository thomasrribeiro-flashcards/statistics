+++
order = 10
subject = "Math"
tags = ["math", "statistics", "anova", "f-test", "sum-of-squares", "multiple-comparisons"]
+++

# Statistics — Analysis of Variance (ANOVA)

## 10.1 Why ANOVA?

Q: Why do we need a new procedure (ANOVA) to compare the means of three or more groups rather than just running many two-sample $t$-tests?
A: Running all pairwise $t$-tests inflates the family-wise Type I error rate. If each test uses $\alpha = 0.05$ and the tests were independent, the probability of at least one false positive across $m$ tests would be $1 - (1 - \alpha)^m$, which climbs quickly — for $k = 4$ groups there are 6 pairwise tests and the family-wise error exceeds 25%. ANOVA tests the global null ("all means equal") in a single test at level $\alpha$.

Q: Why is the inflated error rate from many pairwise $t$-tests called the "multiple comparisons problem"?
A: Each additional comparison gives another chance to reject a true null by chance alone. The more comparisons you run, the more likely at least one rejects spuriously — the error compounds across the family of tests, not within a single test.

C: For $m$ independent tests each at level $\alpha$, the family-wise Type I error rate is approximately $[1 - (1 - \alpha)^m]$, where $\alpha$ is the per-test significance level and $m$ is the number of tests.

Q: Before learning ANOVA, predict: if we want to compare three group means, what quantity might we look at to decide whether they differ "more than chance"?
A: We could compare the spread of the group means (between-group variability) to the spread of observations within each group (within-group variability). If between-group variability is much larger than within-group noise, the group means probably differ.

C: ANOVA stands for [Analysis of Variance], a procedure that tests equality of means by comparing variability between groups to variability within groups.

Q: Why is a procedure called "Analysis of Variance" when the goal is to compare means?
A: Under the null hypothesis that all group means are equal, two independent estimates of the common variance can be formed — one from variability between group means, one from variability within groups. If the group means actually differ, the between-group estimate inflates relative to the within-group estimate. So testing means reduces to comparing variances.

## 10.2 One-way ANOVA setup

C: A [one-way ANOVA] tests whether the means of a single quantitative response variable differ across the levels of one categorical factor with $k \geq 2$ groups.

C: In one-way ANOVA notation, $[k]$ denotes the number of groups (levels of the factor), $n_i$ is the sample size of group $i$, and $n = \sum_{i=1}^{k} n_i$ is the total sample size.

C: In one-way ANOVA, $[X_{ij}]$ denotes the $j$-th observation in group $i$, where $i = 1, \ldots, k$ and $j = 1, \ldots, n_i$.

C: The sample mean of group $i$ in one-way ANOVA is $\bar{X}_i = \frac{1}{n_i} \sum_{j=1}^{n_i} X_{ij}$, called the [group mean] (or treatment mean).

C: The overall mean (or [grand mean]) in one-way ANOVA is $\bar{\bar{X}} = \frac{1}{n} \sum_{i=1}^{k} \sum_{j=1}^{n_i} X_{ij}$, where $n$ is the total sample size across all $k$ groups.

Q: In a one-way ANOVA, is the grand mean $\bar{\bar{X}}$ the simple average of the group means $\bar{X}_i$?
A: Only when all groups have equal sample sizes. In general, $\bar{\bar{X}} = \sum_i n_i \bar{X}_i / n$ is a weighted average of the group means, weighted by $n_i$. Unbalanced designs (unequal $n_i$) make $\bar{\bar{X}} \neq \frac{1}{k}\sum_i \bar{X}_i$.

C: The null hypothesis in one-way ANOVA is $H_0:$ [$\mu_1 = \mu_2 = \cdots = \mu_k$], i.e., all $k$ population group means are equal.

C: The alternative hypothesis in one-way ANOVA is $H_1:$ [at least one $\mu_i$ differs] from the others (not all group means are equal).

Q: Why is the alternative hypothesis in ANOVA "at least one mean differs" rather than "all means differ"?
A: Rejecting $H_0$ only says the assumption of equal means fails somewhere — it could fail because one group differs while the rest agree, or because several differ. ANOVA is an omnibus test; it doesn't tell you which means differ, only that not all are equal.

## 10.3 ANOVA assumptions

C: The three standard one-way ANOVA assumptions are: (1) [normality] of the response within each group, (2) equal variances across groups (homoscedasticity), and (3) independence of observations.

C: The [homoscedasticity] assumption of ANOVA states that all $k$ groups share a common variance $\sigma^2$, i.e., $\text{Var}(X_{ij}) = \sigma^2$ for every group $i$.

Q: Why does ANOVA assume equal variances across groups?
A: The $F$-test pools within-group variability into a single estimate $MS_W$ of a common $\sigma^2$. If variances actually differ, the pooled estimate no longer reflects the variability of any single group, and the null distribution of $F$ ceases to be the claimed $F_{k-1, n-k}$.

Q: Why does ANOVA assume independence of observations?
A: Independence ensures that each observation contributes fresh information. Correlated observations (e.g., repeated measurements on the same subject) make the effective sample size smaller than $n$, so $MS_W$ underestimates the true variability and the $F$-test rejects too often.

Q: Why does ANOVA assume normality within each group?
A: The sampling distributions of $MS_B$ and $MS_W$ being chi-squared (so their ratio is $F$) rely on the underlying observations being normal. For moderate or large $n_i$, the Central Limit Theorem makes ANOVA fairly robust to mild non-normality, but heavy skew or outliers can distort the null distribution.

C: The full one-way ANOVA model is $X_{ij} = \mu_i + \varepsilon_{ij}$, where $\mu_i$ is the mean of group $i$ and the [errors] $\varepsilon_{ij}$ are independent $N(0, \sigma^2)$.

## 10.4 Partition of total sum of squares

Q: Why is the identity $SS_T = SS_B + SS_W$ the foundation of ANOVA?
A: It decomposes total variability in the data into two disjoint, interpretable pieces: variability explained by group differences ($SS_B$) and leftover variability within groups ($SS_W$). Comparing these two pieces is exactly how ANOVA decides whether group means differ.

C: The [total sum of squares] in one-way ANOVA is $SS_T = \sum_{i=1}^{k} \sum_{j=1}^{n_i} (X_{ij} - \bar{\bar{X}})^2$, the total squared deviation of every observation from the grand mean $\bar{\bar{X}}$.

C: The one-way ANOVA partition identity is $SS_T = [SS_B + SS_W]$, where $SS_B$ is the between-group sum of squares and $SS_W$ is the within-group sum of squares.

Q: Why does the cross-term vanish when expanding $(X_{ij} - \bar{\bar{X}})^2 = ((X_{ij} - \bar{X}_i) + (\bar{X}_i - \bar{\bar{X}}))^2$?
A: Expanding the square produces a cross-term $2 \sum_i \sum_j (X_{ij} - \bar{X}_i)(\bar{X}_i - \bar{\bar{X}})$. For each fixed $i$, $(\bar{X}_i - \bar{\bar{X}})$ is constant over $j$ and $\sum_j (X_{ij} - \bar{X}_i) = 0$ by definition of the group mean $\bar{X}_i$. So the cross-term is zero and only the two squared pieces survive.

C: The [degrees of freedom] partition in one-way ANOVA is $n - 1 = (k - 1) + (n - k)$, matching $SS_T = SS_B + SS_W$, where $n$ is total sample size and $k$ is the number of groups.

## 10.5 Between-group sum of squares

C: The [between-group sum of squares] is $SS_B = \sum_{i=1}^{k} n_i (\bar{X}_i - \bar{\bar{X}})^2$, where $n_i$ is the size of group $i$, $\bar{X}_i$ is the group mean, and $\bar{\bar{X}}$ is the grand mean.

Q: Why is each squared deviation in $SS_B$ weighted by $n_i$?
A: $SS_B$ measures total variability attributable to group differences across all $n$ observations. Every one of the $n_i$ observations in group $i$ shares the same group mean $\bar{X}_i$, so the deviation $(\bar{X}_i - \bar{\bar{X}})^2$ is "charged" $n_i$ times — once per observation in that group.

Q: What does $SS_B = 0$ mean?
A: Every group mean equals the grand mean: $\bar{X}_1 = \bar{X}_2 = \cdots = \bar{X}_k = \bar{\bar{X}}$. There is zero sample evidence of any mean difference, and $F = 0$.

C: $SS_B$ has $[k - 1]$ degrees of freedom, where $k$ is the number of groups.

Q: Why does $SS_B$ have exactly $k - 1$ degrees of freedom?
A: It is a sum of squared deviations of $k$ group means from the grand mean, but those $k$ deviations satisfy one linear constraint: $\sum_i n_i (\bar{X}_i - \bar{\bar{X}}) = 0$. One constraint removes one degree of freedom, leaving $k - 1$.

## 10.6 Within-group sum of squares

C: The [within-group sum of squares] is $SS_W = \sum_{i=1}^{k} \sum_{j=1}^{n_i} (X_{ij} - \bar{X}_i)^2$, where $X_{ij}$ is the $j$-th observation in group $i$ and $\bar{X}_i$ is the mean of group $i$.

Q: Why is $SS_W$ also called the "error" or "residual" sum of squares?
A: Under the model $X_{ij} = \mu_i + \varepsilon_{ij}$, the residuals are $X_{ij} - \bar{X}_i$, which estimate the errors $\varepsilon_{ij}$. So $SS_W$ aggregates squared residuals — variability left over after fitting each group's mean.

C: $SS_W$ has $[n - k]$ degrees of freedom, where $n$ is total sample size and $k$ is the number of groups.

Q: Why does $SS_W$ have exactly $n - k$ degrees of freedom?
A: Inside each group, $n_i$ observations contribute squared deviations from their own group mean, which uses one degree of freedom per group. So group $i$ contributes $n_i - 1$ and the total is $\sum_i (n_i - 1) = n - k$.

Q: What does $SS_W = 0$ mean?
A: Every observation equals its own group mean: there is zero variability within any group. All spread in the data is due to between-group differences.

## 10.7 Mean squares

C: The [between-group mean square] is $MS_B = \frac{SS_B}{k - 1}$, where $SS_B$ is the between-group sum of squares and $k - 1$ is its degrees of freedom.

C: The [within-group mean square] is $MS_W = \frac{SS_W}{n - k}$, where $SS_W$ is the within-group sum of squares and $n - k$ is its degrees of freedom.

Q: Why do we convert sums of squares to mean squares before comparing them?
A: $SS_B$ and $SS_W$ both grow with sample size and degrees of freedom, so their raw sizes aren't directly comparable. Dividing by degrees of freedom gives per-degree-of-freedom averages — two estimates of variance that can be compared on an equal footing.

Q: Under $H_0$ (all $\mu_i$ equal), what does $MS_W$ estimate?
A: The common within-group variance $\sigma^2$. This is true regardless of whether $H_0$ holds — $MS_W$ is always an unbiased estimator of $\sigma^2$ under the ANOVA model.

Q: Under $H_0$, what does $MS_B$ estimate?
A: Also $\sigma^2$. When all group means are truly equal, between-group variability arises only from sampling noise, and $E[MS_B] = \sigma^2$.

Q: Under $H_1$ (group means differ), how does $E[MS_B]$ change?
A: It inflates: $E[MS_B] = \sigma^2 + \frac{1}{k-1}\sum_i n_i(\mu_i - \bar{\mu})^2$, where $\bar{\mu}$ is the overall population mean. So $MS_B$ is biased upward by an amount that grows with the true mean differences.

## 10.8 F-statistic

C: The [one-way ANOVA F-statistic] is $F = \frac{MS_B}{MS_W}$, the ratio of between-group mean square to within-group mean square.

C: Under $H_0$ (all group means equal) and the ANOVA assumptions, the F-statistic follows an [$F_{k-1,\, n-k}$] distribution, with $k - 1$ numerator degrees of freedom and $n - k$ denominator degrees of freedom.

Q: Why is the ANOVA F-test always one-sided (upper tail only)?
A: Large values of $F$ indicate $MS_B \gg MS_W$, i.e., group means vary more than within-group noise — evidence against $H_0$. Small $F$ (close to 0 or even below 1) means groups are more similar than noise alone predicts, which is consistent with $H_0$. Only the upper tail signals mean differences.

C: Under $H_0$ in one-way ANOVA, $E[F] \approx [1]$ (more precisely, $\frac{n-k}{n-k-2}$ for $n - k > 2$), reflecting that both numerator and denominator estimate the same variance $\sigma^2$.

Q: What is the rejection rule for a one-way ANOVA F-test at significance level $\alpha$?
A: Reject $H_0$ if $F > F_{k-1,\, n-k,\, \alpha}$, where $F_{k-1,\, n-k,\, \alpha}$ is the upper-$\alpha$ critical value of the F-distribution with $k - 1$ and $n - k$ degrees of freedom. Equivalently, reject if the p-value $P(F_{k-1,n-k} > F_{\text{obs}}) < \alpha$.

## 10.9 Interpreting the F-test

Q: Intuitively, what does a large F-statistic tell you?
A: Between-group differences ($MS_B$) are large compared to within-group noise ($MS_W$). The group means are spread out more than we'd expect from random sampling alone, so it is unlikely all $\mu_i$ are equal.

Q: Intuitively, what does a small F-statistic (near 1 or below) tell you?
A: Between-group differences are about the same size as within-group noise. The observed variation in group means is consistent with pure sampling variability under $H_0$, so there is no evidence the population means differ.

Q: If a one-way ANOVA rejects $H_0$, what does it tell you — and what does it NOT tell you?
A: It tells you that not all $\mu_i$ are equal. It does NOT tell you which specific groups differ, how many differ, or by how much. Post-hoc procedures (Tukey HSD, Bonferroni-corrected pairwise tests) are needed to localize the differences.

Q: Can the one-way ANOVA F-test ever be equivalent to a two-sample $t$-test?
A: Yes. When $k = 2$, the F-statistic equals the square of the pooled two-sample $t$-statistic: $F = t^2$, and $F_{1, n-2} = t_{n-2}^2$. The two tests are algebraically identical for two groups.

## 10.10 Multiple comparisons

Q: Why are post-hoc tests needed after a significant ANOVA?
A: ANOVA only rejects the global null; it doesn't identify which group means differ. Pairwise comparisons are still needed to localize the effect, but those comparisons inherit the multiple-testing problem — so they must be done with a procedure that controls the family-wise error rate.

C: The [Bonferroni correction] controls the family-wise error rate by testing each of $m$ pairwise comparisons at level $\alpha / m$, where $\alpha$ is the desired family-wise significance level and $m$ is the number of comparisons.

Q: Why does Bonferroni divide $\alpha$ by $m$ rather than, say, by $\sqrt{m}$?
A: The union bound says the probability that at least one of $m$ tests makes a Type I error is at most the sum of the per-test error rates. Setting each to $\alpha/m$ bounds the family-wise error at $m \cdot \alpha/m = \alpha$. It's a conservative but simple bound.

Q: What is the main drawback of the Bonferroni correction?
A: It is conservative — the true family-wise error rate is often well below $\alpha$, at the cost of reduced power. With many comparisons, real differences can fail to reach the stricter $\alpha/m$ threshold.

C: [Tukey's HSD] (Honestly Significant Difference) is a post-hoc procedure that controls the family-wise error rate for all pairwise comparisons of group means by using the Studentized range distribution.

Q: Why is Tukey's HSD generally preferred over Bonferroni when comparing all pairs of group means?
A: Tukey exploits the joint distribution of pairwise differences (via the Studentized range), which is tighter than the union bound Bonferroni uses. For all pairwise comparisons with equal group sizes, Tukey is exactly calibrated and has more power than Bonferroni.

Q: When might Bonferroni be preferred over Tukey's HSD?
A: When only a small pre-specified subset of comparisons is of interest (not all pairs), or when the comparisons aren't all pairwise mean differences. Bonferroni is general-purpose and makes no assumption about the structure of the tests.

## 10.11 Two-way ANOVA

C: A [two-way ANOVA] tests the effects of two categorical factors simultaneously on a quantitative response, along with their possible interaction.

C: In two-way ANOVA, a [main effect] of a factor is the average effect of that factor on the response, averaged over the levels of the other factor.

C: In two-way ANOVA, an [interaction effect] means the effect of one factor on the response depends on the level of the other factor.

Q: Why does two-way ANOVA add an interaction term beyond the two main effects?
A: Because factors can combine non-additively. If drug A works only for men and drug B only for women, neither main effect (averaged over sex) captures the real story — the drug's effect depends on sex. The interaction term tests whether such dependence exists.

C: A two-way ANOVA with factors $A$ (with $a$ levels) and $B$ (with $b$ levels) partitions $SS_T$ into [$SS_A + SS_B + SS_{AB} + SS_W$], where $SS_A$ and $SS_B$ capture main effects, $SS_{AB}$ captures the interaction, and $SS_W$ is the residual within-cell variability.

Q: In a two-way ANOVA, how is each effect tested?
A: Each effect (factor $A$, factor $B$, and the $A \times B$ interaction) gets its own $F$-statistic, formed as $MS_{\text{effect}} / MS_W$, compared to an $F$ distribution with the appropriate degrees of freedom for that effect's numerator and $n - ab$ for the denominator (in a balanced complete design).

## 10.12 ANOVA and linear regression

Q: Why is ANOVA a special case of linear regression?
A: One-way ANOVA with $k$ groups is equivalent to a linear regression of the response on $k - 1$ dummy (indicator) variables encoding group membership, with one group as a reference. The regression's overall F-test for "all slopes are zero" is exactly the ANOVA F-test for "all means equal."

C: In one-way ANOVA re-expressed as regression, the model is $X_{ij} = \beta_0 + \beta_1 D_{1} + \cdots + \beta_{k-1} D_{k-1} + \varepsilon_{ij}$, where each [$D_\ell$] is an indicator (dummy) variable that equals 1 if the observation is in group $\ell$ and 0 otherwise, and $\beta_0$ is the mean of the reference group.

Q: In the dummy-variable regression formulation, what do the coefficients $\beta_\ell$ represent?
A: Each $\beta_\ell$ (for $\ell \geq 1$) is the difference between the mean of group $\ell$ and the mean of the reference group (say group $k$). So testing $\beta_\ell = 0$ tests whether group $\ell$ differs from the reference.

Q: Why is the regression F-test for overall model significance identical to the one-way ANOVA F-test?
A: Both partition the same total variability into the same two pieces. Regression splits $SS_T$ into $SS_{\text{reg}}$ (variability explained by the dummies) and $SS_{\text{res}}$, which for group-dummy regression equal $SS_B$ and $SS_W$ exactly. Dividing by the same degrees of freedom gives the same $F$.

Q: What is the advantage of viewing ANOVA through the regression lens?
A: It unifies ANOVA with other linear models — you can add continuous covariates (ANCOVA), interactions, and random effects in the same framework, and use familiar tools (coefficients, confidence intervals, diagnostic plots) instead of ANOVA-specific machinery.

## 10.13 Worked Problem: One-way ANOVA

P: A teacher compares test scores across three teaching methods. Method A: scores $\{85, 90, 88\}$. Method B: scores $\{78, 82, 80\}$. Method C: scores $\{92, 95, 94\}$. Perform a one-way ANOVA at $\alpha = 0.05$ to test whether mean scores differ across methods.

S:
**IDENTIFY**: One-way ANOVA with $k = 3$ groups, each of size $n_i = 3$, total $n = 9$. $H_0: \mu_A = \mu_B = \mu_C$ vs $H_1:$ at least one differs. Degrees of freedom: $k - 1 = 2$ (numerator), $n - k = 6$ (denominator).

**PLAN**:
- Compute each group mean $\bar{X}_i$ and the grand mean $\bar{\bar{X}}$.
- Compute $SS_B = \sum_i n_i (\bar{X}_i - \bar{\bar{X}})^2$.
- Compute $SS_W = \sum_i \sum_j (X_{ij} - \bar{X}_i)^2$.
- Compute $MS_B = SS_B / 2$ and $MS_W = SS_W / 6$.
- Compute $F = MS_B / MS_W$ and compare to $F_{2,6,\,0.05} \approx 5.14$.

**EXECUTE**:
1. Group means:
   - $\bar{X}_A = (85 + 90 + 88)/3 = 263/3 \approx 87.667$
   - $\bar{X}_B = (78 + 82 + 80)/3 = 240/3 = 80.000$
   - $\bar{X}_C = (92 + 95 + 94)/3 = 281/3 \approx 93.667$
2. Grand mean (equal sizes, so simple average):
   $$\bar{\bar{X}} = (263 + 240 + 281)/9 = 784/9 \approx 87.111$$
3. Between-group SS (each $n_i = 3$):
   - $(87.667 - 87.111)^2 \approx 0.309$
   - $(80.000 - 87.111)^2 \approx 50.568$
   - $(93.667 - 87.111)^2 \approx 42.975$
   - $SS_B = 3 \times (0.309 + 50.568 + 42.975) \approx 3 \times 93.852 \approx 281.56$
4. Within-group SS (deviations from each group mean):
   - A: $(85 - 87.667)^2 + (90 - 87.667)^2 + (88 - 87.667)^2 \approx 7.11 + 5.44 + 0.11 = 12.67$
   - B: $(78 - 80)^2 + (82 - 80)^2 + (80 - 80)^2 = 4 + 4 + 0 = 8.00$
   - C: $(92 - 93.667)^2 + (95 - 93.667)^2 + (94 - 93.667)^2 \approx 2.78 + 1.78 + 0.11 = 4.67$
   - $SS_W \approx 12.67 + 8.00 + 4.67 = 25.33$
5. Mean squares:
   - $MS_B = 281.56 / 2 \approx 140.78$
   - $MS_W = 25.33 / 6 \approx 4.22$
6. F-statistic:
   $$F = \frac{MS_B}{MS_W} \approx \frac{140.78}{4.22} \approx 33.35$$
7. Compare: $F_{2,6,\,0.05} \approx 5.14$. Since $33.35 \gg 5.14$, reject $H_0$ (p-value $\approx 0.0006$).

**EVALUATE**:
- Reject $H_0$: the three teaching methods do not all produce the same mean score.
- Sanity check the partition: $SS_T = \sum_{i,j}(X_{ij} - \bar{\bar{X}})^2$. Using $\bar{\bar{X}} \approx 87.111$, the sum of squared deviations across all 9 scores should be $SS_B + SS_W \approx 281.56 + 25.33 = 306.89$, matching direct computation.
- ANOVA alone does not say which methods differ. Given the means (B $\approx 80$, A $\approx 88$, C $\approx 94$), a Tukey HSD or Bonferroni-corrected pairwise comparison is the next step to identify significant pairs.
- The large $F$ (≈ 33) reflects that between-group variability ($MS_B \approx 141$) dwarfs within-group noise ($MS_W \approx 4$), so the group means are clearly spread far wider than sampling error would predict.
