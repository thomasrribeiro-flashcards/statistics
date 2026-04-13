+++
order = 13
tags = ["math", "statistics", "nonparametric", "bootstrap", "bayesian", "conjugate-prior", "credible-interval"]
+++

# Statistics — Nonparametric Methods and Bayesian Inference

## 13.1 Why Nonparametric?

Q: Why do we need nonparametric methods at all, given how powerful $t$-tests and ANOVA are?
A: Classical tests assume the data come from a specific distribution (usually normal) and test parameters like $\mu$ or $\sigma^2$. When those assumptions fail — small samples, heavy tails, outliers, ordinal data — nonparametric methods give valid inference using only weak structural assumptions (e.g., continuity, symmetry, or just the rank ordering).

C: [Nonparametric methods] are inference procedures that make weak or no assumptions about the underlying distributional form of the data.

C: Nonparametric tests typically operate on [ranks] or [signs] of the data rather than the raw values, which makes them robust to outliers and distribution shape.

Q: What do nonparametric methods trade off for their weaker assumptions?
A: Statistical power. When the parametric assumptions actually hold, the corresponding parametric test (e.g., $t$-test) is more powerful — it detects true effects at smaller sample sizes. Nonparametric tests pay a small efficiency cost to gain robustness.

C: The [asymptotic relative efficiency] of the Wilcoxon signed-rank test compared to the $t$-test under normality is about $[0.955]$, meaning only a tiny power loss is incurred when the data are actually normal.

Q: When should you prefer a nonparametric test over its parametric counterpart?
A: When the sample is small and the data are skewed, heavy-tailed, or contain outliers; when the data are ordinal rather than interval; or when a normal-quantile plot shows strong departure from normality that a transformation cannot fix.

## 13.2 Sign Test for the Median

Q: Why does the sign test work with almost no distributional assumptions?
A: Under the null hypothesis that the population median equals $m_0$, each observation is equally likely to fall above or below $m_0$. So the number of observations above $m_0$ is $\text{Binomial}(n, 0.5)$ regardless of the shape of the distribution — as long as the distribution is continuous.

C: The [sign test] tests $H_0: \text{median} = m_0$ by counting how many observations exceed $m_0$ and comparing to a $\text{Binomial}(n, 0.5)$ distribution, where $n$ is the number of non-tied observations.

C: In the sign test, observations exactly equal to $m_0$ are [discarded] and $n$ is reduced accordingly.

C: Let $S_+$ be the number of observations with $x_i > m_0$. Under $H_0$, $S_+ \sim [\text{Binomial}(n, 0.5)]$, where $n$ is the count of non-tied observations.

Q: What is the main weakness of the sign test compared to the Wilcoxon signed-rank test?
A: The sign test uses only the direction (above or below $m_0$) and ignores how far each observation is from $m_0$. This throws away information about magnitude, so it is less powerful when the underlying distribution is symmetric.

## 13.3 Wilcoxon Signed-Rank Test

Q: Why does the Wilcoxon signed-rank test require the distribution to be symmetric about the median?
A: The test uses the ranks of $|x_i - m_0|$ combined with the signs of $x_i - m_0$. Under $H_0$, symmetry ensures that each rank is equally likely to carry a $+$ or a $-$ sign, so the signed-rank sum has a distribution free of the underlying shape.

C: The [Wilcoxon signed-rank test] tests $H_0: \text{median} = m_0$ for data from a continuous distribution that is symmetric about its median.

C: The Wilcoxon signed-rank statistic $W_+$ is the sum of the ranks of $|x_i - m_0|$ over all $i$ with [$x_i > m_0$], where ranks are assigned to the absolute deviations from smallest to largest.

Q: How is the Wilcoxon signed-rank test applied to paired data?
A: Compute the differences $d_i = x_i - y_i$ for each pair, then run the one-sample signed-rank test on the $d_i$ values with null median 0. This tests whether the two paired populations have the same center.

C: Under $H_0$, the mean and variance of the Wilcoxon signed-rank statistic $W_+$ are $E[W_+] = [n(n+1)/4]$ and $\operatorname{Var}(W_+) = n(n+1)(2n+1)/24$, where $n$ is the number of non-zero differences.

