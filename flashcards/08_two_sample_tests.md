+++
order = 8
tags = ["math", "statistics", "two-sample", "t-test", "welch", "paired", "f-test", "proportions"]
+++

# Statistics — Two-Sample Tests

## 8.1 Why Two-Sample Tests?

Q: Why do we need two-sample tests in addition to the one-sample tests from chapter 7?
A: Most real scientific questions compare two groups rather than compare one group to a fixed benchmark — does drug A lower blood pressure more than drug B, do men and women differ on a test, is method 1 more accurate than method 2. A two-sample test asks whether an observed difference between group means (or proportions, or variances) is larger than what sampling variability alone would produce.

Q: What is the generic null hypothesis for a two-sample test of means?
A: $H_0: \mu_1 = \mu_2$, equivalently $\mu_1 - \mu_2 = 0$, where $\mu_1$ is the population mean of group 1 and $\mu_2$ is the population mean of group 2. The test asks whether the observed difference $\bar{X}_1 - \bar{X}_2$ is consistent with a true difference of zero.

C: In a two-sample test, the parameter of interest is typically the [difference of population means] $\mu_1 - \mu_2$, rather than a single mean.

Q: Why do we focus the test on $\bar{X}_1 - \bar{X}_2$ rather than on $\bar{X}_1$ and $\bar{X}_2$ separately?
A: The quantity of scientific interest is the difference, not the individual means. Working directly with $\bar{X}_1 - \bar{X}_2$ as a single random variable lets us reuse the one-sample machinery: we just need its mean (which is $\mu_1 - \mu_2$) and its standard error.

## 8.2 Independent vs Paired Samples

C: Two samples are [independent] if the observations in one sample are unrelated to the observations in the other (e.g., different randomly chosen subjects in each group).

C: Two samples are [paired] (or matched) if each observation in one sample is naturally linked to exactly one observation in the other (e.g., before/after on the same subject, or twins).

Q: Why does the distinction between independent and paired samples matter for which test to use?
A: Independent samples have two separate sources of variability that add in the standard error formula. Paired samples share the subject, so within-subject variability cancels when you take differences — this usually gives a much smaller standard error and a more powerful test. Using the wrong test (e.g., independent t on paired data) throws away the pairing and inflates the standard error.

Q: Give an example of paired data and an example of independent data.
A: Paired: blood pressure of 20 patients measured before and after a drug (each patient is their own control). Independent: blood pressure of 20 patients on drug A and 20 different patients on drug B (no link between individuals across groups).

## 8.3 Two-Sample z-Test (Known Variances)

Q: When is the two-sample z-test for means appropriate?
A: When the two samples are independent, the population variances $\sigma_1^2$ and $\sigma_2^2$ are known, and either the populations are normal or the sample sizes are large enough for the CLT to apply to each sample mean. In practice, known variances are rare, so this test is primarily of theoretical importance.

C: For independent samples with known variances, the test statistic is $Z = \dfrac{(\bar{X}_1 - \bar{X}_2) - \Delta_0}{\sqrt{\sigma_1^2/n_1 + \sigma_2^2/n_2}}$, where $\bar{X}_i$ is the sample mean of group $i$, $\sigma_i^2$ is the known population variance, $n_i$ is the sample size, and $\Delta_0$ is the [hypothesized difference] $\mu_1 - \mu_2$ under $H_0$ (usually $0$).

Q: Why does the denominator of the two-sample z statistic add the two variances $\sigma_1^2/n_1$ and $\sigma_2^2/n_2$ rather than subtract them?
A: $\bar{X}_1$ and $\bar{X}_2$ are independent, so $\mathrm{Var}(\bar{X}_1 - \bar{X}_2) = \mathrm{Var}(\bar{X}_1) + \mathrm{Var}(\bar{X}_2)$. Variances always add for independent random variables, regardless of whether the means are added or subtracted.

C: Under $H_0$ with known variances, the standard error of $\bar{X}_1 - \bar{X}_2$ is $\mathrm{SE} = \sqrt{\sigma_1^2/n_1 + \sigma_2^2/n_2}$, and the statistic $Z$ has the [standard normal] distribution.

## 8.4 Pooled Two-Sample t-Test

