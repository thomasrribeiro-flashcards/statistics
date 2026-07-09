+++
order = 4
subject = "Math"
tags = ["math", "statistics", "estimators", "bias", "mse", "consistency", "efficiency", "cramer-rao"]
+++

# Statistics — Properties of Estimators

## 4.1 Why Evaluate Estimators?

Q: Why do we need criteria for comparing estimators rather than just picking one?
A: For any parameter $\theta$, infinitely many functions of the sample could serve as estimators — the sample mean, median, trimmed mean, first observation, and countless others. Without objective criteria, we cannot say which estimator is "better." Properties like bias, variance, MSE, consistency, and efficiency provide the language to rank estimators and choose the best one for a given task.

Q: Why isn't it enough for an estimator to "seem reasonable"?
A: An estimator may seem intuitive yet be systematically wrong (biased), highly unstable (large variance), or fail to improve as more data arrives (inconsistent). Formal criteria expose these flaws, which intuition alone can miss.

C: An [estimator] $\hat{\theta}$ of a parameter $\theta$ is a function of the sample $X_1, \ldots, X_n$ used to approximate $\theta$; an [estimate] is the numerical value obtained from a specific sample.

Q: Why is an estimator a random variable, while an estimate is just a number?
A: An estimator is a function of the random sample, so before the data is observed it inherits randomness from the $X_i$. Once the sample is observed, the estimator is evaluated at specific numbers, producing a single fixed estimate.

## 4.2 Bias

Q: Before defining bias, predict: if an estimator tends to overshoot $\theta$ on average, should its "bias" be positive or negative?
A: Positive — bias captures the systematic deviation of $E[\hat{\theta}]$ from $\theta$, so an estimator that overshoots on average has $E[\hat{\theta}] > \theta$ and hence positive bias.

C: The [bias] of an estimator $\hat{\theta}$ of $\theta$ is $E\lbrack \hat{\theta}\rbrack  - \theta$, the difference between the estimator's expected value and the true parameter value.

Q: What does bias measure conceptually?
A: The systematic error of an estimator — how far its average value (over all possible samples of size $n$) lies from the true parameter. It is a property of the estimator's distribution, not of any single estimate.

Q: Can a single estimate be "biased"?
A: No. Bias is a property of the estimator (a random variable) across its entire sampling distribution. A single estimate is just a number; it can be close to or far from $\theta$, but it cannot itself be biased.

## 4.3 Unbiased Estimators

C: An estimator $\hat{\theta}$ is called [unbiased] for $\theta$ if $E\lbrack \hat{\theta}\rbrack  = \theta$ for every value of $\theta$ in the parameter space.

Q: Why is unbiasedness desirable?
A: An unbiased estimator has no systematic error — averaged over many samples, it centers exactly on the true parameter. This makes it a natural starting point for estimation and a baseline for comparing other estimators.

Q: Why isn't unbiasedness alone sufficient to declare an estimator "good"?
A: An unbiased estimator can still have huge variance, producing wildly different estimates from different samples. A biased estimator with small variance may be more reliable overall. Unbiasedness is one desirable property among several.

Q: Why is the sample mean $\bar{X} = \frac{1}{n}\sum_{i=1}^n X_i$ an unbiased estimator of the population mean $\mu$?
A: By linearity of expectation, $E[\bar{X}] = \frac{1}{n}\sum_{i=1}^n E[X_i] = \frac{1}{n}(n\mu) = \mu$, where $\mu = E[X_i]$ is the common mean of the i.i.d. sample. So $E[\bar{X}] = \mu$ for every $\mu$.

Q: Why does the sample variance use $n-1$ rather than $n$ in the denominator?
A: Dividing by $n-1$ instead of $n$ makes the sample variance $S^2 = \frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X})^2$ unbiased for $\sigma^2$. The subtraction of $\bar{X}$ (estimated from the same data) removes one degree of freedom, so dividing by $n-1$ corrects the resulting downward bias.

C: The [sample variance] $S^2 = \frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X})^2$ is an unbiased estimator of $\sigma^2$, where $X_i$ is the $i$th observation, $\bar{X}$ is the sample mean, and $n$ is the sample size.

C: The estimator $\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (X_i - \bar{X})^2$ is [biased] for $\sigma^2$: its expectation equals $\frac{n-1}{n}\sigma^2$, which underestimates the true variance.

## 4.4 Mean Squared Error

Q: Before defining MSE, predict: how should a good measure of estimator accuracy combine bias and variance?
A: It should penalize both — systematic error (bias) and random scatter (variance) both push estimates away from $\theta$. A natural combination is to square the total error and take its expectation, yielding MSE.

