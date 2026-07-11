+++
order = 3
subject = "mathematics"
tags = ["math", "statistics", "estimation", "mle", "method-of-moments", "likelihood"]
+++

# Statistics — Point Estimation

## 3.1 Why Point Estimation?

Q: Why do we need point estimation at all?
A: In practice we almost never know the true parameters of a population (e.g. the mean $\mu$ of a distribution). All we have is a finite sample drawn from that population. Point estimation provides a principled way to use that sample to produce a single best guess for an unknown parameter, so that we can make decisions and predictions without knowing the full distribution.

Q: What is the basic setup of a point estimation problem?
A: We assume data $X_1, \ldots, X_n$ are i.i.d. from a distribution $f(x; \theta)$ whose form is known but whose parameter $\theta$ is unknown. The goal is to use the sample to produce a single numerical guess $\hat{\theta}$ for $\theta$.

C: A [point estimate] is a single numerical value used as a best guess for an unknown population parameter $\theta$, based on sample data.

C: In point estimation, the [parameter] $\theta$ is a fixed but unknown constant describing the population, while the sample $X_1, \ldots, X_n$ is random.

Q: Why is point estimation called "point" estimation?
A: Because it produces a single number (a point in parameter space) as the guess for $\theta$, as opposed to interval estimation, which produces a range of plausible values.

## 3.2 Estimator vs Estimate

Q: Why do we distinguish between an "estimator" and an "estimate"?
A: An estimator is a rule (a function of the random sample) — it is itself a random variable with a distribution. An estimate is the specific number produced when that rule is applied to an observed sample. Confusing the two leads to errors: probability statements (bias, variance) apply to the estimator; a reported value is an estimate.

C: An [estimator] of a parameter $\theta$ is a function $\hat{\theta} = T(X_1, \ldots, X_n)$ of the random sample; it is a random variable before data are observed.

C: An [estimate] is the realized numerical value $\hat{\theta} = T(x_1, \ldots, x_n)$ obtained by evaluating an estimator on an observed sample.

Q: Is the sample mean $\bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i$ an estimator or an estimate?
A: As written with capital $X_i$, it is an estimator — a random variable (a function of the random sample). Once we plug in observed numbers $x_1, \ldots, x_n$ to get $\bar{x} = 2.37$, that number is an estimate.

Q: Why does it make sense to talk about the "distribution of an estimator" but not the "distribution of an estimate"?
A: An estimator is a function of random variables, so it has a distribution across possible samples. An estimate is one realized number, which has no distribution — it is a fixed observed value.

## 3.3 Method of Moments

Q: What is the core idea behind the method of moments?
A: The population moments $E[X^k]$ are functions of the unknown parameter(s). The sample moments $\frac{1}{n}\sum_{i=1}^{n} X_i^k$ are observable. By equating population moments to sample moments and solving for the parameters, we obtain estimators.

C: The [$k$-th population moment] is $\mu_k = E\lbrack X^k\rbrack $, where $X$ is a random variable from the population distribution.

C: The [$k$-th sample moment] is $m_k = \frac{1}{n}\sum_{i=1}^{n} X_i^k$, where $X_1, \ldots, X_n$ is an i.i.d. sample and $n$ is the sample size.

Q: How many moment equations do you need for a distribution with $p$ unknown parameters?
A: Exactly $p$ equations. You equate the first $p$ population moments to the first $p$ sample moments and solve the resulting system of $p$ equations in $p$ unknowns.

Q: Why does the method of moments work — i.e. why should sample moments approximate population moments?
A: By the law of large numbers, each sample moment $m_k = \frac{1}{n}\sum X_i^k$ converges in probability to the corresponding population moment $E[X^k]$ as $n \to \infty$. So matching the two is asymptotically justified.

## 3.4 Method of Moments Examples

P: Find the method-of-moments estimator of $\mu$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} f(x; \mu)$ with $E[X] = \mu$.

S:
**IDENTIFY**: One unknown parameter ($\mu$), so we need one moment equation.

**PLAN**:
- Compute the first population moment as a function of $\mu$.
- Set it equal to the first sample moment $\bar{X}$.
- Solve for $\mu$.

**EXECUTE**:
1. Population moment: $E[X] = \mu$.
2. Sample moment: $m_1 = \frac{1}{n}\sum_{i=1}^n X_i = \bar{X}$.
3. Equation: $\mu = \bar{X}$.
4. Solution: $\hat{\mu}_{\mathrm{MoM}} = \bar{X}$.

