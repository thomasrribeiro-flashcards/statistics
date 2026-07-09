+++
order = 7
subject = "Math"
tags = ["math", "statistics", "one-sample-test", "z-test", "t-test", "proportion", "variance"]
+++

# Statistics — One-Sample Tests

## 7.1 Why distinguish known vs unknown $\sigma$?

Q: Why does it matter whether the population standard deviation $\sigma$ is known or unknown when testing a mean?
A: When $\sigma$ is known we can standardize $\bar{X}$ using the exact normal distribution and use a $z$-test. When $\sigma$ is unknown we must estimate it by the sample standard deviation $s$, which adds extra variability, so the standardized statistic follows a $t$-distribution rather than a normal. Using a $z$-test with an estimated $\sigma$ would understate uncertainty and inflate the Type I error rate.

Q: In real applications, is $\sigma$ typically known or unknown?
A: Almost always unknown. The known-$\sigma$ case is mostly a pedagogical stepping stone and appears when historical data or manufacturing specifications pin down $\sigma$ independently of the current sample.

C: If the population standard deviation $\sigma$ is known, the one-sample test for a mean uses a [$z$-test]; if $\sigma$ is unknown we use a $t$-test.

C: Replacing $\sigma$ by the sample standard deviation $s$ introduces extra sampling variability, which is why the test statistic then follows a [$t$-distribution] instead of a standard normal.

## 7.2 One-sample $z$-test for mean (known $\sigma$)

Q: What null and alternative hypotheses does a one-sample test of a mean address?
A: $H_0: \mu = \mu_0$ versus one of $H_1: \mu \neq \mu_0$, $H_1: \mu > \mu_0$, or $H_1: \mu < \mu_0$, where $\mu$ is the true population mean and $\mu_0$ is the hypothesized value.

C: The one-sample $z$-statistic for a mean with known $\sigma$ is $Z = \dfrac{\bar{X} - \mu_0}{\sigma/\sqrt{n}}$, where $\bar{X}$ is the sample mean, $\mu_0$ is the hypothesized mean under $H_0$, $\sigma$ is the known population standard deviation, and $n$ is the [sample size].

C: Under $H_0$, the statistic $Z = (\bar{X} - \mu_0)/(\sigma/\sqrt{n})$ follows a [standard normal] distribution (assuming either a normal population or $n$ large enough for the CLT).

Q: Why is $\sigma/\sqrt{n}$ in the denominator of the $z$-statistic?
A: $\sigma/\sqrt{n}$ is the standard error of $\bar{X}$ — the standard deviation of the sampling distribution of the sample mean. Dividing the deviation $\bar{X} - \mu_0$ by its own standard deviation rescales it to a dimensionless $z$-score under $H_0$.

Q: What two conditions justify using the one-sample $z$-test?
A: (1) Observations are independent (e.g., random sample). (2) Either the population is normal, or $n$ is large enough for the Central Limit Theorem to make $\bar{X}$ approximately normal.

## 7.3 Rejection regions for two-sided and one-sided $z$-tests

C: For a two-sided $z$-test at significance level $\alpha$, reject $H_0$ when $|Z| > [z_{\alpha/2}]$, where $z_{\alpha/2}$ is the upper $\alpha/2$ quantile of the standard normal.

C: For a right-sided $z$-test ($H_1: \mu > \mu_0$) at level $\alpha$, reject $H_0$ when $Z > [z_\alpha]$.

C: For a left-sided $z$-test ($H_1: \mu < \mu_0$) at level $\alpha$, reject $H_0$ when $Z < [-z_\alpha]$.

Q: Why does a two-sided $z$-test at level $\alpha$ use $z_{\alpha/2}$ rather than $z_\alpha$?
A: The total rejection probability under $H_0$ must equal $\alpha$, and the two-sided test splits that mass equally between the two tails. Each tail gets probability $\alpha/2$, so the critical value is $z_{\alpha/2}$.

Q: Why would you ever choose a one-sided test over a two-sided test?
A: When the scientific question only cares about deviations in one direction (e.g., "is the new drug better?" — not just different), a one-sided test places all of $\alpha$ in the relevant tail, giving more power to detect real effects in that direction.

C: At $\alpha = 0.05$, the two-sided critical value is $z_{0.025} \approx [1.96]$ and the one-sided critical value is $z_{0.05} \approx 1.645$.

## 7.4 One-sample $t$-test for mean (unknown $\sigma$)

