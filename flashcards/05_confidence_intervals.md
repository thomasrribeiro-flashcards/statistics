+++
order = 5
subject = "Mathematics"
tags = ["math", "statistics", "confidence-interval", "pivot", "t-distribution", "sample-size"]
+++

# Statistics — Confidence Intervals

## 5.1 Why Confidence Intervals?

Q: Why is a point estimate alone insufficient for reporting an inference about a parameter?
A: A point estimate is a single number that almost certainly differs from the true parameter by some random amount. Reporting only the point estimate hides the sampling variability of the estimator and gives no indication of how precise the estimate is. A confidence interval attaches a range of plausible values whose width reflects that uncertainty.

Q: What does a confidence interval add to a point estimate?
A: A measure of uncertainty — a range of plausible parameter values consistent with the observed data — together with a stated confidence level $1 - \alpha$ that quantifies the long-run reliability of the procedure.

C: A [confidence interval] is a random interval $(L(\mathbf{X}), U(\mathbf{X}))$, computed from the sample $\mathbf{X}$, that covers the true parameter with specified probability.

C: The width of a confidence interval reflects the [precision] of the estimator: narrower intervals mean more precise estimates.

Q: Before seeing any formulas, predict: if we collect more data, should the confidence interval get narrower or wider (at fixed $\alpha$)?
A: Narrower. More data reduces the sampling variability of the estimator, so the range of parameter values consistent with the data shrinks.

## 5.2 Interpretation of a $(1-\alpha)$ Confidence Interval

Q: What is the frequentist definition of a $(1-\alpha)$ confidence interval for a parameter $\theta$?
A: A procedure producing random endpoints $L(\mathbf{X}), U(\mathbf{X})$ such that $P_\theta(L(\mathbf{X}) \le \theta \le U(\mathbf{X})) = 1 - \alpha$ for every value of $\theta$. The probability refers to repeated sampling: in the long run, a fraction $1-\alpha$ of such intervals cover the true $\theta$.

C: The [confidence level] of an interval procedure is $1 - \alpha$, where $\alpha$ is the probability that the random interval fails to cover the true parameter.

Q: Why is it WRONG to say "there is a 95% probability that $\theta$ lies in this specific observed interval"?
A: In the frequentist view $\theta$ is a fixed (unknown) constant and the observed interval is also fixed once the data are in hand — so the event "$\theta \in (l, u)$" is either true or false, with probability $0$ or $1$. The $95\%$ refers to the long-run coverage of the random procedure, not the specific realized interval.

Q: What is the correct interpretation of a realized 95% CI $(l, u)$?
A: If we were to repeat the sampling and interval construction many times, about 95% of the resulting intervals would contain the true parameter. For this particular interval we say we are "95% confident" that $\theta \in (l, u)$ — a statement about the procedure, not a probability about $\theta$.

C: In the frequentist framework, the randomness in $P(L \le \theta \le U) = 1-\alpha$ lies in the [endpoints] $L, U$, not in $\theta$.

Q: How does the Bayesian credible interval differ from a frequentist confidence interval?
A: A Bayesian credible interval treats $\theta$ as random (given a prior) and states $P(\theta \in (l, u) \mid \text{data}) = 1 - \alpha$ — a direct probability about $\theta$. A frequentist CI treats $\theta$ as fixed and only makes a long-run statement about the coverage of the random procedure.

## 5.3 Pivotal Quantity Method

C: A [pivotal quantity] (or pivot) is a function $Q(\mathbf{X}, \theta)$ of the data and the parameter whose distribution does NOT depend on $\theta$ (or any other unknown parameter).

Q: Why is a pivot useful for constructing confidence intervals?
A: Because its distribution is known and parameter-free, we can find fixed quantiles $q_{\alpha/2}$ and $q_{1-\alpha/2}$ such that $P(q_{\alpha/2} \le Q(\mathbf{X}, \theta) \le q_{1-\alpha/2}) = 1 - \alpha$. Algebraically inverting this probability statement to isolate $\theta$ produces a random interval with exact coverage $1 - \alpha$.

Q: Why must the distribution of a pivot NOT depend on the unknown parameter?
A: If the distribution depended on $\theta$, we could not choose numerical quantiles $q_{\alpha/2}, q_{1-\alpha/2}$ without already knowing $\theta$ — so we could not make a usable probability statement or invert it.

P: How do you construct a confidence interval using the pivotal quantity method?

S:
**IDENTIFY**: We want a $(1-\alpha)$ CI for an unknown parameter $\theta$ based on sample $\mathbf{X}$.