C: The [mean squared error] of an estimator $\hat{\theta}$ is $\mathrm{MSE}(\hat{\theta}) = E\lbrack (\hat{\theta} - \theta)^2\rbrack $, where $\hat{\theta}$ is the estimator and $\theta$ is the true parameter.

C: The MSE of any estimator decomposes as $\mathrm{MSE}(\hat{\theta}) = \mathrm{Var}(\hat{\theta}) + [\mathrm{Bias}(\hat{\theta})]^2$, where the first term is the variance of the estimator and the second is the squared bias.

Q: Why does the MSE decomposition $\mathrm{MSE} = \mathrm{Var} + \mathrm{Bias}^2$ hold?
A: Write $\hat{\theta} - \theta = (\hat{\theta} - E[\hat{\theta}]) + (E[\hat{\theta}] - \theta)$. Squaring and taking expectation: the cross term has expectation zero (since $E[\hat{\theta} - E[\hat{\theta}]] = 0$), leaving $E[(\hat{\theta} - E[\hat{\theta}])^2] + (E[\hat{\theta}] - \theta)^2 = \mathrm{Var}(\hat{\theta}) + \mathrm{Bias}(\hat{\theta})^2$.

Q: For an unbiased estimator, what does MSE reduce to?
A: The variance. If $\mathrm{Bias}(\hat{\theta}) = 0$, then $\mathrm{MSE}(\hat{\theta}) = \mathrm{Var}(\hat{\theta})$, so comparing unbiased estimators by MSE is the same as comparing them by variance.

Q: Why is MSE often preferred to bias or variance alone as a comparison criterion?
A: MSE captures total expected squared deviation from the true parameter. It treats systematic error and random error on the same footing, so a single number summarizes overall accuracy — letting a slightly biased but low-variance estimator beat an unbiased but high-variance one.

## 4.5 Bias-Variance Tradeoff

Q: What is the bias-variance tradeoff?
A: The phenomenon that reducing an estimator's bias often increases its variance, and vice versa. Optimizing MSE requires balancing the two: a small amount of bias may be worthwhile if it buys a large reduction in variance, lowering total MSE.

Q: Why might a biased estimator beat an unbiased one on MSE?
A: Because MSE = variance + bias$^2$. If a biased estimator has much smaller variance than any unbiased competitor, the variance savings can outweigh the squared bias penalty, giving lower MSE overall.

C: Adding a small amount of [bias] to an estimator can reduce its variance enough to lower its total MSE.

Q: Give an intuitive example of the bias-variance tradeoff in practice.
A: Shrinkage estimators (e.g., James–Stein, ridge regression) deliberately pull estimates toward zero or a prior guess. This introduces bias but sharply reduces variance, producing lower MSE than the unbiased MLE when the number of parameters is large.

## 4.6 Consistency

Q: Why care about large-sample behavior of an estimator?
A: We want assurance that gathering more data actually helps. An estimator that is accurate only for small samples, or that never converges to $\theta$ no matter how much data we collect, provides weak grounds for inference. Consistency formalizes the expectation that estimates improve as $n$ grows.

C: An estimator $\hat{\theta}_n$ (based on a sample of size $n$) is [consistent] for $\theta$ if $\hat{\theta}_n$ converges in probability to $\theta$ as $n \to \infty$: for every $\epsilon > 0$, $P(|\hat{\theta}_n - \theta| > \epsilon) \to 0$.

Q: What does "converges in probability" mean in plain language?
A: For any tolerance $\epsilon > 0$, the chance that the estimator deviates from $\theta$ by more than $\epsilon$ can be made arbitrarily small by taking $n$ large enough. The estimator gets arbitrarily close to $\theta$ with probability approaching 1.

Q: Why is the sample mean $\bar{X}_n$ a consistent estimator of $\mu$?
A: The weak law of large numbers states that if $X_1, X_2, \ldots$ are i.i.d. with finite mean $\mu$, then $\bar{X}_n$ converges in probability to $\mu$. So by definition, $\bar{X}_n$ is consistent for $\mu$.

Q: Why is an unbiased estimator not automatically consistent?
A: Unbiasedness only says $E[\hat{\theta}_n] = \theta$ for all $n$; it does not constrain the variance. If $\mathrm{Var}(\hat{\theta}_n)$ does not shrink to zero, the estimator can be unbiased yet scatter widely forever and fail to converge.

Q: Why can a consistent estimator fail to be unbiased?
A: Consistent estimators may be biased at every finite $n$, as long as both the bias and the variance shrink to zero as $n \to \infty$. For example, $\frac{1}{n}\sum (X_i - \bar{X})^2$ is biased for $\sigma^2$ but consistent.

## 4.7 Sufficient Condition for Consistency

