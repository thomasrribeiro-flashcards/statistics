+++
order = 2
subject = "Mathematics"
tags = ["math", "statistics", "sampling-distribution", "clt", "chi-square", "t-distribution", "f-distribution"]
+++

# Statistics — Sampling Distributions

## 2.1 Why Sampling Distributions?

Q: Why do we need the concept of a sampling distribution at all?
A: Inference tries to learn about an unknown population from a finite sample. Any statistic we compute (like the sample mean) depends on which observations happened to be drawn, so it is itself random. Its distribution — the sampling distribution — tells us how much the statistic can vary from sample to sample, which is exactly what we need to quantify uncertainty about the population.

Q: How does a sampling distribution bridge probability and inference?
A: Probability assumes a known population and asks what samples look like. Inference reverses the arrow: we see a sample and ask about the population. The sampling distribution of a statistic is the probability model that links the two — it tells us, under a hypothesized population, how the statistic behaves, so we can judge what the observed value implies.

C: The [sampling distribution] of a statistic is the probability distribution of that statistic viewed as a random variable over repeated samples from the population.

Q: Before we derive anything, predict: if a population has mean $\mu$ and we repeatedly take samples of size $n$ and compute $\bar{X}$, should the average of those $\bar{X}$ values be close to $\mu$?
A: Yes — intuitively, sample means should fluctuate around the true population mean, not systematically above or below it. Section 2.5 will show this formally: $E[\bar{X}] = \mu$.

## 2.2 Random Sample and IID Assumption

C: A [random sample] of size $n$ from a population is a collection of random variables $X_1, X_2, \ldots, X_n$ that are independent and identically distributed (iid) with the same distribution as the population.

C: The random variables $X_1, \ldots, X_n$ in a random sample are called [iid] if they are mutually independent and each has the same distribution, where $n$ is the sample size.

Q: What does "identically distributed" mean in the iid assumption?
A: Every observation $X_i$ is drawn from the same underlying distribution — same CDF, same mean $\mu$, same variance $\sigma^2$. No observation is privileged or comes from a different population.

Q: What does "independent" mean in the iid assumption?
A: The value of any $X_i$ gives no probabilistic information about any other $X_j$ — their joint distribution factors as the product of their marginals.

Q: Why is the iid assumption so central to sampling theory?
A: Independence lets us multiply probabilities and makes variances add; identical distribution guarantees a single target population $(\mu, \sigma^2)$ that every observation reflects. Without both, a statistic like $\bar{X}$ has no simple mean or variance formula, and the CLT in its basic form fails.

Q: When is iid a poor model for real data?
A: When observations are clustered (students in classrooms), ordered in time with autocorrelation (stock prices, weather), or drawn without replacement from a small finite population — all of which break independence or identical distribution.

## 2.3 Statistics as Random Variables

C: A [statistic] is any function $T = g(X_1, X_2, \ldots, X_n)$ of the sample, computed without reference to unknown parameters, where $X_1, \ldots, X_n$ is the random sample.

Q: Why is a statistic itself a random variable?
A: It is a function of random variables. Different samples produce different values of the function, so $T = g(X_1, \ldots, X_n)$ has a probability distribution — the sampling distribution.

C: A quantity like $T = g(X_1, \ldots, X_n, \mu)$ that depends on an unknown parameter $\mu$ is [not] a statistic, because a statistic must be computable from the sample alone.

Q: What is the difference between a statistic and a parameter?
A: A parameter (like $\mu$ or $\sigma^2$) is a fixed but usually unknown number describing the population. A statistic (like $\bar{X}$ or $S^2$) is a random quantity computed from the sample. Statistics are used to estimate parameters.

Q: Why do we distinguish between an observed value $t$ of a statistic and the statistic $T$ itself?
A: $T$ is the random variable (with a sampling distribution); $t$ is the specific numerical value obtained from one particular sample. Confusing them leads to statements like "the probability that $\mu = t$" instead of "the probability that $T$ falls in some interval."

## 2.4 Sampling Distribution of the Sample Mean

C: For a random sample $X_1, \ldots, X_n$, the [sample mean] is $\bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i$, where $n$ is the sample size.

Q: Why is $\bar{X}$ a random variable even though, in any given sample, it evaluates to a single number?
A: Before the sample is drawn, each $X_i$ is random, so any function of them — including the average — is random. The "single number" is one realization; the sampling distribution describes the whole range of values $\bar{X}$ could take across repeated sampling.