**PLAN**:
- Find a pivot $Q(\mathbf{X}, \theta)$ whose distribution does not depend on $\theta$.
- Pick quantiles $q_1, q_2$ from that known distribution with $P(q_1 \le Q \le q_2) = 1 - \alpha$ (typically symmetric: $q_1 = q_{\alpha/2}$, $q_2 = q_{1-\alpha/2}$).
- Solve the double inequality $q_1 \le Q(\mathbf{X}, \theta) \le q_2$ for $\theta$ to isolate it in the middle.

**EXECUTE**:
1. Check that $Q$ is monotone in $\theta$ (needed for clean inversion).
2. Rearrange algebraically: $q_1 \le Q(\mathbf{X}, \theta) \le q_2 \iff L(\mathbf{X}) \le \theta \le U(\mathbf{X})$.
3. Report $(L(\mathbf{X}), U(\mathbf{X}))$ as the $(1-\alpha)$ CI.

**EVALUATE**:
- By construction, $P_\theta(L \le \theta \le U) = 1 - \alpha$ exactly, for every $\theta$.
- Symmetric tail probabilities ($\alpha/2$ each side) minimize length for symmetric pivot distributions.
- Sanity-check width: it should shrink as sample size $n$ grows.

## 5.4 CI for the Mean of a Normal with Known $\sigma$

Q: What is the pivot used to build a CI for $\mu$ when sampling from a normal with KNOWN variance $\sigma^2$?
A: $Z = \dfrac{\bar{X} - \mu}{\sigma / \sqrt{n}} \sim N(0,1)$, where $\bar{X}$ is the sample mean, $\mu$ is the unknown population mean, $\sigma$ is the known population standard deviation, and $n$ is the sample size. Its distribution ($N(0,1)$) does not depend on $\mu$, so it is a pivot.

C: For a sample of size $n$ from $N(\mu, \sigma^2)$ with $\sigma$ known, a $(1-\alpha)$ CI for $\mu$ is $\bar{X} \pm [z_{\alpha/2}] \cdot \sigma / \sqrt{n}$, where $z_{\alpha/2}$ is the upper $\alpha/2$ quantile of the standard normal.

C: In the known-$\sigma$ normal-mean CI $\bar{X} \pm z_{\alpha/2}\,\sigma/\sqrt{n}$, the quantity $\sigma/\sqrt{n}$ is the [standard error] of $\bar{X}$.

Q: In $\bar{X} \pm z_{\alpha/2}\,\sigma/\sqrt{n}$, define each symbol.
A: $\bar{X}$ is the sample mean; $z_{\alpha/2}$ is the value such that $P(Z > z_{\alpha/2}) = \alpha/2$ for $Z \sim N(0,1)$; $\sigma$ is the (known) population standard deviation; $n$ is the sample size. The term $z_{\alpha/2}\,\sigma/\sqrt{n}$ is called the margin of error.

Q: For a 95% CI using the normal pivot, what is $z_{\alpha/2}$?
A: $z_{0.025} \approx 1.96$.

C: The [margin of error] of a $(1-\alpha)$ CI is the half-width of the interval; for $\bar{X} \pm z_{\alpha/2}\sigma/\sqrt{n}$ it equals $z_{\alpha/2}\,\sigma/\sqrt{n}$.

Q: Why does the CI for $\mu$ under known $\sigma$ remain valid (at least approximately) even if the data are not exactly normal, when $n$ is large?
A: By the Central Limit Theorem, $\bar{X}$ is approximately normal for large $n$ regardless of the underlying distribution (with finite variance), so the pivot $Z$ is approximately $N(0,1)$ and the interval has approximately correct coverage.

## 5.5 CI for the Mean with Unknown $\sigma$

Q: When $\sigma$ is unknown, why can't we just substitute the sample standard deviation $s$ into the $z$-based formula?
A: Plugging $s$ into $\bar{X} \pm z_{\alpha/2} s/\sqrt{n}$ replaces the constant $\sigma$ with a random quantity. The resulting statistic no longer has an $N(0,1)$ distribution — it has heavier tails — so using $z$-quantiles undercovers the true mean. We need a pivot that accounts for the extra randomness of $s$.