**EVALUATE**: The sample mean is the MoM estimator of the population mean. This is consistent (by the LLN) and unbiased ($E[\bar{X}] = \mu$).

P: Find the method-of-moments estimators of $\mu$ and $\sigma^2$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} N(\mu, \sigma^2)$.

S:
**IDENTIFY**: Two unknown parameters ($\mu, \sigma^2$), so we need two moment equations.

**PLAN**:
- First moment gives $\mu$.
- Second moment gives $\sigma^2$ via $E[X^2] = \mu^2 + \sigma^2$.

**EXECUTE**:
1. $E[X] = \mu = \bar{X}$, so $\hat{\mu} = \bar{X}$.
2. $E[X^2] = \mu^2 + \sigma^2 = \frac{1}{n}\sum_{i=1}^n X_i^2$.
3. Solve: $\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n X_i^2 - \bar{X}^2 = \frac{1}{n}\sum_{i=1}^n (X_i - \bar{X})^2$.

**EVALUATE**: The MoM variance estimator uses divisor $n$, not $n-1$. It is therefore biased (underestimates $\sigma^2$), but it is consistent as $n \to \infty$.

P: Find the method-of-moments estimator of $\theta$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} \mathrm{Uniform}(0, \theta)$.

S:
**IDENTIFY**: One unknown parameter $\theta$ (the upper bound of the support).

**PLAN**: Use the first moment of the uniform distribution.

**EXECUTE**:
1. Population moment: $E[X] = \theta/2$.
2. Equation: $\theta/2 = \bar{X}$.
3. Solution: $\hat{\theta}_{\mathrm{MoM}} = 2\bar{X}$.

**EVALUATE**: This estimator can produce values smaller than the largest observation $X_{(n)}$, which is logically impossible since $\theta \geq X_{(n)}$. This flaw motivates alternative estimators (e.g. the MLE, which is $X_{(n)}$).

Q: Why can $\hat{\theta}_{\mathrm{MoM}} = 2\bar{X}$ give a nonsensical estimate for $\mathrm{Uniform}(0, \theta)$?
A: Because $2\bar{X}$ can fall below the largest observed value $X_{(n)}$, yet every observation must lie in $[0, \theta]$, so $\theta \geq X_{(n)}$. MoM does not use this support constraint.

## 3.5 Likelihood Function

Q: Why introduce the likelihood function instead of staying with moment equations?
A: The likelihood uses the full density, not just a couple of moments, so it captures all the information the model assigns to each possible parameter. This leads to estimators with strong theoretical properties (consistency, asymptotic efficiency) that MoM generally lacks.

C: The [likelihood function] $L(\theta)$ for i.i.d. data $x_1, \ldots, x_n$ from density $f(x; \theta)$ is $L(\theta) = \prod_{i=1}^{n} f(x_i; \theta)$, where $\theta$ is the unknown parameter and $n$ is the sample size.

Q: What is the key conceptual difference between the density $f(x; \theta)$ and the likelihood $L(\theta)$?
A: The density is a function of $x$ with $\theta$ fixed — it describes the probability of data for a known parameter. The likelihood is the same formula viewed as a function of $\theta$ with the data $x$ fixed — it measures how plausible each $\theta$ is given the observed data.

Q: Why does the likelihood multiply the densities $f(x_i; \theta)$ across observations?
A: Because the observations are assumed independent. For independent events, the joint density factors into a product of marginal densities, so the joint density of the whole sample is $\prod_{i=1}^{n} f(x_i; \theta)$.

C: The likelihood $L(\theta)$ is [not a probability distribution over $\theta$] — it does not integrate to 1 over $\theta$, and its absolute scale is meaningless (only ratios matter).

## 3.6 Log-Likelihood

Q: Why do we usually work with the log-likelihood instead of the likelihood?
A: Products of small numbers underflow numerically and are hard to differentiate. Taking the log turns products into sums and preserves the location of the maximum (log is strictly increasing), so differentiation and optimization become much easier without changing the answer.

C: The [log-likelihood] is $\ell(\theta) = \log L(\theta) = \sum_{i=1}^{n} \log f(x_i; \theta)$, where $f(x; \theta)$ is the density and $n$ is the sample size.