Q: Before deriving anything: if individual observations have variance $\sigma^2$, should the average of $n$ of them have larger or smaller variance than a single observation? Predict.
A: Smaller. Averaging cancels out independent random fluctuations, so $\bar{X}$ should be less variable than one $X_i$. The next section shows the variance shrinks by a factor of exactly $1/n$.

## 2.5 Mean, Variance, and Standard Error of $\bar{X}$

C: If $X_1, \ldots, X_n$ are iid with population mean $\mu$, then $E[\bar{X}] = [\mu]$, where $\bar{X}$ is the sample mean.

C: If $X_1, \ldots, X_n$ are iid with population variance $\sigma^2$, then $\mathrm{Var}(\bar{X}) = [\sigma^2 / n]$, where $n$ is the sample size.

Q: Why does $E[\bar{X}] = \mu$?
A: By linearity of expectation, $E[\bar{X}] = \frac{1}{n}\sum_{i=1}^n E[X_i] = \frac{1}{n}(n\mu) = \mu$. Independence is not even needed — only identical means.

Q: Why does $\mathrm{Var}(\bar{X}) = \sigma^2/n$?
A: Because the $X_i$ are independent, variances add: $\mathrm{Var}\bigl(\sum X_i\bigr) = n\sigma^2$. Dividing the sum by $n$ scales the variance by $1/n^2$, giving $\mathrm{Var}(\bar{X}) = n\sigma^2/n^2 = \sigma^2/n$.

C: The [standard error] of the sample mean is $\mathrm{SE}(\bar{X}) = \sigma/\sqrt{n}$, where $\sigma$ is the population standard deviation and $n$ is the sample size.

Q: Why is the standard error called a "standard error" rather than a "standard deviation"?
A: "Standard deviation" is reserved for the spread of individual observations or of a population. "Standard error" refers specifically to the standard deviation of a statistic (like $\bar{X}$) across repeated samples — it measures estimation error, not intrinsic variability of the data.

Q: If you quadruple the sample size, what happens to the standard error of $\bar{X}$?
A: It halves. Since $\mathrm{SE}(\bar{X}) = \sigma/\sqrt{n}$, replacing $n$ by $4n$ divides the SE by $\sqrt{4} = 2$.

Q: Why is the $\sqrt{n}$ in the denominator of the standard error often called the "square root law" of sampling?
A: Precision improves only with the square root of sample size, not linearly. To cut your estimation error in half, you need four times as much data — a fundamental and sometimes frustrating fact of sampling.

## 2.6 Central Limit Theorem for $\bar{X}$

C: [Central Limit Theorem (CLT)]: if $X_1, \ldots, X_n$ are iid with mean $\mu$ and finite variance $\sigma^2$, then as $n \to \infty$, $\frac{\bar{X} - \mu}{\sigma/\sqrt{n}}$ converges in distribution to $N(0,1)$, where $\bar{X}$ is the sample mean and $N(0,1)$ is the standard normal.

Q: Why is the CLT considered the central result of sampling theory?
A: It tells us that, regardless of the shape of the underlying population (as long as variance is finite), the sampling distribution of $\bar{X}$ becomes approximately normal for large $n$. This one result underlies most of classical inference — t-tests, confidence intervals, z-scores — without requiring knowledge of the population's distribution.

Q: For large $n$, what is the approximate sampling distribution of $\bar{X}$?
A: $\bar{X} \stackrel{\text{approx}}{\sim} N\!\left(\mu, \; \sigma^2/n\right)$, where $\mu$ is the population mean, $\sigma^2$ the population variance, and $n$ the sample size.

Q: What assumptions does the classical CLT require about the population?
A: Only finite mean $\mu$ and finite variance $\sigma^2$, plus the iid sampling assumption. No shape assumption — the population can be skewed, discrete, bimodal, etc.

Q: What does "converges in distribution" mean in the CLT statement?
A: It means that the CDF of $(\bar{X} - \mu)/(\sigma/\sqrt{n})$ approaches the standard normal CDF pointwise as $n \to \infty$. For large enough $n$, probabilities computed under the normal approximation are close to the true probabilities.

Q: What is a common rule of thumb for when the CLT gives a good approximation?
A: $n \geq 30$ is the classical rule, but it depends on the underlying distribution: near-symmetric populations need smaller $n$, heavily skewed or heavy-tailed populations may need hundreds.

## 2.7 Exact Normality When the Population is Normal

Q: What happens to the distribution of $\bar{X}$ if the underlying population is exactly normal?
A: $\bar{X}$ is exactly normal for every sample size $n$, not just asymptotically. Specifically, $\bar{X} \sim N(\mu, \sigma^2/n)$.