C: For a sample of size $n$ from $N(\mu, \sigma^2)$ with $\sigma$ UNKNOWN, the pivot $T = \dfrac{\bar{X} - \mu}{s / \sqrt{n}}$ follows a [Student's $t$] distribution with $n - 1$ degrees of freedom, where $s$ is the sample standard deviation.

C: For a normal sample with $\sigma$ unknown, a $(1-\alpha)$ CI for $\mu$ is $\bar{X} \pm [t_{\alpha/2, n-1}] \cdot s/\sqrt{n}$, where $t_{\alpha/2, n-1}$ is the upper $\alpha/2$ quantile of the $t$-distribution with $n-1$ degrees of freedom.

Q: Define every symbol in $\bar{X} \pm t_{\alpha/2, n-1}\,s/\sqrt{n}$.
A: $\bar{X}$ is the sample mean; $s = \sqrt{\frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X})^2}$ is the sample standard deviation; $n$ is the sample size; $n - 1$ is the degrees of freedom; $t_{\alpha/2, n-1}$ is the value satisfying $P(T > t_{\alpha/2, n-1}) = \alpha/2$ for $T \sim t_{n-1}$.

Q: What degrees of freedom does the $t$-based CI for $\mu$ use, and why $n - 1$?
A: $n - 1$. One degree of freedom is "used up" estimating $\mu$ by $\bar{X}$ when computing $s^2 = \frac{1}{n-1}\sum(X_i - \bar{X})^2$; the residuals $X_i - \bar{X}$ satisfy one linear constraint (they sum to zero), leaving $n - 1$ independent pieces of information.

P: Build a $(1-\alpha)$ confidence interval for the mean $\mu$ of a normal population with unknown variance.

S:
**IDENTIFY**: Data $X_1, \ldots, X_n \stackrel{iid}{\sim} N(\mu, \sigma^2)$ with both $\mu$ and $\sigma^2$ unknown. Goal: $(1-\alpha)$ CI for $\mu$.

**PLAN**:
- Use the $t$-pivot $T = (\bar{X} - \mu)/(s/\sqrt{n}) \sim t_{n-1}$.
- Choose two-sided quantile $t^* = t_{\alpha/2, n-1}$.
- Invert $P(-t^* \le T \le t^*) = 1 - \alpha$ for $\mu$.

**EXECUTE**:
1. Compute $\bar{X} = \frac{1}{n}\sum X_i$.
2. Compute $s^2 = \frac{1}{n-1}\sum (X_i - \bar{X})^2$ and $s = \sqrt{s^2}$.
3. Look up $t^* = t_{\alpha/2, n-1}$ for the chosen confidence level.
4. Form the interval: $\bar{X} \pm t^* \cdot s/\sqrt{n}$.

**EVALUATE**:
- Coverage is exactly $1 - \alpha$ under the normality assumption.
- Check robustness: for moderate $n$ and mildly non-normal data, coverage remains approximately correct (CLT + $t$ is robust).
- Sanity check: as $n \to \infty$, $t_{\alpha/2, n-1} \to z_{\alpha/2}$, so the $t$-interval converges to the $z$-interval.

## 5.6 Why $t$ Instead of $z$ When $\sigma$ Unknown

Q: Why does the $t$-distribution have heavier tails than the standard normal?
A: The denominator $s/\sqrt{n}$ in $T = (\bar{X}-\mu)/(s/\sqrt{n})$ is itself random (it estimates $\sigma/\sqrt{n}$). Small realized values of $s$ inflate the ratio, producing extreme values more often than if the denominator were the fixed constant $\sigma/\sqrt{n}$. This extra variability shows up as heavier tails.

Q: What happens to the $t_{n-1}$ distribution as $n \to \infty$?
A: It converges to the standard normal $N(0,1)$. Intuitively, $s \to \sigma$ as $n \to \infty$, so the extra randomness in the denominator vanishes and the $t$-pivot becomes indistinguishable from the $z$-pivot.

C: For small $n$, the $t$-based CI is [wider] than the (invalid) $z$-based CI using $s$, reflecting the extra uncertainty from estimating $\sigma$.

Q: If someone uses $\bar{X} \pm z_{\alpha/2} s/\sqrt{n}$ with small $n$, what goes wrong?
A: The actual coverage is LESS than $1 - \alpha$ — the interval is too narrow because $z_{\alpha/2} < t_{\alpha/2, n-1}$. For small $n$ the undercoverage can be substantial.

## 5.7 CI for a Proportion

C: For a sample of $n$ Bernoulli$(p)$ trials, the sample proportion is $\hat{p} = [X/n]$, where $X$ is the observed number of successes.