Q: Why does maximizing $\ell(\theta)$ give the same answer as maximizing $L(\theta)$?
A: Because $\log$ is strictly monotonically increasing, so $L(\theta_1) \leq L(\theta_2)$ iff $\log L(\theta_1) \leq \log L(\theta_2)$. The maximizer is preserved exactly.

C: Taking the log converts the product $\prod f(x_i; \theta)$ into a [sum] $\sum \log f(x_i; \theta)$, which is analytically much easier to differentiate.

## 3.7 Maximum Likelihood Estimator (MLE)

C: The [maximum likelihood estimator] (MLE) of $\theta$ is $\hat{\theta}_{\mathrm{MLE}} = \arg\max_{\theta} L(\theta)$, the value of $\theta$ that makes the observed data most probable under the model.

Q: Intuitively, why is the MLE a good choice of estimator?
A: It picks the parameter value that makes the data we actually observed most probable. Among all candidate parameters, the MLE is the one under which our sample is least "surprising."

C: Equivalently, $\hat{\theta}_{\mathrm{MLE}} = \arg\max_{\theta} \ell(\theta)$, since $\log$ is strictly increasing and preserves the [argmax].

Q: Before learning MLE: if you saw a coin land heads 9 out of 10 times, what value of $p$ (probability of heads) would make that outcome most likely?
A: $p = 0.9$. Any other value makes the sequence "9 heads out of 10" strictly less probable. This intuition is precisely what MLE formalizes.

## 3.8 MLE via Calculus

Q: Why do we set $\partial \ell / \partial \theta = 0$ to find the MLE?
A: A smooth function is maximized (in the interior of its domain) at a critical point where its derivative vanishes. If $\ell(\theta)$ is differentiable and its maximum is interior, the MLE satisfies $\ell'(\theta) = 0$.

Q: Why must we also check the second derivative when finding an MLE?
A: The first-order condition $\ell'(\theta) = 0$ identifies any critical point — maximum, minimum, or saddle. We need $\ell''(\hat{\theta}) < 0$ to confirm it is a local maximum rather than a minimum or inflection.

C: The [score function] is $U(\theta) = \partial \ell / \partial \theta$; the MLE solves $U(\hat{\theta}) = 0$ (the score equation).

P: What is the general recipe for computing an MLE by calculus?

S:
**IDENTIFY**: Interior maximization of a smooth log-likelihood for parameter $\theta$.

**PLAN**: Reduce the joint density to $\ell(\theta)$, differentiate, solve, and verify.

**EXECUTE**:
1. Write $L(\theta) = \prod_{i=1}^{n} f(x_i; \theta)$.
2. Take the log: $\ell(\theta) = \sum_{i=1}^{n} \log f(x_i; \theta)$.
3. Compute $\ell'(\theta) = \partial \ell / \partial \theta$.
4. Solve $\ell'(\theta) = 0$ for $\theta$ to get the candidate $\hat{\theta}$.
5. Check $\ell''(\hat{\theta}) < 0$ (second-derivative test) to confirm it is a maximum.

**EVALUATE**:
- If the parameter space has boundaries (e.g. $\theta > 0$), also check the boundary — the maximum may not be interior.
- If multiple parameters, compute the gradient and Hessian and verify negative-definiteness.

Q: Why might the calculus approach to MLE fail?
A: It assumes the maximum is interior and the log-likelihood is differentiable there. If the maximum lies on the boundary of the parameter space (e.g. for $\mathrm{Uniform}(0, \theta)$) or the likelihood is not smooth in $\theta$, setting $\ell'(\theta) = 0$ gives no valid critical point and the MLE must be found by inspection.

## 3.9 Invariance of MLE

C: [Invariance of MLE]: If $\hat{\theta}$ is the MLE of $\theta$ and $g$ is any function, then $g(\hat{\theta})$ is the MLE of $g(\theta)$.

Q: Why is the invariance property of MLE so useful?
A: It means you don't have to redo the optimization for transformed parameters. Once you have $\hat{\theta}$, you can immediately write down the MLE of any function of $\theta$ (standard deviation from variance, odds from probability, etc.) by plugging in.

Q: If $\hat{\sigma}^2$ is the MLE of $\sigma^2$, what is the MLE of $\sigma$?
A: By invariance, $\hat{\sigma} = \sqrt{\hat{\sigma}^2}$. No separate optimization needed.

