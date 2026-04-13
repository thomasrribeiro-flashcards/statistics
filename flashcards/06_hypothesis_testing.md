+++
order = 6
tags = ["math", "statistics", "hypothesis-testing", "p-value", "type-i", "type-ii", "power", "neyman-pearson"]
+++

# Statistics — Hypothesis Testing

## 6.1 Why Hypothesis Testing?

Q: Why do we need hypothesis testing at all, given that we already have point estimators and confidence intervals?
A: Estimators and CIs tell us what parameter values are plausible, but they do not directly answer yes/no questions like "does this drug work?" or "is this coin fair?". Hypothesis testing is a formal decision framework: it takes a binary claim about the world and a sample of data, and returns a reject/fail-to-reject verdict with controlled error rates.

Q: What makes hypothesis testing a decision framework under uncertainty rather than a proof?
A: Because the sample is random, any decision rule will sometimes err. Hypothesis testing does not prove the claim is true or false — it chooses an action (reject or not) while bounding the long-run frequency of each type of mistake.

C: [Hypothesis testing] is a formal procedure for using sample data to choose between two competing claims about a population parameter while controlling the probability of error.

Q: Why is hypothesis testing asymmetric — we "reject" or "fail to reject" rather than "accept"?
A: The framework is designed to protect one specific claim (the null) from being discarded without strong evidence. Failing to find enough evidence against it does not prove it true; it just means the data are consistent with it. "Absence of evidence is not evidence of absence."

## 6.2 Null and Alternative Hypotheses

C: The [null hypothesis] $H_0$ is the default claim about a parameter that we assume true unless the data provide strong evidence against it.

C: The [alternative hypothesis] $H_1$ (sometimes $H_a$) is the competing claim we would adopt if the null is rejected.

Q: Why is the null hypothesis typically the "status quo" or a statement of no effect?
A: Placing the burden of proof on the alternative protects us from chasing spurious patterns in noise. A new drug, a new effect, or a departure from a baseline must earn its claim by overcoming strong sample evidence, not merely by fitting the data better than the null.

C: A [two-sided] (or two-tailed) alternative has the form $H_1: \theta \neq \theta_0$, where $\theta$ is the population parameter and $\theta_0$ is the null value.

C: A [one-sided] (or one-tailed) alternative has the form $H_1: \theta > \theta_0$ or $H_1: \theta < \theta_0$, where $\theta$ is the population parameter and $\theta_0$ is the null value.

Q: When should you use a one-sided rather than a two-sided alternative?
A: Only when, before seeing the data, the opposite-direction deviation is either impossible or uninteresting (e.g., a new drug can only matter if it is better, not worse). Otherwise use two-sided, because one-sided tests can overstate evidence if the direction is chosen after peeking at the data.

Q: For testing whether a coin is fair against the possibility that it is biased (either way), what are $H_0$ and $H_1$?
A: $H_0: p = 0.5$ and $H_1: p \neq 0.5$, where $p$ is the probability of heads. This is a two-sided test because bias in either direction counts as evidence against fairness.

## 6.3 Test Statistic and Rejection Region

C: A [test statistic] $T$ is a function of the sample data whose distribution under $H_0$ is known, and whose value summarizes how far the data are from what $H_0$ predicts.

C: The [rejection region] $R$ is the set of test statistic values for which we reject $H_0$; equivalently, the decision rule is "reject $H_0$ if $T \in R$."

Q: Why must the distribution of the test statistic under $H_0$ be known (or approximable)?
A: To control error rates we must compute probabilities like $P(T \in R \mid H_0)$. Without knowing how $T$ behaves when the null is true, we cannot calibrate the rejection region to achieve a specified error probability.

Q: How is the rejection region chosen in practice?
A: Pick a significance level $\alpha$, then choose $R$ so that $P(T \in R \mid H_0) = \alpha$. The shape of $R$ (one tail or two) is determined by $H_1$: values of $T$ most consistent with $H_1$ go into $R$.

C: For a two-sided alternative, the rejection region is typically [symmetric around the null value], e.g., $|T| > c$ for some critical value $c$.

C: For a one-sided alternative $H_1: \theta > \theta_0$, the rejection region has the form $T > c$, where $c$ is the [critical value] chosen so $P(T > c \mid H_0) = \alpha$.

## 6.4 Type I Error and Significance Level

C: A [Type I error] is rejecting $H_0$ when $H_0$ is actually true — a "false alarm."

C: The [significance level] $\alpha$ is the probability of a Type I error: $\alpha = P(\text{reject } H_0 \mid H_0 \text{ true})$.

Q: Why is $\alpha$ chosen before looking at the data?
A: Fixing $\alpha$ in advance pins down the rejection region and guarantees the stated long-run false-alarm rate. Choosing $\alpha$ after seeing the data would let us tune the rule to get whatever verdict we wanted, destroying the error-rate guarantee.