Q: What is the (approximate) variance of $\hat{p}$, and how is this used for CIs?
A: $\mathrm{Var}(\hat{p}) = p(1-p)/n$. For large $n$, the CLT gives $\hat{p} \approx N(p, p(1-p)/n)$, which is the basis for all common proportion CIs.

C: The [Wald confidence interval] for $p$ is $\hat{p} \pm z_{\alpha/2}\sqrt{\hat{p}(1-\hat{p})/n}$, where $\hat{p}$ is the sample proportion and $n$ is the sample size.

Q: What is a known weakness of the Wald interval for proportions?
A: It performs poorly when $\hat{p}$ is near 0 or 1, or when $n$ is small — coverage can drop far below the nominal $1 - \alpha$. In the extreme cases $\hat{p} = 0$ or $\hat{p} = 1$ the interval collapses to a single point.

C: The [Wilson score interval] for $p$ inverts the test statistic $Z = (\hat{p}-p)/\sqrt{p(1-p)/n}$ directly, solving $|Z| \le z_{\alpha/2}$ for $p$ rather than plugging $\hat{p}$ into the variance.

Q: Why does the Wilson score interval generally outperform the Wald interval?
A: It does not substitute $\hat{p}$ for $p$ in the standard error; instead it solves a quadratic in $p$ using the true unknown $p$ in the variance. This keeps coverage close to nominal even for small $n$ and extreme $\hat{p}$, and the interval never goes outside $[0,1]$.

C: The [Agresti-Coull interval] is a Wald-type interval applied after the "add-two-successes-and-two-failures" adjustment: $\tilde{p} = (X + 2)/(n + 4)$, then $\tilde{p} \pm z_{\alpha/2}\sqrt{\tilde{p}(1-\tilde{p})/\tilde{n}}$, where $\tilde{n} = n + 4$.

Q: When is Agresti-Coull especially recommended over plain Wald?
A: For small to moderate $n$ and for $\hat{p}$ near 0 or 1 — exactly where Wald fails. Agresti-Coull keeps Wald's simple form while shrinking $\hat{p}$ toward $1/2$, which restores coverage close to nominal.

## 5.8 CI for a Normal Variance via Chi-square

C: For a sample of size $n$ from $N(\mu, \sigma^2)$, the pivot $\dfrac{(n-1)s^2}{\sigma^2}$ has a [chi-square] distribution with $n-1$ degrees of freedom, where $s^2$ is the sample variance.

Q: Why is the chi-square distribution the right reference for $(n-1)s^2/\sigma^2$?
A: $s^2$ is a scaled sum of squared standardized normal deviations with one linear constraint ($\sum (X_i - \bar{X}) = 0$). A sum of $n-1$ independent squared standard normals is, by definition, $\chi^2_{n-1}$, and the constraint reduces the count from $n$ to $n-1$.

Q: Invert the chi-square pivot to get a $(1-\alpha)$ CI for $\sigma^2$. Why are the chi-square quantiles "swapped" in the formula?
A: From $\chi^2_{1-\alpha/2, n-1} \le (n-1)s^2/\sigma^2 \le \chi^2_{\alpha/2, n-1}$, inverting to isolate $\sigma^2$ flips the inequality direction and swaps the quantiles into the denominators: $\left(\dfrac{(n-1)s^2}{\chi^2_{\alpha/2, n-1}},\; \dfrac{(n-1)s^2}{\chi^2_{1-\alpha/2, n-1}}\right)$.

C: A $(1-\alpha)$ CI for a normal variance $\sigma^2$ is $\left(\dfrac{(n-1)s^2}{\chi^2_{\alpha/2, n-1}},\; \dfrac{(n-1)s^2}{\chi^2_{1-\alpha/2, [n-1]}}\right)$, where $s^2$ is the sample variance and $n$ is the sample size.

Q: In the chi-square-based variance CI, define each symbol.
A: $n$ is the sample size; $s^2 = \frac{1}{n-1}\sum(X_i - \bar{X})^2$ is the sample variance; $\chi^2_{\alpha/2, n-1}$ is the upper $\alpha/2$ quantile (i.e., $P(\chi^2_{n-1} > \chi^2_{\alpha/2, n-1}) = \alpha/2$); $\chi^2_{1-\alpha/2, n-1}$ is the lower $\alpha/2$ quantile.

Q: Why is the variance CI asymmetric around $s^2$, unlike the $z$- and $t$-based mean CIs?
A: The chi-square distribution itself is skewed (right-tailed) for small $n-1$, so its upper and lower quantiles are not symmetric about the mean. Inverting yields an asymmetric interval for $\sigma^2$.

