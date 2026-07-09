+++
order = 9
subject = "Mathematics"
tags = ["math", "statistics", "chi-square", "goodness-of-fit", "independence", "contingency-table"]
+++

# Statistics — Chi-Square Tests

## 9.1 Why Chi-Square Tests?

Q: Why do we need a new family of tests for categorical data?
A: The $z$- and $t$-tests developed earlier apply to means and proportions of numeric data. When observations are counts falling into discrete categories (color, blood type, survey response), the relevant question is whether the pattern of counts matches a hypothesized distribution — a question answered by chi-square tests.

C: [Categorical data] are observations that fall into discrete, unordered (or ordered but non-numeric) categories rather than taking numeric values on a continuous scale.

C: A [goodness-of-fit test] asks whether an observed distribution of categorical counts matches a specified theoretical distribution.

Q: What is the central idea behind every chi-square test?
A: Compare the counts actually observed in each category to the counts we would expect under a null hypothesis, and measure how far the observed counts deviate from the expected counts. Large deviations are evidence against the null.

Q: Why are chi-square tests always one-sided (right-tailed) on the $\chi^2$ distribution even when the underlying hypothesis is two-sided?
A: The test statistic squares the deviations $(O_i - E_i)$, so both positive and negative discrepancies produce large values of $\chi^2$. Evidence against the null always sits in the right tail.

## 9.2 Chi-Square Goodness-of-Fit Test

C: In a [chi-square goodness-of-fit test], the null hypothesis specifies a probability $p_i$ for each of $k$ categories, and the alternative is that at least one true probability differs from the specified value.

C: In a goodness-of-fit test, the [observed count] $O_i$ is the number of sample observations that fell into category $i$.

C: In a goodness-of-fit test with total sample size $n$ and hypothesized probability $p_i$ for category $i$, the [expected count] is $E_i = n p_i$, where $n$ is the sample size and $p_i$ is the probability of category $i$ under $H_0$.

Q: How do you state the hypotheses for a goodness-of-fit test with $k$ categories?
A: $H_0$: $p_1 = p_1^0, p_2 = p_2^0, \ldots, p_k = p_k^0$ (the true category probabilities match the specified values). $H_a$: at least one $p_i$ differs from its specified value $p_i^0$.

Q: What assumptions underlie the goodness-of-fit test?
A: (1) Observations are independent and form a simple random sample. (2) Each observation falls into exactly one of $k$ mutually exclusive categories. (3) Expected counts $E_i$ are large enough (commonly $E_i \geq 5$) so the $\chi^2$ approximation is valid.

## 9.3 The Chi-Square Test Statistic

Q: Before seeing the formula, predict: how should a test statistic combine the deviations $O_i - E_i$ into a single number?
A: It must (a) treat positive and negative deviations symmetrically (square them), and (b) weight a given absolute deviation more heavily when the expected count is small (a miss of 5 out of 10 expected is more striking than 5 out of 1000). Dividing the squared deviation by $E_i$ accomplishes both.

C: The [chi-square test statistic] is $\chi^2 = \sum_{i=1}^{k} \frac{(O_i - E_i)^2}{E_i}$, where $O_i$ is the observed count in category $i$, $E_i$ is the expected count under $H_0$, and $k$ is the number of categories.

Q: Why is each squared deviation divided by $E_i$ rather than by $\sqrt{E_i}$ or nothing at all?
A: Under the null, a count $O_i$ is approximately Poisson with mean $E_i$ and variance $E_i$, so $(O_i - E_i)/\sqrt{E_i}$ is approximately standard normal. Squaring and summing gives a sum of squared standard normals — which follows a chi-square distribution. Dividing by $E_i$ is the variance scaling that makes this distributional match work.

Q: What does $\chi^2 = 0$ mean?
A: Every observed count equals its expected count exactly — a perfect fit to the null hypothesis. Any positive value of $\chi^2$ indicates some discrepancy; larger values indicate stronger evidence against $H_0$.

C: In a chi-square test, we reject $H_0$ when $\chi^2$ is [large] (in the right tail of the reference distribution), because large values correspond to big discrepancies between observed and expected counts.

## 9.4 Degrees of Freedom

Q: Intuitively, why does a chi-square test have fewer degrees of freedom than categories?
A: The $k$ observed counts must sum to the sample size $n$, which imposes one linear constraint. Any additional parameters estimated from the data to compute the $E_i$ impose further constraints. Each constraint removes one degree of freedom.