Q: Why look for a convenient sufficient condition for consistency rather than checking convergence in probability directly?
A: Verifying $P(|\hat{\theta}_n - \theta| > \epsilon) \to 0$ from first principles is usually hard. A sufficient condition involving means and variances (which we can often compute) turns a limit statement about probabilities into a manageable algebraic check.

C: If $\mathrm{MSE}(\hat{\theta}_n) \to 0$ as $n \to \infty$, then $\hat{\theta}_n$ is a [consistent] estimator of $\theta$.

Q: Why does MSE $\to 0$ imply consistency?
A: By Markov's inequality applied to $(\hat{\theta}_n - \theta)^2$, $P(|\hat{\theta}_n - \theta| > \epsilon) \le \mathrm{MSE}(\hat{\theta}_n)/\epsilon^2$. If the right side tends to zero, so does the left, which is exactly convergence in probability.

Q: Using the MSE criterion, what two conditions together guarantee consistency?
A: $\mathrm{Bias}(\hat{\theta}_n) \to 0$ and $\mathrm{Var}(\hat{\theta}_n) \to 0$ as $n \to \infty$. Since $\mathrm{MSE} = \mathrm{Var} + \mathrm{Bias}^2$, both parts vanishing forces MSE to zero, which in turn forces consistency.

Q: Why is MSE $\to 0$ only sufficient, not necessary, for consistency?
A: An estimator can be consistent without having a finite MSE at all — for example, if the estimator has heavy-tailed distribution, its second moment may be infinite while convergence in probability still holds.

## 4.8 Efficiency and Relative Efficiency

Q: Why do we need a notion of "efficiency" in addition to unbiasedness?
A: Among unbiased estimators, some are more tightly concentrated around $\theta$ than others. Efficiency ranks unbiased estimators by how small their variance is — smaller variance means more information extracted from the same sample.

C: Among unbiased estimators of $\theta$, the one with the smallest variance is called the [most efficient] (or minimum-variance unbiased) estimator.

C: The [relative efficiency] of unbiased estimator $\hat{\theta}_1$ with respect to unbiased estimator $\hat{\theta}_2$ is $\mathrm{RE}(\hat{\theta}_1, \hat{\theta}_2) = \mathrm{Var}(\hat{\theta}_2) / \mathrm{Var}(\hat{\theta}_1)$.

Q: How do you interpret a relative efficiency of 2?
A: $\mathrm{RE}(\hat{\theta}_1, \hat{\theta}_2) = 2$ means $\hat{\theta}_1$ has half the variance of $\hat{\theta}_2$, so $\hat{\theta}_1$ is twice as efficient — equivalently, $\hat{\theta}_2$ needs roughly twice as many observations to match the precision of $\hat{\theta}_1$.

Q: Why does minimizing variance among unbiased estimators make sense?
A: Since all competing estimators have the same mean (equal to $\theta$), the one with smallest variance has the narrowest sampling distribution around $\theta$. It gives estimates that are on average correct and individually most reliable.

## 4.9 Fisher Information

Q: Why do we need a quantity that measures how much "information" data carries about $\theta$?
A: Intuitively, a likelihood that changes sharply with $\theta$ near the truth is very informative — nearby parameter values produce very different data distributions, so the data pins down $\theta$ tightly. A dull, flat likelihood carries little information. Fisher information makes this precise.

C: The [Fisher information] $I(\theta)$ for a single observation with density $f(x; \theta)$ is $I(\theta) = E\!\left\lbrack \left(\frac{\partial \log f(X; \theta)}{\partial \theta}\right)^2\right\rbrack $, where the expectation is taken with respect to $X \sim f(\cdot; \theta)$.

C: Under regularity conditions, Fisher information can also be written as $I(\theta) = -E\!\left[\frac{\partial^2 \log f(X; \theta)}{\partial \theta^2}\right]$, where the expectation is over $X \sim f(\cdot; \theta)$.

Q: What does Fisher information measure intuitively?
A: The expected curvature (second derivative) of the log-likelihood near the true $\theta$. Higher curvature = a sharper peak = data that pins down $\theta$ precisely. Lower curvature = a flatter likelihood = less informative data.

Q: Why does Fisher information for an i.i.d. sample of size $n$ equal $n I(\theta)$?
A: Independent observations contribute additively to the log-likelihood ($\log \prod f(X_i;\theta) = \sum \log f(X_i;\theta)$), so the expected squared score of the sum is $n$ times the expected squared score of a single observation. Doubling the sample doubles the information.

## 4.10 Cramér–Rao Lower Bound

Q: Why might there be a theoretical lower bound on the variance of an unbiased estimator?
A: Data carries a finite amount of information about $\theta$, quantified by Fisher information. No unbiased estimator can be more precise than that information allows — so there must be a variance floor set by $I(\theta)$ and sample size $n$.