Q: Why is the normal-variance CI NOT robust to departures from normality?
A: Unlike the $t$-interval for $\mu$, the chi-square pivot relies heavily on the normality assumption. The distribution of $(n-1)s^2/\sigma^2$ can deviate substantially from $\chi^2_{n-1}$ under heavy tails or skewness, and the CLT does not rescue it for variance inference.

## 5.9 CI for a Difference of Two Means

Q: What sampling design distinguishes the "independent samples" case from the "paired" case for two-means inference?
A: Independent samples: two separate groups with independent observations $X_1,\ldots, X_{n_1}$ and $Y_1, \ldots, Y_{n_2}$. Paired: each pair $(X_i, Y_i)$ is matched (same subject, twin, before/after), so the relevant data are the within-pair differences $D_i = X_i - Y_i$.

C: For two independent normal samples with equal variance $\sigma^2$, the [pooled variance] is $s_p^2 = \dfrac{(n_1-1)s_1^2 + (n_2-1)s_2^2}{n_1 + n_2 - 2}$, where $s_1^2, s_2^2$ are the two sample variances and $n_1, n_2$ the two sample sizes.

C: Under equal variances, a $(1-\alpha)$ CI for $\mu_1 - \mu_2$ is $(\bar{X}_1 - \bar{X}_2) \pm t_{\alpha/2,\, n_1+n_2-2}\, s_p\sqrt{\tfrac{1}{n_1} + \tfrac{1}{[n_2]}}$, where $s_p$ is the pooled standard deviation.

Q: When variances are NOT assumed equal, what CI is used for $\mu_1 - \mu_2$ in the independent case?
A: Welch's interval: $(\bar{X}_1 - \bar{X}_2) \pm t_{\alpha/2, \nu}\sqrt{s_1^2/n_1 + s_2^2/n_2}$, where the degrees of freedom $\nu$ are given by the Welch-Satterthwaite approximation $\nu \approx \frac{(s_1^2/n_1 + s_2^2/n_2)^2}{(s_1^2/n_1)^2/(n_1-1) + (s_2^2/n_2)^2/(n_2-1)}$.

Q: For paired data, what CI is used for $\mu_D = \mu_X - \mu_Y$?
A: Treat the $n$ differences $D_i = X_i - Y_i$ as a single sample and apply the one-sample $t$ CI: $\bar{D} \pm t_{\alpha/2, n-1}\, s_D/\sqrt{n}$, where $\bar{D}$ is the mean and $s_D$ the standard deviation of the $D_i$'s, and $n$ is the number of pairs.

Q: Why is the paired analysis usually more powerful than the independent-samples analysis when the pairing is informative?
A: Pairing removes between-subject variability: the within-pair differences $D_i$ have smaller variance than the difference of independent means, shrinking the standard error and narrowing the CI.

## 5.10 Sample Size Determination

Q: Why might a researcher compute a required sample size BEFORE collecting data?
A: To guarantee that the confidence interval will be precise enough to answer the question of interest — i.e., that the margin of error is no larger than a pre-specified tolerance $E$. This prevents the waste of an underpowered study and supports study design and budgeting.

C: The [margin of error] for $\mu$ with known $\sigma$ is $E = z_{\alpha/2}\,\sigma/\sqrt{n}$, where $E$ is the desired half-width, $z_{\alpha/2}$ is the normal quantile, $\sigma$ is the population standard deviation, and $n$ is the required sample size.

C: Solving $E = z_{\alpha/2}\sigma/\sqrt{n}$ for $n$ gives the required sample size $n = [\lceil (z_{\alpha/2}\sigma/E)^2 \rceil]$, where $\lceil \cdot \rceil$ denotes rounding up.

P: Determine the required sample size $n$ to estimate a proportion $p$ within margin of error $E$ with confidence $1-\alpha$.

S:
**IDENTIFY**: Sample-size computation for a Wald-type proportion CI with target margin of error $E$.

**PLAN**:
- Margin of error for proportion: $E = z_{\alpha/2}\sqrt{p(1-p)/n}$.
- Solve for $n$: $n = z_{\alpha/2}^2\, p(1-p)/E^2$.
- Since $p$ is unknown, use a planning value: either a prior estimate $p_0$ or the worst-case $p = 1/2$ (maximizes $p(1-p) = 1/4$).

**EXECUTE**:
1. Choose confidence level: look up $z_{\alpha/2}$ (e.g., $1.96$ for $95\%$).
2. Pick a planning value $p^*$ (use $p^* = 0.5$ if none is available).
3. Compute $n = z_{\alpha/2}^2\, p^*(1-p^*)/E^2$.
4. Round UP to the nearest integer.