C: For a goodness-of-fit test with $k$ categories and a fully specified null distribution, the degrees of freedom are [$k - 1$], because the counts must sum to $n$.

C: If $p$ parameters of the null distribution are [estimated from the data] before computing expected counts, the degrees of freedom become $k - 1 - p$, where $k$ is the number of categories and $p$ is the number of estimated parameters.

Q: If you test whether data follow a Poisson distribution (with unknown mean) using $k = 6$ grouped categories, how many degrees of freedom does the chi-square statistic have?
A: $k - 1 - p = 6 - 1 - 1 = 4$. One degree of freedom is lost because counts sum to $n$, and one more because the Poisson mean $\lambda$ was estimated from the sample.

Q: Why does estimating parameters from the same data used in the test cost degrees of freedom?
A: Estimating a parameter forces the expected counts to fit the data more closely than they would if the parameter had been pre-specified. This artificially shrinks $\chi^2$, so we must compare against a distribution with fewer degrees of freedom to keep the test honest.

## 9.5 Expected Counts and the $E_i \geq 5$ Rule

Q: Why does the chi-square test require reasonably large expected counts?
A: The chi-square distribution is only an approximation to the true sampling distribution of $\sum (O_i - E_i)^2 / E_i$. The approximation relies on each $(O_i - E_i)/\sqrt{E_i}$ being roughly normal, which fails when $E_i$ is very small — counts are discrete and skewed when their mean is near zero.

C: A common rule of thumb is that the chi-square approximation is reliable when every expected count satisfies [$E_i \geq 5$].

Q: What can you do when some expected counts are below 5?
A: Combine adjacent or similar categories so every pooled $E_i \geq 5$, collect a larger sample, or switch to an exact method such as Fisher's exact test for small $2 \times 2$ tables.

Q: If one category has $E_i = 2$ and the rest have $E_i \geq 10$, is the test valid?
A: Not reliably. Even a single small expected count can inflate the variance of $\chi^2$ away from the theoretical chi-square distribution, distorting the $p$-value. Pool that category with a neighbor or reconsider the design.

## 9.6 Chi-Square Test of Independence

Q: What does a chi-square test of independence ask?
A: Given a single sample cross-classified by two categorical variables, are the two variables statistically independent in the underlying population, or are they associated?

C: A [two-way contingency table] (or cross-tabulation) displays counts for every combination of categories of two categorical variables, with one variable's levels as rows and the other's as columns.

C: In an $r \times c$ contingency table, the [row total] $R_i$ is the sum of counts in row $i$ and the [column total] $C_j$ is the sum of counts in column $j$; the grand total is $n = \sum_i R_i = \sum_j C_j$.

Q: State the hypotheses for a chi-square test of independence on an $r \times c$ table.
A: $H_0$: the row variable and column variable are independent (joint probabilities factor as products of marginals). $H_a$: the two variables are not independent — there is some association between them.

Q: Why do we sample once and cross-classify, rather than sampling separately within each row?
A: In the independence framing, a single random sample of size $n$ is drawn from a population and each subject is classified on both variables. The row and column totals are both random. This contrasts with the homogeneity design, where row totals are fixed by design.

## 9.7 Expected Counts in a Contingency Table

Q: Under the independence null, how should we estimate the expected count in cell $(i, j)$?
A: Under independence, $P(\text{row } i \text{ and column } j) = P(\text{row } i) \cdot P(\text{column } j)$. Estimate the marginal probabilities by $R_i / n$ and $C_j / n$, so the estimated joint probability is $R_i C_j / n^2$, and the expected count is $n$ times this: $E_{ij} = R_i C_j / n$.

C: In a chi-square test on a contingency table, the [expected count] for cell $(i, j)$ is $E_{ij} = \dfrac{R_i C_j}{n}$, where $R_i$ is the total of row $i$, $C_j$ is the total of column $j$, and $n$ is the grand total.

C: The chi-square statistic for a contingency table is $\chi^2 = [\sum_{i=1}^{r} \sum_{j=1}^{c} \dfrac{(O_{ij} - E_{ij})^2}{E_{ij}}]$, where $O_{ij}$ is the observed count and $E_{ij}$ is the expected count in cell $(i, j)$.