Q: What assumption distinguishes the pooled t-test from the z-test?
A: The pooled t-test assumes the two populations have the same unknown variance $\sigma^2 = \sigma_1^2 = \sigma_2^2$ (equal variances assumption), and estimates this common variance from both samples. Because $\sigma$ is unknown and estimated, the sampling distribution is Student's $t$, not normal.

C: The [pooled variance] estimator combines both samples into one estimate of the common variance: $s_p^2 = \dfrac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}$, where $s_i^2$ is the sample variance of group $i$ and $n_i$ is the sample size.

Q: Why is $s_p^2$ a weighted average of $s_1^2$ and $s_2^2$ with weights $n_i - 1$?
A: Each sample variance $s_i^2$ is built from $n_i - 1$ degrees of freedom. Weighting by degrees of freedom gives more influence to the sample that carries more information about the common variance, and the resulting $s_p^2$ is an unbiased estimator of $\sigma^2$ under the equal-variance assumption.

C: The [pooled t-statistic] is $t = \dfrac{(\bar{X}_1 - \bar{X}_2) - \Delta_0}{s_p \sqrt{1/n_1 + 1/n_2}}$, where $\bar{X}_i$ is the sample mean of group $i$, $s_p$ is the pooled standard deviation, $n_i$ is the sample size, and $\Delta_0$ is the null difference.

C: Under $H_0$, the pooled t-statistic follows a $t$ distribution with [$n_1 + n_2 - 2$] degrees of freedom.

Q: Why is the degrees of freedom for the pooled t-test $n_1 + n_2 - 2$?
A: We lose one degree of freedom per sample when estimating each sample mean (to compute each $s_i^2$). Total observations are $n_1 + n_2$, and two means are estimated, leaving $n_1 + n_2 - 2$ degrees of freedom for estimating the common variance.

## 8.5 Welch's t-Test

Q: When should you use Welch's t-test instead of the pooled t-test?
A: When the two population variances cannot be assumed equal. Welch's test does not pool the variances; it uses each sample's own $s_i^2$ to estimate its own $\sigma_i^2$. This is the default two-sample t-test in most modern software (including R) because it is nearly as powerful as the pooled test when variances are equal, and much more reliable when they are not.

C: The [Welch t-statistic] is $t = \dfrac{(\bar{X}_1 - \bar{X}_2) - \Delta_0}{\sqrt{s_1^2/n_1 + s_2^2/n_2}}$, where $\bar{X}_i$ is the sample mean, $s_i^2$ is the sample variance of group $i$, $n_i$ is the sample size, and $\Delta_0$ is the null difference.

Q: How does Welch's standard error differ from the pooled standard error?
A: Welch uses $\sqrt{s_1^2/n_1 + s_2^2/n_2}$ — each group contributes its own variance estimate. The pooled version uses $s_p\sqrt{1/n_1 + 1/n_2}$, forcing a single shared variance estimate. When variances truly differ, Welch's SE is accurate and the pooled SE is biased.

C: Welch's t-statistic does not follow an exact $t$ distribution; its distribution is approximated by a $t$ with [Satterthwaite] (or Welch-Satterthwaite) degrees of freedom.

C: The [Satterthwaite degrees of freedom] formula is $\nu = \dfrac{\left(s_1^2/n_1 + s_2^2/n_2\right)^2}{\dfrac{(s_1^2/n_1)^2}{n_1 - 1} + \dfrac{(s_2^2/n_2)^2}{n_2 - 1}}$, where $s_i^2$ is the sample variance and $n_i$ is the sample size of group $i$.

Q: Why does Welch's test use a non-integer, data-dependent degrees of freedom?
A: The exact distribution of Welch's statistic is not a $t$ distribution — it is a linear combination of two independent chi-squares in the denominator. Satterthwaite's approximation matches the first two moments of this distribution to a $t$ distribution, producing a $\nu$ that depends on the observed variances and is generally non-integer.

Q: What are the bounds on Welch's $\nu$?
A: $\min(n_1-1, n_2-1) \le \nu \le n_1 + n_2 - 2$. It reduces to the smaller of the two degrees of freedom when one variance dominates, and to the pooled value when variances and sample sizes are equal.

## 8.6 Choosing Pooled vs Welch

Q: What is the simple rule of thumb for choosing pooled vs Welch?
A: Default to Welch. The pooled test only gains meaningful power when the equal-variance assumption is truly satisfied, and it fails badly when it is not. Welch is almost as good as pooled when variances are equal and much safer when they differ — so the downside of defaulting to Welch is tiny and the upside is large.