C: When $\sigma$ is unknown, the one-sample $t$-statistic is $T = \dfrac{\bar{X} - \mu_0}{s/\sqrt{n}}$, where $\bar{X}$ is the sample mean, $\mu_0$ is the hypothesized mean, $s$ is the [sample standard deviation], and $n$ is the sample size.

C: Under $H_0: \mu = \mu_0$, the statistic $T = (\bar{X} - \mu_0)/(s/\sqrt{n})$ follows a [$t$-distribution] with $n - 1$ degrees of freedom (for a normal population).

Q: What changes in the formula when going from the one-sample $z$-statistic to the one-sample $t$-statistic?
A: Only the denominator: $\sigma$ (known population SD) is replaced by $s$ (sample SD computed from the same data). The numerator $\bar{X} - \mu_0$ is identical.

Q: Why is the $t$-distribution wider (heavier-tailed) than the standard normal?
A: The denominator $s$ is itself a random variable estimated from the same sample, so $T$ has variability from both $\bar{X}$ and $s$. This extra uncertainty thickens the tails, making extreme values more likely than under the normal.

Q: What happens to the $t$-distribution as $n \to \infty$?
A: $s$ converges to $\sigma$, so $T$ converges in distribution to the standard normal. In practice, for $n \gtrsim 30$ the $t$ and $z$ critical values agree to within a few percent.

## 7.5 Degrees of freedom $n-1$

C: The one-sample $t$-statistic has $n - 1$ degrees of freedom because one degree of freedom is consumed estimating the [sample mean] $\bar{X}$ before computing $s$.

Q: Why does the one-sample $t$-test use $n - 1$ degrees of freedom rather than $n$?
A: The sample standard deviation $s$ is computed from the deviations $X_i - \bar{X}$. Those $n$ deviations must sum to zero, so only $n - 1$ of them are free to vary. The remaining $n - 1$ independent pieces of information about spread give the degrees of freedom.

Q: If $n = 10$, how many degrees of freedom does the one-sample $t$-test use?
A: $n - 1 = 9$ degrees of freedom.

C: For a two-sided $t$-test at level $\alpha$ with sample size $n$, reject $H_0$ when $|T| > t_{\alpha/2,\, n-1}$, where $t_{\alpha/2,\, n-1}$ is the upper $\alpha/2$ [critical value] of the $t$-distribution with $n - 1$ degrees of freedom.

## 7.6 Assumptions of the $t$-test

Q: What are the two core assumptions of the one-sample $t$-test?
A: (1) The observations $X_1, \ldots, X_n$ are independent (ideally from a random sample). (2) The population distribution is approximately normal — or $n$ is large enough that $\bar{X}$ is approximately normal by the CLT.

Q: Why is the independence assumption critical for the $t$-test?
A: The formula $s/\sqrt{n}$ for the standard error assumes independent observations so variances add without covariance terms. Positive correlation (e.g., repeated measures on the same subject) makes the true standard error larger than $s/\sqrt{n}$, so $T$ is inflated and rejection rates are too high.

Q: How robust is the one-sample $t$-test to violations of normality?
A: Fairly robust for large $n$ (CLT helps) and for symmetric distributions. It is most sensitive to heavy skew and outliers in small samples, where a single extreme observation can dominate both $\bar{X}$ and $s$.

C: If the normality assumption is badly violated at small $n$, a common alternative is a [nonparametric] test such as the Wilcoxon signed-rank test.

## 7.7 One-sample test for proportion (large $n$)

Q: When testing $H_0: p = p_0$ for a population proportion, what underlying distribution describes the raw count of successes?
A: A binomial distribution: if we observe $n$ independent trials with success probability $p$, the number of successes $X$ follows $\mathrm{Bin}(n, p)$.

C: The one-sample large-sample $z$-statistic for a proportion is $Z = \dfrac{\hat{p} - p_0}{\sqrt{p_0(1 - p_0)/n}}$, where $\hat{p} = X/n$ is the sample proportion, $p_0$ is the hypothesized proportion under $H_0$, and $n$ is the [sample size].

Q: Why does the denominator of the proportion $z$-test use $p_0(1 - p_0)$ rather than $\hat{p}(1 - \hat{p})$?
A: The test statistic is computed under $H_0: p = p_0$, so the null variance $p_0(1 - p_0)/n$ is used. Plugging $p_0$ (not $\hat{p}$) in the denominator ensures the statistic has an exact standard-normal reference distribution when $H_0$ is true.