Q: What does $\alpha = 0.05$ mean in repeated-use terms?
A: If $H_0$ were true and we applied the test to many independent samples, we would falsely reject $H_0$ in about 5% of those samples in the long run.

C: Common choices of significance level are $\alpha = 0.05$, $\alpha = 0.01$, and $\alpha = 0.10$, selected based on [how costly a false rejection is] relative to the context.

## 6.5 Type II Error

C: A [Type II error] is failing to reject $H_0$ when $H_0$ is actually false — a "missed detection."

C: The probability of a Type II error is denoted [$\beta$], and it depends on the true parameter value under $H_1$.

Q: Why does $\beta$ depend on the specific alternative value, while $\alpha$ does not?
A: Under $H_0$ the parameter is pinned down (e.g., $\theta = \theta_0$), so the distribution of $T$ is fixed and $\alpha$ is a single number. Under $H_1$, the parameter can take many values; the farther the truth is from $\theta_0$, the easier the test detects it, so $\beta$ is a function of the true $\theta$.

Q: Why can we not simply set $\beta = 0$?
A: Driving the miss rate to zero would require rejecting $H_0$ for almost any data, which would push the false-alarm rate $\alpha$ toward 1. We can only reduce $\beta$ by either loosening $\alpha$ or collecting more data.

## 6.6 Power of a Test

C: The [power] of a test at a particular alternative value $\theta_1$ is $1 - \beta(\theta_1)$, the probability of correctly rejecting $H_0$ when the true parameter equals $\theta_1$.

Q: Why is power a function of $\theta_1$ rather than a single number?
A: Detecting a small deviation from $\theta_0$ is harder than detecting a large one, so power grows as the true parameter moves away from $\theta_0$. Plotting power vs. $\theta$ (the "power curve") shows how the test's sensitivity varies across the alternative.

Q: What three levers increase the power of a test?
A: (1) Increase sample size $n$ (shrinks the sampling variability of $T$); (2) raise the significance level $\alpha$ (enlarges the rejection region); (3) focus on larger effect sizes (move $\theta_1$ farther from $\theta_0$).

C: A test with power $0.80$ at effect size $\theta_1$ has an [80%] chance of correctly rejecting $H_0$ when the true parameter equals $\theta_1$.

Q: Why do researchers commonly target power of at least 0.80?
A: It is a conventional balance: 80% gives a reasonably high chance of detecting a real effect without demanding the enormous sample sizes that higher power (e.g., 0.99) would require. It is a cost-vs-sensitivity compromise, not a mathematical necessity.

## 6.7 The α–β Tradeoff

Q: Why is there a tradeoff between $\alpha$ and $\beta$ for a fixed sample size?
A: Enlarging the rejection region to catch more real effects (lower $\beta$) necessarily captures more chance fluctuations under $H_0$ (higher $\alpha$). With $n$ fixed, pushing one error rate down pushes the other up — only more data can shrink both at once.

C: For a fixed sample size $n$, reducing $\alpha$ (fewer false alarms) generally [increases] $\beta$ (more missed detections).

Q: How does increasing the sample size $n$ affect the $\alpha$–$\beta$ tradeoff?
A: More data sharpens the sampling distribution of $T$, so the distributions of $T$ under $H_0$ and $H_1$ overlap less. We can then shrink the rejection region (smaller $\alpha$) without enlarging $\beta$ — both error rates can be driven down together.

Q: When designing a study, how do you typically resolve the $\alpha$–$\beta$ tradeoff?
A: Fix $\alpha$ at a conventional level (e.g., 0.05), specify a minimum effect size worth detecting, demand a target power (e.g., 0.80), then solve for the sample size $n$ needed. This is called a power calculation.

## 6.8 p-value

C: The [p-value] is the probability, computed under $H_0$, of observing a test statistic at least as extreme as the one actually observed, where "extreme" is defined in the direction(s) favoring $H_1$.

Q: Why is the phrase "as or more extreme" critical to the p-value definition?
A: The p-value must account not only for the specific outcome observed but also for all outcomes that would give even stronger evidence against $H_0$. Restricting to just the observed point would give a probability of zero for continuous statistics and would misstate the strength of evidence.

C: For a two-sided test, the p-value is typically $2 \cdot P(T \geq |t_{\text{obs}}| \mid H_0)$, where $t_{\text{obs}}$ is the [observed test statistic value] and $T$ is the test statistic under $H_0$.

Q: What exactly does a p-value of $0.03$ mean?
A: If $H_0$ were true, there is a 3% probability of obtaining data yielding a test statistic at least as extreme as the one we observed. It is a measure of how surprising the data are under $H_0$, not a probability that $H_0$ is true.