Q: Why is it a bad idea to "pre-test" for equal variances and then choose pooled vs Welch based on the result?
A: A two-stage procedure (test variances first, then choose test) inflates the overall Type I error rate and distorts the $p$-value of the final test. The pre-test is also underpowered when it matters most (small samples). Just using Welch unconditionally avoids these issues.

C: A common guideline: if the larger sample variance is more than about [4] times the smaller, Welch is clearly preferable to pooled.

## 8.7 Paired t-Test

Q: What is the key insight that turns a paired two-sample problem into a one-sample problem?
A: For each pair $i$, compute the difference $D_i = X_{1i} - X_{2i}$. The $D_i$ form a single sample of $n$ differences, and testing $\mu_1 = \mu_2$ is equivalent to testing $\mu_D = 0$ on this new sample. All the one-sample t-test machinery from chapter 7 applies directly.

C: For paired data $(X_{1i}, X_{2i})$ with $i = 1, \ldots, n$, the [paired differences] are $D_i = X_{1i} - X_{2i}$, and the paired t-test is the one-sample t-test applied to $D_1, \ldots, D_n$.

C: The paired t-statistic is $t = [\dfrac{\bar{D} - \Delta_0}{s_D / \sqrt{n}}]$, where $\bar{D}$ is the sample mean of the differences, $s_D$ is the sample standard deviation of the differences, $n$ is the number of pairs, and $\Delta_0$ is the null mean difference (usually $0$).

C: Under $H_0$, the paired t-statistic follows a $t$ distribution with [$n - 1$] degrees of freedom, where $n$ is the number of pairs (not the total number of observations).

Q: Why does the paired t-test usually have a smaller standard error than an independent t-test on the same data?
A: Variability between subjects is often larger than variability from the treatment itself. Taking within-subject differences cancels the between-subject variability entirely, leaving only the within-subject variability in $s_D$. If subjects differ a lot at baseline, this shrinks the SE dramatically and increases power.

## 8.8 When to Pair vs Not Pair (Design)

Q: When is it worth paying the cost of a paired design?
A: When pairs share a strong nuisance source of variability that you can remove by differencing — same subject over time, siblings, matched controls on age and sex, side-by-side field plots. If the pairing correlation is high, paired beats independent by a wide margin.

Q: When is pairing a bad idea?
A: When natural pairs don't exist or the correlation within pairs is weak. Forced pairing halves the effective sample size (you now have $n$ differences instead of $2n$ observations) and only pays off if the variance reduction from pairing exceeds this loss of degrees of freedom.

C: Pairing helps when the within-pair correlation $\rho$ is [positive] (ideally close to $1$), because the variance of the difference is $\sigma_1^2 + \sigma_2^2 - 2\rho\sigma_1\sigma_2$ — the covariance term subtracts only when $\rho > 0$.

Q: If two groups have the same variance $\sigma^2$ and within-pair correlation $\rho$, what is the variance of $D_i = X_{1i} - X_{2i}$?
A: $\mathrm{Var}(D_i) = 2\sigma^2(1 - \rho)$. When $\rho = 0$ (no pairing benefit) this equals $2\sigma^2$, the same as for independent pairs. When $\rho$ is close to $1$, variance collapses toward zero and pairing wins big.

## 8.9 Two-Proportion z-Test

Q: What question does the two-proportion z-test answer?
A: Whether two independent population proportions are equal: $H_0: p_1 = p_2$. Classic applications include A/B tests (does the new website convert at the same rate as the old?) and clinical trials (does the cure rate differ between drug and placebo?).

C: For two independent samples with $n_i$ trials and $X_i$ successes, the sample proportions are $\hat{p}_i = X_i / n_i$, and under $H_0$ the [pooled proportion] is $\hat{p} = \dfrac{X_1 + X_2}{n_1 + n_2}$.

C: The two-proportion z-statistic is $Z = \dfrac{\hat{p}_1 - \hat{p}_2}{\sqrt{\hat{p}(1 - \hat{p})(1/n_1 + 1/n_2)}}$, where $\hat{p}_i$ is the sample proportion of group $i$, $\hat{p}$ is the pooled proportion, and $n_i$ is the sample size. Under $H_0$, $Z$ is approximately [standard normal].