Q: Why is the Wilcoxon signed-rank test more powerful than the sign test under symmetry?
A: It uses both the sign and the magnitude of each deviation (via ranks), not just the sign. Large deviations carry more weight than small ones, so the test can detect a shift that the sign test would miss.

## 13.4 Mann-Whitney U (Wilcoxon Rank-Sum) Test

Q: What is the null hypothesis of the Mann-Whitney U test in its simplest form?
A: That the two independent samples come from the same continuous distribution — equivalently, that a randomly chosen observation from population 1 is equally likely to be above or below a random observation from population 2: $P(X_1 > X_2) = 0.5$.

C: The [Mann-Whitney U test] (equivalently, the Wilcoxon rank-sum test) compares two independent samples by pooling them, ranking all observations together, and comparing the rank sums of the two groups.

C: With sample sizes $n_1$ and $n_2$, let $R_1$ be the sum of ranks in group 1 in the pooled ranking. Then $U_1 = R_1 - [n_1(n_1+1)/2]$, where $n_1(n_1+1)/2$ is the minimum possible value of $R_1$.

C: Under $H_0$, $E[U_1] = [n_1 n_2 / 2]$ and $\operatorname{Var}(U_1) = n_1 n_2 (n_1 + n_2 + 1)/12$, where $n_1, n_2$ are the two group sizes.

Q: Why is the Mann-Whitney U called the nonparametric analogue of the two-sample $t$-test?
A: Both test whether two independent populations have the same center. The $t$-test assumes normality and tests equality of means; Mann-Whitney U requires only continuity and tests the stochastic ordering of the distributions, remaining valid under non-normal shapes.

Q: What do tied observations force you to do in rank-based tests?
A: Assign each tied observation the average of the ranks it would have received had they been distinguishable (midranks). The test statistic's variance must also be adjusted downward to account for the ties, or a tie-corrected formula used.

## 13.5 Kruskal-Wallis Test

Q: Why do we need a separate test when we have more than two groups?
A: Running multiple pairwise Mann-Whitney tests inflates the Type I error rate. Kruskal-Wallis extends rank-based testing to $k \geq 2$ groups with a single global test, just as one-way ANOVA extends the two-sample $t$-test.

C: The [Kruskal-Wallis test] is the nonparametric analogue of one-way ANOVA: it tests whether $k$ independent samples come from the same continuous distribution, using the pooled ranks.

C: The Kruskal-Wallis statistic is $H = \frac{12}{N(N+1)} \sum_{j=1}^{k} \frac{R_j^2}{n_j} - 3(N+1)$, where $N = \sum n_j$ is the total sample size, $n_j$ is the size of group $j$, and $R_j$ is the [sum of ranks in group $j$].

C: Under $H_0$ and for large $n_j$, the Kruskal-Wallis statistic $H$ approximately follows a [chi-squared] distribution with $k - 1$ degrees of freedom, where $k$ is the number of groups.

Q: What assumption does Kruskal-Wallis make beyond continuity of the distributions?
A: For the test to be interpreted as a test of equal medians (rather than just equal distributions), the groups are assumed to have the same shape and spread, differing at most in location. Without this, a significant $H$ only says "at least one distribution differs."

## 13.6 Spearman's Rank Correlation

Q: Why use Spearman's correlation instead of Pearson's?
A: Pearson's $r$ measures linear association and is sensitive to outliers and non-linear monotone relationships. Spearman's $\rho_s$ replaces the raw data with their ranks, so it measures any monotone association and is robust to outliers and non-linear but monotone trends.