Q: Why does a smaller p-value constitute stronger evidence against $H_0$?
A: A small p-value means the observed data would be very unlikely under $H_0$. The more unlikely the data under $H_0$, the less tenable $H_0$ becomes as an explanation — that is what "evidence against" means in this framework.

## 6.9 Decision Rule Using the p-value

C: The p-value decision rule is: [reject $H_0$ if $p < \alpha$], and fail to reject $H_0$ otherwise.

Q: Why is "reject if $p < \alpha$" equivalent to "reject if $T \in R$"?
A: The rejection region is built so that $P(T \in R \mid H_0) = \alpha$. The p-value equals the smallest $\alpha$ at which the observed data would lead to rejection; so $p < \alpha$ holds exactly when the observed $T$ falls in the rejection region calibrated to level $\alpha$.

C: The p-value is the [smallest significance level] at which the observed data would lead to rejection of $H_0$.

Q: Why should $\alpha$ be chosen before computing the p-value rather than after?
A: Choosing $\alpha$ after seeing $p$ lets you select any threshold that delivers the verdict you prefer, which destroys the Type I error guarantee. Pre-specifying $\alpha$ keeps the procedure honest.

## 6.10 Common Misinterpretations of p-values

Q: Why is "the p-value is the probability that $H_0$ is true" wrong?
A: The p-value is $P(\text{data as extreme} \mid H_0)$, not $P(H_0 \mid \text{data})$. Swapping the two is the conditional-probability fallacy. Computing $P(H_0 \mid \text{data})$ would require a Bayesian prior on $H_0$, which classical testing does not use.

Q: Why is "$1 - p$ is the probability that $H_1$ is true" wrong?
A: For the same reason — the p-value is not a posterior probability. Neither $p$ nor $1 - p$ can be interpreted as the probability of any hypothesis without a prior.

Q: Why does "$p > \alpha$" not prove $H_0$ is true?
A: Failing to reject $H_0$ means the data are consistent with $H_0$, not that $H_0$ has been established. The true parameter could still differ from $\theta_0$; the sample was just too small or too noisy to detect it. Absence of evidence is not evidence of absence.

Q: Why is a very small p-value not the same as a large effect?
A: A tiny p-value says the effect is statistically detectable given the sample, which can happen even for a trivially small effect if $n$ is huge. Effect size (how far from $\theta_0$) and statistical significance (how unlikely under $H_0$) are distinct — always report both.

C: Statistical significance is [not the same as] practical or scientific significance.

## 6.11 Neyman-Pearson Lemma

Q: Why do we need a lemma about "most powerful" tests at all?
A: Many tests achieve the same $\alpha$, but they differ in power. Among level-$\alpha$ tests for a given alternative, we want the one most likely to catch real effects. The Neyman-Pearson lemma identifies that uniquely most powerful test for the simplest setting.

C: A test is called [simple vs. simple] when both $H_0: \theta = \theta_0$ and $H_1: \theta = \theta_1$ specify a single parameter value.

C: The [likelihood ratio] at data $\vec{x}$ is $\Lambda(\vec{x}) = \dfrac{L(\theta_1 \mid \vec{x})}{L(\theta_0 \mid \vec{x})}$, where $L(\theta \mid \vec{x})$ is the likelihood of $\theta$ given data $\vec{x}$.

C: [Neyman-Pearson lemma]: among all level-$\alpha$ tests of simple $H_0: \theta = \theta_0$ vs. simple $H_1: \theta = \theta_1$, the test that rejects $H_0$ when $\Lambda(\vec{x}) > k$ (with $k$ chosen so $P(\Lambda > k \mid H_0) = \alpha$) is the most powerful.

Q: Intuitively, why does the likelihood ratio give the most powerful test?
A: $\Lambda$ is the exact measure of how much more likely the data are under $H_1$ than under $H_0$. Rejecting for the largest $\Lambda$ values means rejecting precisely when the data are maximally favorable to $H_1$, so every unit of rejection "budget" $\alpha$ is spent on the outcomes that matter most.

Q: What is the main limitation of the Neyman-Pearson lemma?
A: It assumes both hypotheses are simple (single parameter values), which is rarely true in practice. Real alternatives are composite (e.g., $\theta > \theta_0$), so the lemma gives the ideal to approximate rather than a direct recipe.

## 6.12 Likelihood Ratio Test

Q: Why generalize Neyman-Pearson to the likelihood ratio test?
A: Composite hypotheses (sets of parameter values) do not have a single likelihood; we need to compare the best-fitting parameter under $H_0$ against the best-fitting parameter overall. The likelihood ratio test does exactly that and extends the Neyman-Pearson logic to realistic settings.