Q: Why does the test use the pooled $\hat{p}$ in the standard error rather than $\hat{p}_1$ and $\hat{p}_2$ separately?
A: Under $H_0$, $p_1 = p_2 = p$ — there is one common proportion. Pooling $\hat{p}$ uses all the data to estimate this common $p$, giving the most precise estimate of the null standard error. (For confidence intervals, which don't assume $p_1 = p_2$, the unpooled SE is used instead.)

Q: What sample-size condition makes the normal approximation valid for the two-proportion z-test?
A: Roughly $n_i \hat{p}_i \geq 10$ and $n_i(1 - \hat{p}_i) \geq 10$ in each group — at least about 10 successes and 10 failures per group. This ensures the binomial sampling distributions of $\hat{p}_1$ and $\hat{p}_2$ are each well-approximated by a normal.

## 8.10 F-Test for Equality of Two Variances

Q: What is the F-test for two variances used for?
A: To test $H_0: \sigma_1^2 = \sigma_2^2$ against a one- or two-sided alternative. Historically it was used to check the equal-variance assumption before a pooled t-test, but this pre-testing practice is now discouraged (see 8.6). The F-test is still useful when variance equality is itself the scientific question (e.g., comparing measurement precision of two instruments).

C: For independent normal samples, the F-statistic is $F = [s_1^2 / s_2^2]$, and under $H_0: \sigma_1^2 = \sigma_2^2$ it follows an $F$ distribution with $(n_1 - 1, n_2 - 1)$ degrees of freedom, where $s_i^2$ is the sample variance and $n_i$ is the sample size of group $i$. This is written $F \sim F_{n_1 - 1,\, n_2 - 1}$.

Q: Why is the F-test for variances especially sensitive to the normality assumption?
A: Unlike the t-test, which is robust to non-normality via the CLT, the F-test for variances relies on the exact chi-square distributions of $(n_i - 1)s_i^2 / \sigma_i^2$. Even mild departures from normality (heavy tails, skew) can severely distort the F distribution and give very wrong $p$-values.

C: The $F$ distribution with degrees of freedom $(\nu_1, \nu_2)$ is the distribution of $\dfrac{U_1 / \nu_1}{U_2 / \nu_2}$, where $U_1 \sim \chi^2_{\nu_1}$ and $U_2 \sim \chi^2_{\nu_2}$ are [independent].

Q: Why is the F-test one-sided by construction, even for a two-sided hypothesis?
A: The statistic $F = s_1^2/s_2^2$ is always positive, and large values indicate $\sigma_1^2 > \sigma_2^2$ while small values indicate $\sigma_1^2 < \sigma_2^2$. For a two-sided test, you either compute two one-sided tail probabilities and double the smaller, or you arrange the ratio so the larger variance is on top and compare to the upper tail only.

## 8.11 Assumptions and Robustness

Q: What are the assumptions of the independent two-sample t-test (pooled or Welch)?
A: (1) The two samples are independent of each other. (2) Observations within each sample are i.i.d. (3) Each population is approximately normal, or each sample size is large enough for the CLT. (4) For pooled only: equal population variances.

Q: How robust is the two-sample t-test to non-normality?
A: Very robust for moderately large samples ($n_1, n_2 \gtrsim 30$) thanks to the CLT applied to each sample mean. It is less robust with small samples, especially with skewed distributions or outliers. Heavy tails and outliers degrade power even when the Type I error is preserved.

Q: How robust is the two-sample t-test to unequal variances?
A: The pooled t-test is not robust to unequal variances when sample sizes are also unequal — Type I error can be badly inflated or deflated. Welch's t-test is robust to unequal variances by construction. This is the main argument for defaulting to Welch.

Q: How robust is the paired t-test to non-normality of the original data?
A: Quite robust, because only the differences $D_i$ need to be approximately normal (or the number of pairs large enough for CLT). Even if $X_{1i}$ and $X_{2i}$ are individually skewed, the differences can be approximately symmetric, especially when the two groups have similar shapes.

## 8.12 Two-Sample Tests as Regression/ANOVA (Preview)

Q: How does the independent two-sample t-test correspond to linear regression?
A: Regress the outcome $Y$ on an indicator variable $X = 1$ for group 1 and $X = 0$ for group 2: $Y = \beta_0 + \beta_1 X + \varepsilon$. Then $\beta_1 = \mu_1 - \mu_2$, and the t-test of $H_0: \beta_1 = 0$ is mathematically identical to the pooled two-sample t-test. This is the gateway to viewing all classical tests as special cases of regression.

Q: How does the two-sample t-test relate to one-way ANOVA?
A: One-way ANOVA generalizes the pooled two-sample t-test to $k \geq 2$ groups. For $k = 2$, ANOVA's F-statistic equals the square of the pooled t-statistic, and the two tests give identical $p$-values. ANOVA's F is $t^2$ in the two-group case.

Q: Why is recognizing "two-sample t-test = regression with an indicator" useful?
A: It unifies a growing zoo of tests under one framework. Once you see t-tests as regression, you can add covariates (controlling for confounders), handle more than two groups, model interactions, and apply everything you know about regression diagnostics — instead of learning a new test for each new situation.

C: In the regression formulation $Y = \beta_0 + \beta_1 X + \varepsilon$ with $X$ an indicator for group 1, the coefficient $\beta_1$ equals the [difference of means] $\mu_1 - \mu_2$.

## 8.13 Worked Problem: Welch's t-Test

P: Two independent samples of exam scores are collected. Group 1 (new teaching method): $n_1 = 12$, $\bar{X}_1 = 82.5$, $s_1 = 6.0$. Group 2 (traditional method): $n_2 = 15$, $\bar{X}_2 = 78.0$, $s_2 = 10.0$. Test at $\alpha = 0.05$ whether the new method produces a higher mean score, using Welch's t-test.

S:
**IDENTIFY**: Independent two-sample test of means. Sample variances differ substantially ($s_1^2 = 36$ vs $s_2^2 = 100$, ratio $\approx 2.8$) and sample sizes are unequal — Welch's t-test is appropriate. One-sided alternative: $H_1: \mu_1 > \mu_2$.

**PLAN**:
- State hypotheses: $H_0: \mu_1 = \mu_2$ vs $H_1: \mu_1 > \mu_2$, i.e., $\Delta_0 = 0$.
- Compute the Welch standard error $\mathrm{SE} = \sqrt{s_1^2/n_1 + s_2^2/n_2}$.
- Compute the Welch t-statistic $t = (\bar{X}_1 - \bar{X}_2)/\mathrm{SE}$.
- Compute the Satterthwaite degrees of freedom $\nu$.
- Compare $t$ to the one-sided critical value $t_{\alpha, \nu}$ and/or compute a $p$-value.

**EXECUTE**:
1. Variance contributions:
   - $s_1^2 / n_1 = 36 / 12 = 3.000$
   - $s_2^2 / n_2 = 100 / 15 \approx 6.667$
   - Sum: $3.000 + 6.667 = 9.667$
2. Standard error: $\mathrm{SE} = \sqrt{9.667} \approx 3.109$.
3. Test statistic: $t = \dfrac{82.5 - 78.0}{3.109} = \dfrac{4.5}{3.109} \approx 1.447$.
4. Satterthwaite degrees of freedom:
   $$\nu = \dfrac{(9.667)^2}{\dfrac{(3.000)^2}{11} + \dfrac{(6.667)^2}{14}} = \dfrac{93.45}{0.8182 + 3.175} = \dfrac{93.45}{3.993} \approx 23.4.$$
5. Critical value: for a one-sided test at $\alpha = 0.05$ with $\nu \approx 23$, $t_{0.05, 23} \approx 1.714$. The observed $t \approx 1.447 < 1.714$, so we fail to reject $H_0$.
6. $p$-value: $P(T_{23.4} > 1.447) \approx 0.08$, which exceeds $0.05$.

**EVALUATE**:
- Decision: fail to reject $H_0$ at $\alpha = 0.05$. The evidence is suggestive ($p \approx 0.08$) but not conclusive at the chosen significance level.
- Sanity check: the observed difference $\bar{X}_1 - \bar{X}_2 = 4.5$ is about $1.45$ standard errors — modest but not extreme, matching the $p$-value.
- Note: if we had wrongly used the pooled t-test, we would have gotten a different (and less trustworthy) SE because the variances differ by nearly a factor of three.
- Reporting: "Welch's t-test: $t(23.4) = 1.45$, one-sided $p = 0.08$; no significant evidence at $\alpha = 0.05$ that the new method raises mean scores."