Q: Why is a linear combination of independent normal random variables itself normal?
A: The normal family is closed under linear combinations — if $X_i \sim N(\mu_i, \sigma_i^2)$ are independent, then $\sum a_i X_i \sim N\bigl(\sum a_i \mu_i, \sum a_i^2 \sigma_i^2\bigr)$. The sample mean is such a linear combination, so it inherits normality exactly.

C: If $X_1, \ldots, X_n$ are iid $N(\mu, \sigma^2)$, then $\bar{X} \sim N([\mu, \sigma^2/n])$ exactly for every sample size $n$.

Q: When the population is normal, why do we not need the CLT for $\bar{X}$?
A: Because normality of $\bar{X}$ is exact for every $n$, we get the normal distribution directly from closure under linear combinations. The CLT is only needed when the population is non-normal and we rely on asymptotic approximation.

## 2.8 Sampling Distribution of $S^2$

C: For a random sample, the [sample variance] is $S^2 = \frac{1}{n-1}\sum_{i=1}^{n} (X_i - \bar{X})^2$, where $n$ is the sample size and $\bar{X}$ is the sample mean.

Q: Why is the divisor $n-1$ rather than $n$ in the sample variance?
A: Using $\bar{X}$ instead of the unknown $\mu$ in the deviations $(X_i - \bar{X})$ consumes one degree of freedom: the deviations sum to zero, so only $n-1$ of them vary freely. Dividing by $n-1$ makes $S^2$ an unbiased estimator of $\sigma^2$, i.e., $E[S^2] = \sigma^2$.

Q: When $X_1, \ldots, X_n$ are iid normal, what is the exact sampling distribution of $S^2$ (after suitable scaling)?
A: $\frac{(n-1) S^2}{\sigma^2} \sim \chi^2_{n-1}$, a chi-square distribution with $n-1$ degrees of freedom, where $\sigma^2$ is the population variance and $n$ is the sample size.

C: When $X_1, \ldots, X_n$ are iid $N(\mu, \sigma^2)$, the scaled sample variance satisfies $\frac{(n-1)S^2}{\sigma^2} \sim [\chi^2_{n-1}]$, where $S^2$ is the sample variance and $n$ is the sample size.

Q: When $X_1, \ldots, X_n$ are iid normal, what is the relationship between $\bar{X}$ and $S^2$?
A: They are independent. This is a special (and deeply useful) property of the normal distribution — it fails for non-normal populations and is what makes the Student's $t$ construction clean.

Q: Why does the chi-square result for $S^2$ require the population to be normal?
A: The derivation uses that $X_i - \mu$ is normal and that sums of squared independent standard normals are chi-square. For non-normal populations, $(n-1)S^2/\sigma^2$ has a different (generally unknown) distribution and the exact chi-square result fails.

## 2.9 Chi-Square Distribution

C: If $Z_1, Z_2, \ldots, Z_k$ are iid $N(0,1)$, then $Q = \sum_{i=1}^{k} Z_i^2$ follows a [chi-square distribution] with $k$ degrees of freedom, written $Q \sim \chi^2_k$.

C: The parameter $k$ of a $\chi^2_k$ distribution is called the [degrees of freedom] and equals the number of independent standard normal variables being squared and summed.

Q: Why is the chi-square distribution always non-negative?
A: It is a sum of squares $Z_i^2 \geq 0$, so any realization is a sum of non-negative numbers and cannot be less than zero.

Q: If $Q \sim \chi^2_k$, what are $E[Q]$ and $\mathrm{Var}(Q)$?
A: $E[Q] = k$ and $\mathrm{Var}(Q) = 2k$, where $k$ is the degrees of freedom. These follow from $E[Z^2]=1$, $\mathrm{Var}(Z^2)=2$ for $Z \sim N(0,1)$, and independence.

Q: If $Q_1 \sim \chi^2_{k_1}$ and $Q_2 \sim \chi^2_{k_2}$ are independent, what is the distribution of $Q_1 + Q_2$?
A: $Q_1 + Q_2 \sim \chi^2_{k_1+k_2}$. Chi-squares add their degrees of freedom under independence — because the sum is itself a sum of $k_1 + k_2$ independent squared standard normals.

## 2.10 Student's t-Distribution