C: The [Cramér–Rao lower bound] (CRLB) states that for any unbiased estimator $\hat{\theta}$ of $\theta$ based on an i.i.d. sample of size $n$, $\mathrm{Var}(\hat{\theta}) \ge \frac{1}{n I(\theta)}$, where $I(\theta)$ is the Fisher information for one observation.

Q: What does the Cramér–Rao lower bound tell us about "how good" an unbiased estimator can be?
A: It gives a universal floor: no unbiased estimator can have variance smaller than $1/[n I(\theta)]$. An estimator that attains this bound is the best possible unbiased estimator (in variance), and no amount of cleverness can do better without giving up unbiasedness.

C: An unbiased estimator whose variance equals the Cramér–Rao lower bound is called [efficient] (it attains the minimum possible variance).

Q: If an unbiased estimator has variance strictly greater than $1/[nI(\theta)]$, can we conclude it is not the best?
A: Not necessarily. The CRLB is a lower bound, not always attainable — in some problems, no unbiased estimator reaches it. An estimator may still be the minimum-variance unbiased estimator (MVUE) even though its variance exceeds the CRLB.

Q: How is Fisher information linked to the Cramér–Rao lower bound?
A: The CRLB says variance $\ge 1/[nI(\theta)]$. More Fisher information per observation (sharper likelihood) means a lower bound, so unbiased estimators can potentially be more precise. Fisher information sets the information budget; CRLB converts it into a precision limit.

## 4.11 Asymptotic Normality of the MLE

Q: Why is it useful to know the asymptotic distribution of the MLE, not just its consistency?
A: Consistency alone tells us the MLE converges to $\theta$ but not how fast or with what shape of error. Asymptotic normality gives the rate ($1/\sqrt{n}$) and the limiting distribution (normal), enabling confidence intervals and hypothesis tests for large samples.

C: Under regularity conditions, the maximum likelihood estimator $\hat{\theta}_{\mathrm{MLE}}$ based on an i.i.d. sample of size $n$ is [asymptotically normal]: $\sqrt{n}(\hat{\theta}_{\mathrm{MLE}} - \theta) \xrightarrow{d} N(0,\, 1/I(\theta))$, where $I(\theta)$ is the Fisher information for one observation.

Q: Why is the MLE often described as "asymptotically efficient"?
A: Its limiting variance $1/I(\theta)$ matches the Cramér–Rao lower bound per observation. So for large $n$, no unbiased estimator can do better than the MLE — it attains the information-theoretic precision floor asymptotically.

Q: What is the approximate distribution of the MLE in large samples?
A: $\hat{\theta}_{\mathrm{MLE}} \approx N\!\left(\theta,\, \frac{1}{n I(\theta)}\right)$ for large $n$, where $\theta$ is the true parameter and $n I(\theta)$ is the total Fisher information in the sample. This approximation underpins standard Wald-type confidence intervals.

## 4.12 Sufficiency

Q: Why might we want a "sufficient statistic" rather than keeping the whole sample?
A: If a statistic $T(X_1,\ldots,X_n)$ captures every bit of information the data contain about $\theta$, then working with $T$ alone is as good as working with the raw data for inference about $\theta$. This compresses the data without loss and simplifies estimation theory.

C: A statistic $T(X_1, \ldots, X_n)$ is [sufficient] for $\theta$ if the conditional distribution of the sample given $T$ does not depend on $\theta$.

Q: What is the intuition behind sufficiency?
A: Once you know $T$, the specific values of the raw data carry no further information about $\theta$ — any residual variability is "parameter-free noise." So $T$ alone is enough for any inference about $\theta$.

C: [Factorization theorem] (Fisher–Neyman): $T$ is sufficient for $\theta$ if and only if the joint density factors as $f(x_1, \ldots, x_n;\theta) = g(T(x_1,\ldots,x_n);\theta) \cdot h(x_1,\ldots,x_n)$, where $g$ depends on the data only through $T$ and $h$ does not depend on $\theta$.

Q: How does the factorization theorem make sufficiency easier to check in practice?
A: Rather than verifying that a conditional distribution is parameter-free (often analytically intractable), you only need to factor the joint density into a $\theta$-dependent piece involving $T$ and a $\theta$-free piece involving the raw data. If such a factorization exists, $T$ is sufficient.

Q: For an i.i.d. sample from $N(\mu, \sigma^2)$ with $\sigma^2$ known, why is $\bar{X}$ sufficient for $\mu$?
A: The joint density factors as a function of $\sum X_i$ (equivalently $\bar{X}$) and $\mu$, times a piece depending only on the $X_i$ and $\sigma^2$ but not on $\mu$. By the factorization theorem, $\bar{X}$ is sufficient for $\mu$.