Q: What is the usual rule of thumb for using the normal approximation in a proportion test?
A: Both $n p_0 \geq 10$ and $n(1 - p_0) \geq 10$ (some texts use 5). This guarantees enough expected successes and failures for the binomial to be well-approximated by a normal distribution.

C: Under $H_0: p = p_0$ and with large $n$, the statistic $Z = (\hat{p} - p_0)/\sqrt{p_0(1-p_0)/n}$ is approximately [standard normal].

## 7.8 Exact binomial test for proportion (small $n$)

Q: Why do we need an exact binomial test when $n$ is small?
A: The normal approximation breaks down when $n p_0$ or $n(1 - p_0)$ is too small — the discrete, skewed binomial is poorly fit by a continuous normal. Computing tail probabilities directly from the binomial PMF gives exact, valid $p$-values without approximation.

C: The [exact binomial test] computes $p$-values directly from the $\mathrm{Bin}(n, p_0)$ distribution of $X$ under $H_0: p = p_0$ rather than relying on a normal approximation.

Q: For a right-sided exact binomial test of $H_0: p = p_0$ vs. $H_1: p > p_0$ with observed count $X = x$, how is the $p$-value computed?
A: $p\text{-value} = P(X \geq x \mid p = p_0) = \sum_{k=x}^{n} \binom{n}{k} p_0^k (1 - p_0)^{n-k}$, summing the upper tail of the null binomial distribution.

C: For a left-sided exact binomial test with observed successes $x$, the $p$-value is $P(X \leq x \mid p = p_0) = \sum_{k=0}^{x} \binom{n}{k} p_0^k (1 - p_0)^{[n-k]}$.

Q: Why is the two-sided exact binomial $p$-value trickier to define than in the $z$-case?
A: The binomial under $H_0$ is generally asymmetric when $p_0 \neq 0.5$, so "the other tail" is not a mirror image. Common conventions are to double the smaller one-sided $p$-value, or to sum the probabilities of all outcomes at least as unlikely as the observed count.

## 7.9 Chi-square test for variance

Q: What is the one-sample test for a variance testing, and what is $H_0$?
A: It tests whether a normal population's variance equals a hypothesized value: $H_0: \sigma^2 = \sigma_0^2$ against a one- or two-sided alternative, given a random sample $X_1, \ldots, X_n$.

C: The one-sample chi-square statistic for a variance is $\chi^2 = \dfrac{(n - 1) s^2}{\sigma_0^2}$, where $s^2$ is the sample variance, $\sigma_0^2$ is the [hypothesized variance] under $H_0$, and $n$ is the sample size.

C: Under $H_0: \sigma^2 = \sigma_0^2$ with a normal population, the statistic $(n-1) s^2 / \sigma_0^2$ follows a [chi-square] distribution with $n - 1$ degrees of freedom.

Q: Why does the chi-square test for variance require the population to be normal?
A: Unlike the $t$-test for a mean, this test is not robust to non-normality. The chi-square sampling distribution of $(n-1)s^2/\sigma^2$ depends on the fourth moment (kurtosis) of the population; non-normal tails distort the null distribution badly even at moderate $n$.

C: For a two-sided chi-square test of variance at level $\alpha$ with sample size $n$, reject $H_0$ when $\chi^2 < \chi^2_{1-\alpha/2,\, n-1}$ or $\chi^2 > \chi^2_{\alpha/2,\, [n-1]}$.

Q: Why is the two-sided rejection region for a chi-square variance test not symmetric around a single critical value?
A: The chi-square distribution is itself skewed (supported on $[0, \infty)$ and right-skewed), so equal-tail rejection requires two different critical values — the lower $\alpha/2$ quantile and the upper $\alpha/2$ quantile — rather than a symmetric $\pm$ pair.

## 7.10 $p$-values for each test

C: The [$p$-value] is the probability, under $H_0$, of observing a test statistic at least as extreme (in the direction of $H_1$) as the one actually observed.

C: For a two-sided $z$-test with observed statistic $z_{\text{obs}}$, the $p$-value is $2 \cdot P(Z > |z_{\text{obs}}|) = 2\,[1 - \Phi(|z_{\text{obs}}|)]$, where $\Phi$ is the standard normal [CDF].

C: For a right-sided $t$-test with observed $t_{\text{obs}}$ and $\nu = n - 1$ degrees of freedom, the $p$-value is $P(T_\nu > t_{\text{obs}})$, read from a [$t$-table] or software.

C: For a right-sided chi-square variance test with observed $\chi^2_{\text{obs}}$ and $n - 1$ df, the $p$-value is $P(\chi^2_{n-1} > \chi^2_{\text{obs}})$, read from a [chi-square table].