C: If $Z \sim N(0,1)$ and $V \sim \chi^2_k$ are independent, then $T = \frac{Z}{\sqrt{V/k}}$ follows a [Student's t-distribution] with $k$ degrees of freedom, written $T \sim t_k$.

Q: Why was the t-distribution invented?
A: When the population variance $\sigma^2$ is unknown and must be estimated by $S^2$, the statistic $(\bar{X}-\mu)/(S/\sqrt{n})$ is no longer exactly standard normal — the denominator is random. The t-distribution gives the exact distribution of this ratio (under normality) and accounts for the extra uncertainty from estimating $\sigma$.

C: For a random sample of size $n$ from $N(\mu, \sigma^2)$, the statistic $\frac{\bar{X}-\mu}{S/\sqrt{n}}$ follows a [$t_{n-1}$] distribution, where $\bar{X}$ is the sample mean, $S$ is the sample standard deviation, and $n$ is the sample size.

Q: Why does the t-statistic $\frac{\bar{X}-\mu}{S/\sqrt{n}}$ fit the definition $Z/\sqrt{V/k}$?
A: Write it as $\frac{(\bar{X}-\mu)/(\sigma/\sqrt{n})}{S/\sigma} = \frac{Z}{\sqrt{(n-1)S^2/\sigma^2 / (n-1)}}$. The numerator is $Z \sim N(0,1)$; the denominator's inside is a $\chi^2_{n-1}/(n-1)$; and under normality $\bar{X}$ and $S^2$ are independent — matching the ratio definition with $k = n-1$.

Q: How does the shape of $t_k$ compare to the standard normal?
A: $t_k$ is symmetric, bell-shaped, and centered at 0 like $N(0,1)$, but has heavier tails. As $k \to \infty$, $t_k \to N(0,1)$ in distribution, because $V/k \to 1$ almost surely.

Q: Why does $t_k$ have heavier tails than the standard normal for small $k$?
A: The denominator $\sqrt{V/k}$ is random and can occasionally be small, inflating the ratio. This extra variability — absent when $\sigma$ is known — spreads mass into the tails. For large $k$, $V/k$ concentrates near 1 and the extra spread disappears.

Q: For what values of $k$ does $t_k$ have no finite mean? No finite variance?
A: $t_k$ has no finite mean for $k = 1$ (the Cauchy distribution) and no finite variance for $k \leq 2$. For $k \geq 2$ the mean is 0; for $k \geq 3$ the variance is $k/(k-2)$.

## 2.11 F-Distribution

C: If $U \sim \chi^2_{k_1}$ and $V \sim \chi^2_{k_2}$ are independent, then $F = \frac{U/k_1}{V/k_2}$ follows an [F-distribution] with $(k_1, k_2)$ degrees of freedom, written $F \sim F_{k_1, k_2}$.

Q: Why does the F-distribution have two degrees-of-freedom parameters?
A: It is the ratio of two independent chi-squares, each with its own degrees of freedom. The numerator df ($k_1$) and denominator df ($k_2$) both affect the shape, so both must be specified.

Q: Where does the F-distribution naturally arise in statistics?
A: In comparing two variances. If $S_1^2$ and $S_2^2$ are sample variances from two independent normal samples with population variances $\sigma_1^2$ and $\sigma_2^2$, then $\frac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2} \sim F_{n_1-1,\; n_2-1}$, where $n_1, n_2$ are the sample sizes.

Q: If $F \sim F_{k_1, k_2}$, what is the distribution of $1/F$?
A: $1/F \sim F_{k_2, k_1}$ — the degrees of freedom swap. This follows directly from inverting the ratio of the two scaled chi-squares.

Q: If $T \sim t_k$, what is the distribution of $T^2$?
A: $T^2 \sim F_{1, k}$. Squaring a $t_k$ gives the ratio of a $\chi^2_1$ (the squared numerator) to a $\chi^2_k/k$ (the denominator), which is exactly the $F_{1,k}$ form.

## 2.12 Slutsky's Theorem