**EVALUATE**:
- Using $p^* = 0.5$ gives a conservative (larger) sample size — safe if $p$ is truly unknown.
- Halving the margin of error $E$ quadruples the required $n$.
- Sanity-check: the formula gives $n \to \infty$ as $E \to 0$ and $n$ decreases as $\alpha$ increases (less stringent confidence).

Q: Why does halving the desired margin of error roughly quadruple the required sample size?
A: Because $n \propto 1/E^2$ — the margin scales as $1/\sqrt{n}$, so reducing $E$ by a factor of 2 requires increasing $n$ by a factor of $2^2 = 4$.

Q: Why is $p = 1/2$ the conservative choice in proportion sample-size calculations?
A: The function $p(1-p)$ is maximized at $p = 1/2$, giving the largest possible variance $1/4$. Designing for this worst case guarantees the target margin of error regardless of the true $p$.

## 5.11 Large-Sample CI via CLT for General MLEs

Q: Under regularity conditions, what is the asymptotic distribution of a maximum likelihood estimator $\hat{\theta}_n$?
A: $\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} N\bigl(0, I(\theta)^{-1}\bigr)$, where $I(\theta)$ is the Fisher information per observation. Equivalently $\hat{\theta}_n \approx N(\theta, [nI(\theta)]^{-1})$ for large $n$.

C: A large-sample $(1-\alpha)$ CI based on the asymptotic normality of the MLE is $\hat{\theta} \pm z_{\alpha/2}/\sqrt{n [I(\hat{\theta})]}$, where $\hat{\theta}$ is the MLE and $I(\hat{\theta})$ is the Fisher information evaluated at the MLE.

Q: Why is it acceptable to plug $I(\hat{\theta})$ in place of $I(\theta)$ in the large-sample CI?
A: By consistency, $\hat{\theta} \to \theta$ in probability as $n \to \infty$, and continuity of $I$ implies $I(\hat{\theta}) \to I(\theta)$. Slutsky's theorem then guarantees that replacing $I(\theta)$ with $I(\hat{\theta})$ preserves the asymptotic $N(0,1)$ distribution of the pivot.

Q: What does "approximate" mean for a large-sample CI?
A: The stated coverage $1 - \alpha$ holds only in the limit $n \to \infty$. For finite $n$ the actual coverage is approximately, but not exactly, $1 - \alpha$; the approximation improves as $n$ increases and as the likelihood becomes more regular.

Q: Name two assumptions required for the large-sample MLE CI to be valid.
A: (1) The usual regularity conditions on the likelihood (interior true parameter, identifiability, sufficient smoothness so that Fisher information exists and the log-likelihood is differentiable). (2) Large enough $n$ for the asymptotic normal approximation to be accurate.

## 5.12 Bootstrap Confidence Intervals

Q: What is the basic idea behind the bootstrap for CIs?
A: Approximate the sampling distribution of an estimator $\hat{\theta}$ by repeatedly resampling WITH replacement from the observed data. Each resample produces a bootstrap replicate $\hat{\theta}^*$; the empirical distribution of many $\hat{\theta}^*$ values stands in for the unknown true sampling distribution.

C: In the bootstrap, each resample of size $n$ is drawn [with replacement] from the original data to form a "bootstrap sample".

C: The [percentile bootstrap] CI uses the $\alpha/2$ and $1-\alpha/2$ quantiles of the bootstrap replicates $\hat{\theta}^*$ as the CI endpoints.

Q: When is the bootstrap especially useful compared to analytical CIs?
A: When the estimator has no closed-form pivot, when the sampling distribution is unknown or intractable, or when assumptions like normality are suspect. The bootstrap trades mathematical derivation for computational resampling.

Q: What is a limitation of the percentile bootstrap CI?
A: Its coverage can be biased when the estimator's distribution is skewed or when $n$ is small. Refinements such as the bias-corrected and accelerated ($\mathrm{BC_a}$) bootstrap or the studentized bootstrap improve coverage but at additional computational and conceptual cost.

Q: Why does the bootstrap CI rely only on the observed sample, without parametric assumptions?
A: Resampling treats the empirical distribution of the data as a plug-in estimate of the true underlying distribution. No parametric family (normal, etc.) is assumed — only that the sample is representative of the population. This makes bootstrap CIs broadly applicable but still asymptotic in their guarantees.