Q: How is the decision rule "reject if $p < \alpha$" related to the critical-value rule?
A: They are equivalent. The $p$-value is the smallest $\alpha$ at which the observed statistic would lie in the rejection region. So $p < \alpha$ iff the statistic is more extreme than the level-$\alpha$ critical value.

Q: For a two-sided $t$-test, why is the $p$-value computed as $2 \cdot P(T_\nu > |t_{\text{obs}}|)$?
A: The $t$-distribution is symmetric about zero. "At least as extreme" in either direction means $|T| \geq |t_{\text{obs}}|$, and by symmetry each tail contributes equal probability, so we double the one-tail value.

## 7.11 Power calculation example for a one-sample $z$-test

P: For a one-sample $z$-test of $H_0: \mu = \mu_0$ vs. $H_1: \mu > \mu_0$ at level $\alpha$, known $\sigma$, and sample size $n$, derive the power at a specific alternative $\mu = \mu_1 > \mu_0$, then evaluate it when $\mu_0 = 100$, $\mu_1 = 103$, $\sigma = 10$, $n = 25$, $\alpha = 0.05$.

S:
**IDENTIFY**: Power = $P(\text{reject } H_0 \mid \mu = \mu_1)$ for a right-sided one-sample $z$-test with known $\sigma$.

**PLAN**:
- Write the rejection rule in terms of $\bar{X}$.
- Express the event $\{\bar{X} > c\}$ under the alternative $\mu = \mu_1$ by standardizing with $\mu_1$ (not $\mu_0$).
- Convert to $\Phi$ and plug in numbers.

**EXECUTE**:
1. Rejection rule: reject when $Z = (\bar{X} - \mu_0)/(\sigma/\sqrt{n}) > z_\alpha$, i.e., when $\bar{X} > \mu_0 + z_\alpha \sigma/\sqrt{n}$.
2. Under $H_1: \mu = \mu_1$, $\bar{X} \sim \mathcal{N}(\mu_1, \sigma^2/n)$. Standardize using $\mu_1$:
$$\text{Power} = P\!\left(\bar{X} > \mu_0 + z_\alpha \tfrac{\sigma}{\sqrt{n}} \,\Big|\, \mu = \mu_1\right) = P\!\left(Z > \frac{\mu_0 - \mu_1}{\sigma/\sqrt{n}} + z_\alpha\right) = \Phi\!\left(\frac{\mu_1 - \mu_0}{\sigma/\sqrt{n}} - z_\alpha\right).$$
3. Plug in numbers: $\sigma/\sqrt{n} = 10/\sqrt{25} = 2$. Effect $= (\mu_1 - \mu_0)/(\sigma/\sqrt{n}) = 3/2 = 1.5$. With $\alpha = 0.05$, $z_\alpha = 1.645$.
4. Power $= \Phi(1.5 - 1.645) = \Phi(-0.145) \approx 0.442$.

**EVALUATE**:
- About a 44% chance of detecting a 3-unit shift with this sample size — underpowered for typical standards ($\geq 0.8$).
- Sanity checks: power increases if $n$ grows (smaller $\sigma/\sqrt{n}$), if $\mu_1$ moves farther from $\mu_0$, or if $\alpha$ grows (smaller $z_\alpha$). Our formula reflects all three.
- To raise power to $0.80$, solve $\Phi^{-1}(0.80) = 0.8416 = (\mu_1 - \mu_0)/(\sigma/\sqrt{n}) - z_\alpha$, giving $(\mu_1 - \mu_0)/(\sigma/\sqrt{n}) = 2.486$, so $n \geq (2.486 \cdot \sigma/(\mu_1 - \mu_0))^2 \approx 68.7$, i.e., $n = 69$.

C: For a right-sided one-sample $z$-test, power at alternative $\mu_1$ equals $\Phi\!\left(\dfrac{\mu_1 - \mu_0}{\sigma/\sqrt{n}} - [z_\alpha]\right)$.

Q: For a fixed effect size $\mu_1 - \mu_0$, how does power change when $n$ increases?
A: Power increases. Larger $n$ shrinks the standard error $\sigma/\sqrt{n}$, so the standardized effect $(\mu_1 - \mu_0)/(\sigma/\sqrt{n})$ grows and $\Phi$ of a larger argument is larger.

Q: How does lowering $\alpha$ affect power, holding everything else fixed?
A: Power decreases. A smaller $\alpha$ raises $z_\alpha$, shrinking the argument of $\Phi$ and therefore the probability of rejection under the alternative. This is the fundamental Type I / Type II error trade-off.