C: [Spearman's rank correlation coefficient] $\rho_s$ is Pearson's correlation computed on the ranks of the two variables instead of their raw values.

C: When there are no ties, Spearman's $\rho_s = 1 - \frac{6 \sum_{i=1}^{n} d_i^2}{n(n^2 - 1)}$, where $d_i$ is the [difference in ranks] of the $i$th observation between the two variables, and $n$ is the sample size.

Q: What does $\rho_s = 1$ mean, and how does it differ from $r = 1$?
A: $\rho_s = 1$ means the two variables are related by a perfect monotone increasing function — as one increases, so does the other, but not necessarily linearly. $r = 1$ requires an exact linear relationship. Every $r = 1$ pattern gives $\rho_s = 1$, but not vice versa.

C: Spearman's $\rho_s$ takes values in [$[-1, 1]$], with $-1$ indicating a perfect monotone decreasing relationship and $+1$ indicating a perfect monotone increasing one.

## 13.7 The Bootstrap Idea

Q: Why do we resort to resampling when we already have formulas for standard errors?
A: Classical standard-error formulas rely on distributional assumptions (often normality) or on having a simple estimator like a sample mean. For complicated statistics — the median, a ratio, a trimmed mean, a regression coefficient under weird conditions — analytical standard errors may not exist or may require assumptions we cannot defend. The bootstrap sidesteps this by simulating the sampling distribution directly.

C: The [bootstrap] is a resampling method that estimates the sampling distribution of a statistic by repeatedly drawing samples with replacement from the observed data.

C: In the nonparametric bootstrap, each bootstrap sample is drawn from the original data of size $n$ [with replacement] and has the same size $n$.

C: The empirical distribution $\hat{F}_n$ places mass $[1/n]$ on each observed data point, where $n$ is the sample size; the bootstrap treats $\hat{F}_n$ as a stand-in for the unknown true distribution $F$.

Q: What is the "bootstrap principle" in one sentence?
A: The distribution of an estimator's deviation from the true parameter (under $F$) is approximated by the distribution of the bootstrap estimator's deviation from the sample estimate (under $\hat{F}_n$).

Q: Why do bootstrap samples match the original size $n$ instead of being smaller?
A: Because the variance of an estimator typically depends on the sample size. Drawing samples of size $n$ preserves the right sampling variability; using a smaller size would underestimate uncertainty, and a larger size would overestimate precision.

## 13.8 Bootstrap Percentile Confidence Interval

Q: What is the core idea of the bootstrap percentile confidence interval?
A: Generate many bootstrap estimates $\hat{\theta}^{*(1)}, \ldots, \hat{\theta}^{*(B)}$ of the parameter, and use the empirical quantiles of this bootstrap distribution as the confidence interval endpoints. No formula for the standard error is needed.

C: The [bootstrap percentile interval] at level $1 - \alpha$ is $[\hat{\theta}^*_{(\alpha/2)}, \hat{\theta}^*_{(1-\alpha/2)}]$, where $\hat{\theta}^*_{(p)}$ is the $p$th empirical quantile of the $B$ bootstrap replicates.

C: For a 95% bootstrap percentile CI, you use the [2.5th] and 97.5th percentiles of the bootstrap distribution as the lower and upper endpoints.

Q: How many bootstrap replicates $B$ are usually enough for a percentile CI?
A: For standard errors, $B \approx 200$ suffices; for percentile confidence intervals, aim for $B \geq 1000$, and $B \geq 10{,}000$ if you want stable tail quantiles. More replicates reduce Monte Carlo error but never fix sampling error in the original data.

Q: What is a failure mode of the bootstrap percentile interval?
A: It can have poor coverage when the estimator is biased or the sampling distribution is skewed — the percentile method assumes (implicitly) that the bootstrap distribution is roughly symmetric around the true parameter. Bias-corrected ($\text{BC}_a$) intervals fix this at the cost of extra machinery.

P: You observe data $x_1, \ldots, x_n$ and want a 95% bootstrap percentile confidence interval for the population median. How do you do it?

S:
**IDENTIFY**: Nonparametric CI for a statistic (the median) with no simple closed-form standard error.

**PLAN**:
- Use the nonparametric bootstrap to simulate the sampling distribution of the sample median.
- Extract the 2.5th and 97.5th empirical quantiles of the bootstrap medians as the interval.

**EXECUTE**:
1. Compute the observed sample median $\hat{m}$ from $x_1, \ldots, x_n$.
2. For $b = 1, \ldots, B$ (with $B \geq 1000$): draw a sample of size $n$ with replacement from $\{x_1, \ldots, x_n\}$ and compute its median $\hat{m}^{*(b)}$.
3. Sort the $B$ bootstrap medians.
4. Report $(\hat{m}^*_{(0.025)},\; \hat{m}^*_{(0.975)})$ as the 95% percentile CI.

**EVALUATE**:
- Check that the observed $\hat{m}$ lies inside the interval; if the interval looks badly skewed around $\hat{m}$, consider a bias-corrected interval instead.
- Increase $B$ and rerun to verify the endpoints have stabilized.
- Remember this is a CI for the population median, not a prediction interval for a new observation.

## 13.9 Permutation Tests

Q: Why is a permutation test often the "gold standard" for two-sample comparisons?
A: Under the null hypothesis of no difference between groups, the group labels are exchangeable — so the distribution of the test statistic under $H_0$ is exactly the distribution obtained by randomly shuffling the labels. This gives an exact $p$-value with no distributional assumption beyond exchangeability.

C: A [permutation test] computes a $p$-value by re-randomizing group labels (or pairings) many times and comparing the observed test statistic to the distribution of permuted statistics.

C: The exchangeability assumption of a permutation test says that under $H_0$, every reassignment of labels is [equally likely] to have produced the observed data.

Q: How does a permutation test differ from the bootstrap?
A: A permutation test resamples without replacement and is designed for testing a null hypothesis by breaking the relationship between labels and outcomes. The bootstrap resamples with replacement to approximate the sampling distribution of an estimator (for standard errors and CIs), not to test a specific null.

C: The two-sample permutation $p$-value is $p = [\frac{\#\{T^{*(b)} \geq T_{\text{obs}}\}}{B}]$ for a one-sided test, where $T_{\text{obs}}$ is the observed statistic, $T^{*(b)}$ is the statistic from the $b$th permutation, and $B$ is the number of permutations.

Q: When is a permutation test exact rather than approximate?
A: When all $\binom{n_1 + n_2}{n_1}$ possible label assignments are enumerated (complete enumeration), the $p$-value is exact. When only $B$ random permutations are used (Monte Carlo permutation test), the $p$-value is an approximation whose Monte Carlo error shrinks as $B$ increases.

## 13.10 Bayesian Inference Basics

Q: What fundamental shift does Bayesian inference make compared to the frequentist view?
A: Bayesian inference treats the unknown parameter $\theta$ as a random variable with its own probability distribution, representing our uncertainty about its value. Frequentists treat $\theta$ as a fixed (unknown) constant and attach probabilities only to data.

C: The [prior distribution] $\pi(\theta)$ encodes our beliefs about the parameter $\theta$ before observing any data.

C: The [likelihood] $L(x \mid \theta)$ is the probability (or density) of the observed data $x$ viewed as a function of the parameter $\theta$.

C: The [posterior distribution] $\pi(\theta \mid x)$ encodes our beliefs about $\theta$ after combining the prior with the data.

Q: Why do Bayesians view inference as "updating beliefs"?
A: The posterior is obtained by combining prior beliefs with evidence from the data via Bayes' rule. As more data accumulate, the posterior concentrates on the truth and the influence of the prior shrinks. Inference becomes a formal process of belief revision.

## 13.11 Bayes' Rule for Parameters

C: Bayes' rule for parameters states $\pi(\theta \mid x) = \frac{L(x \mid \theta) \pi(\theta)}{\int L(x \mid \theta') \pi(\theta')\, d\theta'}$, where $\pi(\theta)$ is the prior, $L(x \mid \theta)$ is the likelihood, and the [denominator] is the marginal likelihood (a normalizing constant).

C: Because the denominator in Bayes' rule does not depend on $\theta$, we often write $\pi(\theta \mid x) \propto L(x \mid \theta)\, \pi(\theta)$, where $\propto$ means [proportional to] (up to a constant in $\theta$).

Q: Why is the proportional form $\pi(\theta \mid x) \propto L(x \mid \theta)\pi(\theta)$ so useful in practice?
A: It lets us find the posterior's shape without computing the often-intractable marginal likelihood $\int L(x \mid \theta')\pi(\theta')\,d\theta'$. If the product $L\pi$ matches a known distributional kernel, we immediately recognize the posterior and its normalizing constant is fixed automatically.

Q: What role does the marginal likelihood play in Bayes' rule?
A: It is the normalizing constant $\int L(x \mid \theta)\pi(\theta)\,d\theta$ that makes the posterior integrate to 1. It also equals $P(x)$, the probability of the observed data averaged over the prior, and is used for Bayesian model comparison (Bayes factors).

Q: What happens to the posterior as the sample size $n$ grows large?
A: The likelihood concentrates sharply around the maximum likelihood estimate, overwhelming the prior. The posterior becomes approximately normal centered at the MLE with variance given by the inverse observed Fisher information — the Bernstein-von Mises theorem.

## 13.12 Conjugate Priors

Q: Why do we care about conjugate priors?
A: When the prior and likelihood are conjugate, the posterior lies in the same family as the prior. This means Bayes' rule reduces to a simple update of parameters instead of integration, giving closed-form posteriors — enormously convenient for teaching, interpretation, and fast computation.

C: A prior is [conjugate] to a likelihood if the resulting posterior belongs to the same parametric family as the prior.

C: For a Binomial likelihood with success probability $\theta$, the conjugate prior is the [Beta distribution]: if $x \sim \text{Binomial}(n, \theta)$ and $\theta \sim \text{Beta}(\alpha, \beta)$, then $\theta \mid x \sim \text{Beta}(\alpha + x, \beta + n - x)$.

Q: How are the Beta prior parameters $\alpha$ and $\beta$ interpreted in the Beta-Binomial model?
A: They act as "pseudo-counts": $\alpha$ is the equivalent number of prior successes and $\beta$ the equivalent number of prior failures. A $\text{Beta}(1,1)$ prior corresponds to zero pseudo-observations (uniform on $[0,1]$), while a $\text{Beta}(10, 10)$ prior carries the weight of 20 prior trials centered at $\theta = 0.5$.

C: For a Normal likelihood $x_i \sim N(\mu, \sigma^2)$ with known variance $\sigma^2$, the conjugate prior for $\mu$ is [Normal]: if $\mu \sim N(\mu_0, \tau_0^2)$, the posterior is also Normal with updated mean and variance.

C: In the Normal-Normal model with known $\sigma^2$, the posterior mean is a [precision-weighted average] of the prior mean $\mu_0$ and the sample mean $\bar{x}$, where precision equals $1/\text{variance}$.

C: For a Poisson likelihood $x_i \sim \text{Poisson}(\lambda)$, the conjugate prior for $\lambda$ is the [Gamma distribution]: if $\lambda \sim \text{Gamma}(\alpha, \beta)$, then $\lambda \mid \mathbf{x} \sim \text{Gamma}(\alpha + \sum x_i, \beta + n)$, where $n$ is the number of observations.

Q: What does the posterior $\theta \mid x \sim \text{Beta}(\alpha + x, \beta + n - x)$ tell us intuitively?
A: Each observed success adds 1 to the first Beta parameter, each failure adds 1 to the second. The prior $(\alpha, \beta)$ is "updated" by adding the actual counts; pseudo-counts and real counts combine additively.

P: You believe the success probability $\theta$ of a new treatment has a $\text{Beta}(2, 2)$ prior (weak belief centered at 0.5). You observe 7 successes in 10 trials. What is the posterior distribution, and what are its mean and 95% credible interval (conceptually)?

S:
**IDENTIFY**: Beta-Binomial conjugate update. Parameter: success probability $\theta$. Prior: $\text{Beta}(\alpha, \beta)$. Likelihood: $\text{Binomial}(n, \theta)$. Goal: derive posterior and summarize it.

**PLAN**:
- Apply the Beta-Binomial conjugacy: $\theta \mid x \sim \text{Beta}(\alpha + x, \beta + n - x)$.
- Use the Beta mean formula to get the posterior mean.
- Use the 2.5th and 97.5th quantiles of the resulting Beta distribution for the 95% credible interval.

**EXECUTE**:
1. Prior: $\alpha = 2$, $\beta = 2$. Data: $n = 10$, $x = 7$.
2. Posterior: $\theta \mid x \sim \text{Beta}(2 + 7,\; 2 + 10 - 7) = \text{Beta}(9, 5)$.
3. Posterior mean: $E[\theta \mid x] = \frac{9}{9 + 5} = \frac{9}{14} \approx 0.643$.
4. 95% credible interval: $(Q_{0.025},\; Q_{0.975})$ of $\text{Beta}(9, 5)$, computed numerically (approximately $(0.39, 0.87)$).

**EVALUATE**:
- Sanity check: the posterior mean $0.643$ lies between the prior mean $0.5$ and the sample proportion $0.7$, as a Bayesian shrinkage estimator should.
- The prior contributed the equivalent of 4 pseudo-trials, the data 10 real trials, so the posterior leans toward the data but is pulled slightly toward 0.5.
- The credible interval excludes 0.5 only weakly, reflecting modest evidence of $\theta > 0.5$ with just 10 observations.

## 13.13 Posterior Summaries and Credible Intervals

Q: Why summarize a posterior distribution with a single number at all?
A: The full posterior captures all our uncertainty, but for reporting and decision-making we often need a point estimate and an interval. The choice of summary depends on loss: posterior mean minimizes squared-error loss, posterior median minimizes absolute-error loss, posterior mode (MAP) minimizes 0-1 loss.

C: The [posterior mean] $E[\theta \mid x] = \int \theta\, \pi(\theta \mid x)\, d\theta$ is the Bayes estimator under squared-error loss.

C: The [posterior mode] (also called the [maximum a posteriori] or MAP estimate) is the value of $\theta$ that maximizes $\pi(\theta \mid x)$.

C: A $100(1-\alpha)\%$ [credible interval] for $\theta$ is any interval $[a, b]$ with $P(a \leq \theta \leq b \mid x) = 1 - \alpha$, i.e., posterior probability $1 - \alpha$.

C: A credible interval chosen so that the posterior density at both endpoints is equal — and the interval has shortest length — is called a [highest posterior density] (HPD) interval.

Q: What is the difference between an equal-tailed credible interval and an HPD credible interval?
A: An equal-tailed interval puts $\alpha/2$ probability in each tail of the posterior, so its endpoints are the $\alpha/2$ and $1-\alpha/2$ quantiles. An HPD interval contains the values of $\theta$ with highest posterior density and is the shortest interval with the given coverage. They coincide for symmetric posteriors but differ for skewed ones.

## 13.14 Frequentist vs Bayesian Interpretation

Q: How does a Bayesian credible interval differ philosophically from a frequentist confidence interval?
A: A 95% credible interval $[a,b]$ means "given the data, there is a 95% probability that $\theta$ lies in $[a, b]$" — a direct statement about $\theta$. A 95% confidence interval means "if we repeated the experiment many times, 95% of such intervals would contain the true $\theta$" — a statement about the procedure, not this particular interval.

Q: Why can a frequentist NOT say "there is a 95% probability that $\theta$ is in my interval"?
A: In the frequentist framework, $\theta$ is a fixed unknown constant — it is either in the interval or not, with probability 0 or 1. The 95% refers to the long-run coverage of the procedure over repeated samples, not to the probability for any one realized interval.

C: In the Bayesian framework, the parameter $\theta$ is treated as a [random variable]; in the frequentist framework, $\theta$ is treated as a fixed unknown constant.

Q: How do Bayesian and frequentist conclusions compare as sample size grows?
A: For most reasonable priors, posterior credible intervals and frequentist confidence intervals converge: both shrink around the true value and have similar coverage. Practical disagreement is largest with small samples or strong priors, where the Bayesian answer depends noticeably on prior choice.

Q: What is one practical advantage of the Bayesian approach?
A: It delivers a full probability distribution over $\theta$, so any probability statement ("what is $P(\theta > 0.5 \mid x)$?") can be read off directly. Frequentist inference only provides reject/fail-to-reject decisions and coverage guarantees, not posterior probabilities of hypotheses.

Q: What is one practical advantage of the frequentist approach?
A: It requires no prior, so inferences cannot be criticized as reflecting the analyst's subjective beliefs. For regulated decisions (clinical trials, quality control) and well-specified repeated experiments, frequentist error rates provide clean, pre-specified operating characteristics.