C: [Slutsky's theorem]: if $X_n \xrightarrow{d} X$ and $Y_n \xrightarrow{P} c$ (a constant), then $X_n + Y_n \xrightarrow{d} X + c$, $X_n Y_n \xrightarrow{d} cX$, and $X_n/Y_n \xrightarrow{d} X/c$ (for $c \neq 0$).

Q: What does "$X_n \xrightarrow{d} X$" mean, and what does "$Y_n \xrightarrow{P} c$" mean?
A: $X_n \xrightarrow{d} X$ means $X_n$ converges in distribution to $X$ — its CDF approaches that of $X$. $Y_n \xrightarrow{P} c$ means $Y_n$ converges in probability to the constant $c$ — for any $\varepsilon > 0$, $P(|Y_n - c| > \varepsilon) \to 0$.

Q: Why is Slutsky's theorem useful in sampling theory?
A: It lets us substitute consistent estimators for unknown constants in asymptotic arguments. For example, replacing the unknown $\sigma$ by the sample standard deviation $S$ in a limiting argument — since $S \xrightarrow{P} \sigma$ — preserves the limiting distribution.

Q: How does Slutsky's theorem justify using the sample standard deviation $S$ in place of $\sigma$ for large-sample z-intervals?
A: By the CLT, $(\bar{X}-\mu)/(\sigma/\sqrt{n}) \xrightarrow{d} N(0,1)$. Since $S/\sigma \xrightarrow{P} 1$, Slutsky's theorem gives $(\bar{X}-\mu)/(S/\sqrt{n}) \xrightarrow{d} N(0,1)$ as well. So for large $n$ we may use $S$ instead of $\sigma$ and still refer to the standard normal.

Q: Why does Slutsky's theorem not apply when $Y_n$ converges to a non-degenerate random variable rather than a constant?
A: If $Y_n \xrightarrow{d} Y$ where $Y$ is random, then $X_n$ and $Y_n$ may have arbitrary joint dependence, and $X_n + Y_n$ need not converge to $X + Y$. The theorem's power comes from $Y_n$ collapsing to a fixed number, which washes out any dependence.

## 2.13 Worked Problem: Sampling Distribution of $\bar{X}$

P: A population has mean $\mu = 50$ and standard deviation $\sigma = 10$. An iid sample of size $n = 25$ is drawn. Find $P(\bar{X} > 53)$, stating any approximations used.

S:
**IDENTIFY**: Probability question about the sample mean $\bar{X}$ from a sample of known size, known population mean, and known population standard deviation. Population shape is not specified.

**PLAN**:
- Compute $E[\bar{X}]$ and $\mathrm{SE}(\bar{X}) = \sigma/\sqrt{n}$.
- With $n = 25$, invoke the CLT to approximate $\bar{X}$ as normal.
- Standardize and read the tail probability from $N(0,1)$.

**EXECUTE**:
1. $E[\bar{X}] = \mu = 50$ and $\mathrm{SE}(\bar{X}) = \sigma/\sqrt{n} = 10/\sqrt{25} = 2$.
2. By the CLT, $\bar{X} \stackrel{\text{approx}}{\sim} N(50, 2^2)$.
3. Standardize: $Z = \frac{\bar{X} - 50}{2}$, so $P(\bar{X} > 53) = P\!\left(Z > \frac{53-50}{2}\right) = P(Z > 1.5)$.
4. From standard normal tables, $P(Z > 1.5) \approx 0.0668$.

**EVALUATE**:
- Answer: $P(\bar{X} > 53) \approx 0.067$ (about 6.7%).
- Sanity check: 53 is 1.5 standard errors above the mean, so a right-tail probability near 7% is consistent with $N(0,1)$ tail values.
- Caveat: the CLT approximation quality depends on the unspecified population shape. For symmetric light-tailed populations, $n = 25$ is typically fine; for very skewed populations the true probability could differ.

## 2.14 Worked Problem: Using the t-Distribution

P: A random sample of size $n = 10$ is drawn from a $N(\mu, \sigma^2)$ population with unknown $\mu$ and unknown $\sigma^2$. The observed sample mean is $\bar{x} = 4.2$ and the observed sample standard deviation is $s = 1.5$. Find the distribution of the statistic $T = \frac{\bar{X} - \mu}{S/\sqrt{n}}$ and compute the observed value $t$ if the hypothesized value of $\mu$ is $3.5$.

S:
**IDENTIFY**: Normal population with both parameters unknown, small sample size. The natural pivot is the t-statistic.

**PLAN**:
- Identify the degrees of freedom from the sample size.
- State the sampling distribution of $T$.
- Plug the observed values into the formula to compute $t$.

**EXECUTE**:
1. Under iid $N(\mu, \sigma^2)$ sampling, $T = \frac{\bar{X}-\mu}{S/\sqrt{n}} \sim t_{n-1}$.
2. With $n = 10$, degrees of freedom $= n - 1 = 9$, so $T \sim t_9$.
3. Compute $\mathrm{se} = s/\sqrt{n} = 1.5/\sqrt{10} \approx 0.4743$.
4. Observed statistic: $t = (4.2 - 3.5)/0.4743 \approx 1.476$.

**EVALUATE**:
- $T$ has a Student's $t$-distribution with 9 degrees of freedom, symmetric around 0, with heavier tails than $N(0,1)$.
- Observed $t \approx 1.48$ is about 1.5 standard errors above the hypothesized mean — moderate but not extreme for $t_9$.
- Note: we used $S$ (not $\sigma$), so $t_9$ is the correct reference distribution; using $N(0,1)$ would understate tail probabilities for $n = 10$.