## 7.12 When to prefer CI vs test

Q: When should you prefer a confidence interval over a formal hypothesis test?
A: When you care about the magnitude and precision of the effect, not just a binary reject/don't-reject decision. A CI shows the plausible range of $\mu$ (or $p$, or $\sigma^2$), conveying both statistical significance and practical size in one object.

Q: When is a formal hypothesis test preferred over a confidence interval?
A: When the scientific or decision-theoretic question is genuinely dichotomous — e.g., does a drug meet a regulatory threshold, does a manufacturing process exceed spec — and a pre-specified error rate $\alpha$ is required.

Q: How are a two-sided level-$\alpha$ test and a $100(1-\alpha)\%$ confidence interval for the same parameter related?
A: They are duals: the two-sided test rejects $H_0: \mu = \mu_0$ at level $\alpha$ if and only if $\mu_0$ lies outside the $100(1-\alpha)\%$ CI for $\mu$. The CI contains exactly the values of $\mu_0$ that would not be rejected.

C: The duality between tests and CIs says that a two-sided level-$\alpha$ test rejects $\mu = \mu_0$ iff $\mu_0$ lies [outside] the $100(1 - \alpha)\%$ confidence interval.

Q: Why can a CI be more informative than just a $p$-value?
A: A tiny $p$-value can come from a massive sample with a trivially small effect, and a non-significant test can hide a large but noisy effect. The CI reveals both the point estimate and the uncertainty, exposing practical (non)significance that a $p$-value alone hides.

P: A quality engineer measures the fill weight (grams) of 16 randomly sampled bottles from a production line. The sample mean is $\bar{x} = 498.2$ g and the sample standard deviation is $s = 3.5$ g. The target fill is $\mu_0 = 500$ g. Test $H_0: \mu = 500$ vs. $H_1: \mu \neq 500$ at $\alpha = 0.05$, and report the conclusion.

S:
**IDENTIFY**: One-sample two-sided test of a mean with unknown $\sigma$ → one-sample $t$-test with $n - 1 = 15$ df.

**PLAN**:
- Check assumptions: random sample (independence) and approximate normality of fill weights (reasonable for manufacturing processes).
- Compute $T = (\bar{x} - \mu_0)/(s/\sqrt{n})$.
- Compare $|T|$ to the critical value $t_{0.025,\, 15}$, or equivalently compute the two-sided $p$-value.
- Reject $H_0$ iff $|T| > t_{0.025, 15}$.

**EXECUTE**:
1. Standard error: $s/\sqrt{n} = 3.5/\sqrt{16} = 3.5/4 = 0.875$ g.
2. Statistic: $T = (498.2 - 500)/0.875 = -1.8/0.875 \approx -2.057$.
3. Critical value: $t_{0.025,\, 15} \approx 2.131$ (from $t$-table).
4. Decision: $|T| \approx 2.057 < 2.131$, so do not reject $H_0$ at $\alpha = 0.05$.
5. Two-sided $p$-value: $2 \cdot P(T_{15} > 2.057) \approx 2 \cdot 0.028 = 0.056$.

**EVALUATE**:
- $p$-value $\approx 0.056 > 0.05$, consistent with the critical-value decision.
- A $95\%$ CI for $\mu$ is $\bar{x} \pm t_{0.025, 15} \cdot s/\sqrt{n} = 498.2 \pm 2.131 \cdot 0.875 \approx (496.3, 500.1)$. The target $500$ is (just barely) inside the CI, matching the non-rejection.
- Practical note: the CI makes clear the evidence is borderline. A follow-up study with larger $n$ would resolve whether the process is actually running slightly light.

Q: In the bottle-fill example, why are the critical-value decision and the $p$-value decision guaranteed to agree?
A: They are algebraically the same rule. The $p$-value is the tail probability beyond $|T|$, and the critical value $t_{0.025, 15}$ is defined so that the tail probability beyond it equals $\alpha = 0.05$. Hence $|T| > t_{0.025, 15}$ iff $p < 0.05$.

Q: Why does the CI in the bottle-fill example barely contain $\mu_0 = 500$, consistent with $p \approx 0.056$?
A: By the test-CI duality, the 95% CI contains exactly those $\mu_0$ for which the two-sided level-0.05 test fails to reject. Since $p = 0.056$ is just above $0.05$, $\mu_0 = 500$ lies just inside the boundary of the 95% CI.