Q: A contingency table has $R_2 = 80$, $C_3 = 50$, and $n = 200$. What is $E_{23}$?
A: $E_{23} = R_2 C_3 / n = (80)(50)/200 = 20$.

## 9.8 Degrees of Freedom for an $r \times c$ Table

Q: Why does an $r \times c$ contingency table have $(r-1)(c-1)$ degrees of freedom?
A: The expected counts $E_{ij}$ are built from the $r$ row totals and $c$ column totals, but these marginals carry $(r-1) + (c-1) + 1$ pieces of information (after accounting for the grand-total constraint). There are $rc$ cells, so degrees of freedom are $rc - [(r-1) + (c-1) + 1] = (r-1)(c-1)$.

C: For a chi-square test on an $r \times c$ contingency table, the degrees of freedom are [$(r-1)(c-1)$], where $r$ is the number of rows and $c$ is the number of columns.

Q: How many degrees of freedom does a $2 \times 2$ contingency table have?
A: $(2-1)(2-1) = 1$ degree of freedom.

Q: How many degrees of freedom does a $3 \times 4$ contingency table have?
A: $(3-1)(4-1) = 2 \cdot 3 = 6$ degrees of freedom.

## 9.9 Chi-Square Test of Homogeneity

Q: What is the chi-square test of homogeneity?
A: It compares the distribution of a single categorical variable across two or more populations, asking whether the population-level distributions are identical (homogeneous) or differ.

Q: How does the homogeneity design differ from the independence design?
A: In homogeneity, separate random samples are drawn from each population and one row total per population is fixed by the researcher. In independence, a single sample is drawn and both margins are random. The data and computations look identical, but the sampling scheme differs.

C: The chi-square tests of [independence] and [homogeneity] use the same test statistic, the same expected-count formula $E_{ij} = R_i C_j / n$, and the same $(r-1)(c-1)$ degrees of freedom; only the sampling interpretation differs.

Q: Given that independence and homogeneity use identical arithmetic, why bother distinguishing them?
A: The hypotheses and scientific conclusions differ. Independence addresses association within one population; homogeneity addresses whether several populations share the same distribution. Reporting the correct framing is essential for interpreting the result.

## 9.10 Relationship to the Two-Proportion $z$-Test

Q: For a $2 \times 2$ contingency table, how does the chi-square test of independence relate to the two-proportion $z$-test?
A: They are equivalent. The chi-square statistic equals the square of the two-proportion $z$-statistic: $\chi^2 = z^2$. The two-sided $z$-test and the one-sided (right-tailed) $\chi^2$ test give identical $p$-values.

C: For a $2 \times 2$ contingency table, the chi-square statistic and the two-proportion $z$-statistic satisfy [$\chi^2 = z^2$], and the two tests produce identical $p$-values.

Q: Why does $\chi^2 = z^2$ hold only for $2 \times 2$ tables and not for larger ones?
A: A $z$-test compares two proportions along a single dimension of variation, which corresponds to the 1 degree of freedom of a $2 \times 2$ chi-square. Larger tables have multiple independent dimensions of variation $((r-1)(c-1) > 1)$, which no single $z$-statistic can capture.

Q: If the two-proportion $z$-test gives $z = 2.1$, what is the corresponding $\chi^2$ value on the $2 \times 2$ table?
A: $\chi^2 = z^2 = (2.1)^2 = 4.41$, with 1 degree of freedom.

## 9.11 Continuity Correction (Yates)

Q: Why might we apply a continuity correction to a chi-square statistic?
A: The observed counts are discrete integers, but the chi-square distribution is continuous. For $2 \times 2$ tables with small expected counts, this mismatch makes the uncorrected $\chi^2$ systematically too large, inflating Type I error. A continuity correction shrinks the statistic to better align the discrete and continuous distributions.