C: The [likelihood ratio test statistic] is $\lambda(\vec{x}) = \dfrac{\sup_{\theta \in \Theta_0} L(\theta \mid \vec{x})}{\sup_{\theta \in \Theta} L(\theta \mid \vec{x})}$, where $\Theta_0$ is the null parameter set, $\Theta$ is the full parameter set, and $L(\theta \mid \vec{x})$ is the likelihood.

Q: Why does $\lambda(\vec{x})$ always satisfy $0 \leq \lambda \leq 1$?
A: The numerator maximizes $L$ over a subset $\Theta_0 \subseteq \Theta$, and the denominator maximizes over all of $\Theta$. A supremum over a subset cannot exceed the supremum over the larger set, so the ratio lies in $[0, 1]$.

Q: Why does a small $\lambda$ argue against $H_0$?
A: $\lambda$ small means even the best-fitting parameter inside $\Theta_0$ explains the data much worse than the best-fitting parameter overall. The data are compatible with some $\theta \notin \Theta_0$ far better than with anything in $\Theta_0$, so $H_0$ looks wrong.

C: The likelihood ratio test rejects $H_0$ when [$\lambda(\vec{x}) < c$], where $c$ is chosen so $P(\lambda < c \mid H_0) = \alpha$.

Q: Under regularity conditions, what is the large-sample distribution of $-2 \ln \lambda$ under $H_0$?
A: $-2 \ln \lambda \xrightarrow{d} \chi^2_k$, where $k$ is the difference in dimension between the full parameter space $\Theta$ and the null subspace $\Theta_0$. This (Wilks' theorem) lets us calibrate the test using chi-square critical values when exact distributions are intractable.

## 6.13 Duality Between Confidence Intervals and Tests

Q: Why is there a tight correspondence between confidence intervals and hypothesis tests?
A: Both answer the same geometric question — which parameter values are consistent with the data. A CI collects all $\theta_0$ we would fail to reject; a test asks whether a given $\theta_0$ lies in that set. They are two views of one object.

C: A $(1 - \alpha)$ confidence interval for $\theta$ is the set of all null values $\theta_0$ for which the level-$\alpha$ test of $H_0: \theta = \theta_0$ [fails to reject].

Q: Given a $95\%$ CI for $\mu$ of $[2.1, 5.7]$, what is the result of a two-sided test of $H_0: \mu = 4$ at $\alpha = 0.05$?
A: Fail to reject, because $4 \in [2.1, 5.7]$. Any null value inside the CI is consistent with the data at that level.

Q: Given the same $95\%$ CI $[2.1, 5.7]$, what is the result of a two-sided test of $H_0: \mu = 6$ at $\alpha = 0.05$?
A: Reject, because $6 \notin [2.1, 5.7]$. Any null value outside the CI is rejected at the corresponding level.

Q: Why is it often more informative to report a CI than a p-value alone?
A: A CI shows both whether the null is rejected (is $\theta_0$ inside?) and the magnitude and precision of the effect (where is the interval, how wide is it?). A p-value collapses all of this into one number and discards effect size information.

## 6.14 Procedure: Performing a Hypothesis Test

P: You have an i.i.d. sample $X_1, \ldots, X_n$ from a population with unknown parameter $\theta$, and you want to test a claim about $\theta$ at significance level $\alpha$. Describe the full procedure for performing the hypothesis test.

S:
**IDENTIFY**: A hypothesis test about a population parameter $\theta$ using a random sample. Goal: produce a reject / fail-to-reject decision while controlling the Type I error rate at $\alpha$.

**PLAN**:
- State the null $H_0$ and alternative $H_1$ (decide one-sided vs. two-sided from the scientific question, before looking at data).
- Choose a significance level $\alpha$ (commonly $0.05$) in advance.
- Pick a test statistic $T$ whose distribution under $H_0$ is known (or approximable, e.g., via CLT).
- Determine either the rejection region $R$ at level $\alpha$ or plan to compute a p-value.

**EXECUTE**:
1. Check the assumptions of the test (independence, approximate normality or large $n$, known or estimated variance, etc.). If assumptions fail, use a different test.
2. Compute the observed test statistic $t_{\text{obs}}$ from the sample.
3. Compute the p-value: $p = P(T \text{ as or more extreme than } t_{\text{obs}} \mid H_0)$, with "extreme" matching the direction of $H_1$ (one-sided or two-sided).
4. Apply the decision rule: reject $H_0$ if $p < \alpha$; otherwise fail to reject $H_0$.

**EVALUATE**:
- State the conclusion in plain language referring to $\theta$ and the scientific question, not just "reject $H_0$."
- Report the effect size (e.g., $\hat\theta - \theta_0$) and a $(1 - \alpha)$ CI for $\theta$ alongside the p-value so readers see both significance and magnitude.
- Remember: failing to reject is not proof of $H_0$; rejecting is not proof that the effect is practically important.
- Sanity check: does the CI–test duality agree? $\theta_0$ should be outside the CI iff the test rejects.