Q: If $\hat{p}$ is the MLE of the success probability $p$ in a Bernoulli model, what is the MLE of the odds $p/(1-p)$?
A: By invariance, $\hat{p}/(1 - \hat{p})$ is the MLE of the odds.

## 3.10 MLE Examples

P: Find the MLE of $p$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} \mathrm{Bernoulli}(p)$.

S:
**IDENTIFY**: Discrete MLE with one parameter $p \in (0, 1)$.

**PLAN**: Write the pmf, take the log, differentiate, solve.

**EXECUTE**:
1. PMF: $f(x; p) = p^x (1-p)^{1-x}$ for $x \in \{0, 1\}$.
2. Likelihood: $L(p) = p^{\sum x_i}(1-p)^{n - \sum x_i}$.
3. Log-likelihood: $\ell(p) = \left(\sum_{i=1}^n x_i\right)\log p + \left(n - \sum_{i=1}^n x_i\right)\log(1-p)$.
4. Derivative: $\ell'(p) = \frac{\sum x_i}{p} - \frac{n - \sum x_i}{1-p}$.
5. Set to zero and solve: $\hat{p} = \frac{1}{n}\sum_{i=1}^n x_i = \bar{x}$.

**EVALUATE**: $\ell''(\hat{p}) < 0$, confirming a maximum. The MLE is the sample proportion of successes — matches intuition.

P: Find the MLE of $\mu$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} N(\mu, \sigma^2)$ with $\sigma^2$ known.

S:
**IDENTIFY**: Continuous MLE with one parameter $\mu \in \mathbb{R}$.

**PLAN**: Normal log-likelihood is quadratic in $\mu$, so differentiation is straightforward.

**EXECUTE**:
1. $\ell(\mu) = -\frac{n}{2}\log(2\pi\sigma^2) - \frac{1}{2\sigma^2}\sum_{i=1}^n (x_i - \mu)^2$.
2. $\ell'(\mu) = \frac{1}{\sigma^2}\sum_{i=1}^n (x_i - \mu)$.
3. Setting $\ell'(\mu) = 0$: $\sum_{i=1}^n (x_i - \mu) = 0 \Rightarrow \hat{\mu} = \bar{x}$.

**EVALUATE**: $\ell''(\mu) = -n/\sigma^2 < 0$, confirming a maximum. MLE equals MoM equals sample mean.

P: Find the MLE of $\sigma^2$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} N(\mu, \sigma^2)$ with both $\mu$ and $\sigma^2$ unknown.

S:
**IDENTIFY**: Two-parameter MLE; need gradient set to zero.

**PLAN**: From $\partial \ell / \partial \mu = 0$ get $\hat{\mu} = \bar{x}$. Substitute and solve $\partial \ell / \partial \sigma^2 = 0$.

**EXECUTE**:
1. $\ell(\mu, \sigma^2) = -\frac{n}{2}\log(2\pi\sigma^2) - \frac{1}{2\sigma^2}\sum_{i=1}^n (x_i - \mu)^2$.
2. $\partial \ell / \partial \mu = 0 \Rightarrow \hat{\mu} = \bar{x}$.
3. $\partial \ell / \partial \sigma^2 = -\frac{n}{2\sigma^2} + \frac{1}{2\sigma^4}\sum_{i=1}^n (x_i - \mu)^2 = 0$.
4. Solve: $\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (x_i - \bar{x})^2$.

**EVALUATE**: MLE uses divisor $n$, so it is biased: $E[\hat{\sigma}^2] = \frac{n-1}{n}\sigma^2$. The unbiased sample variance uses $n-1$, but that is not the MLE.

P: Find the MLE of $\lambda$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} \mathrm{Exp}(\lambda)$, where $f(x; \lambda) = \lambda e^{-\lambda x}$ for $x \geq 0$.

S:
**IDENTIFY**: One-parameter continuous MLE, $\lambda > 0$.

**PLAN**: Standard log-likelihood + calculus.

**EXECUTE**:
1. $L(\lambda) = \lambda^n e^{-\lambda \sum x_i}$.
2. $\ell(\lambda) = n\log\lambda - \lambda \sum_{i=1}^n x_i$.
3. $\ell'(\lambda) = n/\lambda - \sum x_i = 0 \Rightarrow \hat{\lambda} = n / \sum x_i = 1/\bar{x}$.

**EVALUATE**: $\ell''(\lambda) = -n/\lambda^2 < 0$, maximum confirmed. Note: by invariance, the MLE of the mean $1/\lambda$ is $\bar{x}$.