C: [Yates' continuity correction] for a $2 \times 2$ table subtracts $0.5$ from each absolute deviation before squaring: $\chi^2_{\text{Yates}} = \sum \dfrac{(|O_{ij} - E_{ij}| - 0.5)^2}{E_{ij}}$.

Q: When is Yates' correction most useful, and when is it unnecessary?
A: Most useful for $2 \times 2$ tables with small expected counts, where the uncorrected chi-square is noticeably liberal. Unnecessary — and arguably overly conservative — for large samples, for tables with $E_{ij}$ comfortably above 5, or for tables larger than $2 \times 2$.

Q: Does Yates' correction make a test more conservative or less conservative?
A: More conservative. By shrinking each deviation, it reduces $\chi^2$ and raises the $p$-value, so the test rejects $H_0$ less often at any given significance level.

## 9.12 Fisher's Exact Test

Q: Why do we need an alternative to chi-square for very small counts?
A: The chi-square distribution is only an approximation. When expected counts are below about 5, the approximation becomes unreliable — even with Yates' correction — so a method that computes an exact $p$-value from the discrete distribution of the table is preferable.

C: [Fisher's exact test] computes an exact $p$-value for a $2 \times 2$ contingency table by summing hypergeometric probabilities of tables at least as extreme as the observed one, conditional on the fixed row and column totals.

Q: When should you prefer Fisher's exact test over a chi-square test?
A: When the table is small (typically $2 \times 2$) and one or more expected counts fall below 5, making the chi-square approximation untrustworthy. Fisher's test is valid for any sample size because it uses the exact discrete distribution.

Q: What is a practical drawback of Fisher's exact test?
A: It conditions on both margins being fixed (often unrealistic), and for larger tables or larger sample sizes it becomes computationally expensive. Most software extends it to $r \times c$ tables but it remains slower than the chi-square approximation.

## 9.13 Worked Problem: $2 \times 2$ Test of Independence

P: A random sample of 200 adults is classified by smoking status (smoker, non-smoker) and whether they developed a chronic cough within one year. The observed counts are:

| | Cough | No cough | Total |
|---|---|---|---|
| Smoker | 30 | 40 | 70 |
| Non-smoker | 20 | 110 | 130 |
| Total | 50 | 150 | 200 |

Test at $\alpha = 0.05$ whether smoking status and chronic cough are independent.

S:
**IDENTIFY**: Chi-square test of independence on a $2 \times 2$ contingency table. The question is whether the row variable (smoking) and the column variable (cough) are associated in the population.

**PLAN**:
- State $H_0$: smoking and cough are independent; $H_a$: smoking and cough are not independent.
- Compute expected counts using $E_{ij} = R_i C_j / n$.
- Check that every $E_{ij} \geq 5$.
- Compute $\chi^2 = \sum (O_{ij} - E_{ij})^2 / E_{ij}$.
- Compare to the chi-square distribution with $(r-1)(c-1) = 1$ degree of freedom at $\alpha = 0.05$ (critical value $\chi^2_{0.05, 1} = 3.84$).

**EXECUTE**:
1. Marginals: $R_1 = 70, R_2 = 130, C_1 = 50, C_2 = 150, n = 200$.
2. Expected counts:
   - $E_{11} = (70)(50)/200 = 17.5$
   - $E_{12} = (70)(150)/200 = 52.5$
   - $E_{21} = (130)(50)/200 = 32.5$
   - $E_{22} = (130)(150)/200 = 97.5$
3. All expected counts exceed 5, so the chi-square approximation is valid.
4. Contributions:
   - Cell $(1,1)$: $(30 - 17.5)^2 / 17.5 = 156.25/17.5 \approx 8.929$
   - Cell $(1,2)$: $(40 - 52.5)^2 / 52.5 = 156.25/52.5 \approx 2.976$
   - Cell $(2,1)$: $(20 - 32.5)^2 / 32.5 = 156.25/32.5 \approx 4.808$
   - Cell $(2,2)$: $(110 - 97.5)^2 / 97.5 = 156.25/97.5 \approx 1.603$
5. Sum: $\chi^2 \approx 8.929 + 2.976 + 4.808 + 1.603 \approx 18.32$.
6. Degrees of freedom: $(2-1)(2-1) = 1$. Critical value at $\alpha = 0.05$: $3.84$.

**EVALUATE**:
- $\chi^2 \approx 18.32 \gg 3.84$, so we reject $H_0$ at the $5\%$ level.
- There is strong evidence of an association between smoking status and chronic cough.
- Sanity check: smokers had $30/70 \approx 43\%$ cough rate vs non-smokers $20/130 \approx 15\%$ — a large observed gap, consistent with a large $\chi^2$.
- The equivalent two-proportion $z$-statistic satisfies $z^2 = \chi^2$, so $|z| \approx \sqrt{18.32} \approx 4.28$, which would also reject at $\alpha = 0.05$ two-sided.
- All expected counts exceed 5, so Yates' correction is not required; Fisher's exact test is also unnecessary here.