P: Find the MLE of $\lambda$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} \mathrm{Poisson}(\lambda)$, where $P(X = k) = e^{-\lambda}\lambda^k/k!$.

S:
**IDENTIFY**: One-parameter discrete MLE, $\lambda > 0$.

**PLAN**: Standard recipe.

**EXECUTE**:
1. $L(\lambda) = \prod_{i=1}^n \frac{e^{-\lambda}\lambda^{x_i}}{x_i!} = e^{-n\lambda}\lambda^{\sum x_i}\big/\prod x_i!$.
2. $\ell(\lambda) = -n\lambda + \left(\sum x_i\right)\log\lambda - \sum \log(x_i!)$.
3. $\ell'(\lambda) = -n + \frac{\sum x_i}{\lambda} = 0 \Rightarrow \hat{\lambda} = \bar{x}$.

**EVALUATE**: $\ell''(\lambda) = -\sum x_i / \lambda^2 < 0$ (assuming $\sum x_i > 0$), maximum confirmed.

P: Find the MLE of $\theta$ for $X_1, \ldots, X_n \stackrel{\mathrm{iid}}{\sim} \mathrm{Uniform}(0, \theta)$.

S:
**IDENTIFY**: The support of the density depends on $\theta$, so calculus fails — this is a boundary MLE.

**PLAN**: Write the likelihood carefully, noting where it is zero.

**EXECUTE**:
1. Density: $f(x; \theta) = 1/\theta$ for $0 \leq x \leq \theta$, and $0$ otherwise.
2. Likelihood: $L(\theta) = \theta^{-n}$ if $\theta \geq \max_i x_i$, and $L(\theta) = 0$ otherwise (because any $x_i > \theta$ makes $f(x_i; \theta) = 0$).
3. On the feasible region $\theta \geq x_{(n)}$, $L(\theta) = \theta^{-n}$ is strictly decreasing in $\theta$.
4. So $L$ is maximized at the smallest feasible $\theta$, namely $\hat{\theta}_{\mathrm{MLE}} = x_{(n)} = \max_i x_i$.

**EVALUATE**: Calculus on $\log L = -n\log\theta$ gives $\ell'(\theta) = -n/\theta \neq 0$ — no interior critical point. The MLE is on the boundary of the feasible set. Note this also respects $\theta \geq x_{(n)}$, unlike the MoM estimator $2\bar{x}$.

Q: Why does the Uniform$(0, \theta)$ MLE differ fundamentally from the Bernoulli or Normal MLE?
A: Because the support $[0, \theta]$ depends on the parameter. The likelihood is discontinuous in $\theta$ at $\theta = x_{(n)}$, so the maximum is at that boundary rather than at an interior critical point found by $\ell'(\theta) = 0$.

## 3.11 When MLE Doesn't Exist on Boundary

Q: Why did the calculus recipe (set derivative to zero) fail for $\mathrm{Uniform}(0, \theta)$?
A: The log-likelihood $\ell(\theta) = -n \log\theta$ is strictly decreasing on the feasible region $\theta \geq x_{(n)}$ — its derivative $-n/\theta$ is never zero. The maximum sits at the left endpoint of the feasible region, which calculus cannot detect.

Q: What general lesson does the uniform example teach about finding MLEs?
A: Always check whether the support depends on the parameter. If it does, the likelihood may be maximized at a boundary of the parameter space, and you must handle that boundary explicitly rather than relying on $\ell'(\theta) = 0$.

C: When the support of $f(x; \theta)$ depends on $\theta$, the MLE may lie on the [boundary] of the feasible set rather than at an interior critical point.

Q: For $\mathrm{Uniform}(0, \theta)$, why is the MLE $X_{(n)}$ rather than any $\theta < X_{(n)}$?
A: If $\theta < X_{(n)}$, then at least one observation lies outside $[0, \theta]$, so $f(X_{(n)}; \theta) = 0$ and the likelihood is zero. The smallest feasible value is $X_{(n)}$ itself, where the likelihood $\theta^{-n}$ is largest.

Q: In general, what two places should you check for the maximum of $\ell(\theta)$?
A: (1) Interior critical points where $\ell'(\theta) = 0$ and $\ell''(\theta) < 0$, and (2) the boundary of the parameter space. Whichever yields the largest $\ell$ is the MLE.
