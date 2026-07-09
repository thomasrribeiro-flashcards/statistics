+++
order = 1
subject = "Math"
tags = ["math", "statistics", "descriptive", "mean", "variance", "correlation", "eda"]
+++

# Statistics — Descriptive Statistics and EDA

## 1.1 Why Descriptive Statistics?

Q: Why do we start a statistics course with descriptive statistics rather than jumping straight to inference?
A: Raw data is typically too large and noisy to understand by staring at it. Descriptive statistics compresses a dataset into a handful of summaries (center, spread, shape) and pictures (histograms, boxplots) that reveal what the data actually looks like. Without this step, inferential procedures risk being misapplied — you cannot check assumptions you have never visualized.

Q: Why is exploratory data analysis (EDA) considered a prerequisite to formal inference?
A: EDA exposes issues — outliers, skewness, missing values, wrong scales — that would otherwise silently violate the assumptions of inferential tests. A $t$-test on badly skewed data gives a number, but that number is meaningless. Exploring first lets you choose an appropriate model and catch data problems early.

C: [Descriptive statistics] is the branch of statistics concerned with summarizing and visualizing data, as opposed to drawing conclusions about a larger population.

C: [Exploratory data analysis] (EDA) is the process of examining data through summaries and plots before formal modeling, to uncover patterns, anomalies, and the need for transformations.

Q: Before running a hypothesis test, predict what could go wrong if you skip EDA on a skewed dataset.
A: A test assuming normality (like a standard $t$-test) may give misleading $p$-values because the sample mean is pulled by extreme values, and the reference distribution does not match the data. You might also miss outliers that drive the result entirely.

## 1.2 Population vs Sample; Parameter vs Statistic

Q: Why is the distinction between a population and a sample foundational to statistics?
A: Nearly every interesting question concerns a population (all voters, all patients, all manufactured bolts) that is too large to measure completely. We observe only a sample and use it to make statements about the population. Every inferential claim depends on keeping these two levels straight.

C: A [population] is the complete set of all units (people, objects, measurements) about which we want to draw conclusions.

C: A [sample] is a subset of the population that is actually observed or measured.

C: A [parameter] is a numerical summary of a population (e.g., the population mean $\mu$), typically unknown.

C: A [statistic] is a numerical summary computed from a sample (e.g., the sample mean $\bar{x}$), which is observable.

Q: Why is the population mean $\mu$ usually unknown while the sample mean $\bar{x}$ is known?
A: Computing $\mu$ would require measuring every unit in the population, which is almost always impossible or prohibitively expensive. The sample mean $\bar{x}$ is computed from the finite sample we actually collected, so it is always directly calculable.

C: Greek letters (e.g., $\mu$, $\sigma$) typically denote [parameters], while Latin letters (e.g., $\bar{x}$, $s$) denote statistics.

Q: Why do we use sample statistics to estimate population parameters rather than the other way around?
A: Parameters describe the target of inference, but they are not observable. Statistics are observable and, if the sample is drawn well, systematically close to the parameters. The whole enterprise of inference is to quantify how close.

## 1.3 Types of Data

Q: Why does the type of data (categorical vs numerical) matter before computing any summary?
A: The statistics that make sense depend on what operations the data supports. You can average heights but not eye colors; you can rank test grades but not meaningfully add them as percentages of a total. Applying the wrong summary produces numbers that look precise but are meaningless.

C: [Categorical data] takes values from a finite set of labels with no inherent numerical meaning (e.g., blood type, country).

C: [Ordinal data] is categorical data whose categories have a natural order but no meaningful distance between them (e.g., "small, medium, large").

C: [Interval data] is numerical data where differences are meaningful but there is no true zero (e.g., temperature in °C — 0 °C is not "no temperature").

C: [Ratio data] is numerical data with a true zero, so ratios are meaningful (e.g., height, mass, duration — twice as tall is meaningful).

Q: Why can you say "twice as heavy" but not "twice as hot" (in Celsius)?
A: Mass is ratio data with a true zero (0 kg = no mass), so the ratio $2\,\text{kg}/1\,\text{kg} = 2$ is meaningful. Celsius temperature is interval data: 0 °C is just the freezing point of water, not the absence of thermal energy, so $20/10 = 2$ does not correspond to "twice the heat."

Q: Why is ranking ordinal data acceptable but averaging it risky?
A: Ordinal categories preserve order but not spacing: the gap between "small" and "medium" may not equal the gap between "medium" and "large." Averaging treats the gaps as equal, which can distort the summary. Medians and ranks respect only order and are safer.

## 1.4 Measures of Center: Mean, Median, Mode

Q: Why do we need more than one measure of center?
A: A single number must summarize a whole distribution, and no one number captures every feature. The mean reflects the balance point, the median reflects the middle, and the mode reflects the most common value. Different shapes of distribution make different measures informative.

C: The [sample mean] of $n$ values $x_1, \ldots, x_n$ is $\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$, where $x_i$ is the $i$-th observation and $n$ is the sample size.

C: The [median] of a dataset is the middle value when the data is sorted — the value with equal numbers of observations below and above it.

C: For an even number of observations, the median is the [average of the two middle values] after sorting.

C: The [mode] of a dataset is the value (or values) that occur most frequently.

Q: Why is the mean often described as the "balance point" of the data?
A: If you place equal weights at each data value on a number line, the mean is the single point at which the line would balance. Algebraically, $\sum (x_i - \bar{x}) = 0$, so deviations on either side cancel exactly, where $x_i$ is the $i$-th data point and $\bar{x}$ is the sample mean.

Q: When is the mode more useful than the mean or median?
A: For categorical data (where mean and median may not even exist) and for multimodal numerical distributions where two or more peaks carry substantive meaning (e.g., two subpopulations mixed together).

## 1.5 Robustness of Median vs Mean

Q: Why is the median called "robust" while the mean is not?
A: A statistic is robust if extreme values have limited influence on it. The median only cares about rank order, so moving a single extreme value to infinity does not change it. The mean sums all values, so a single extreme value can drag it arbitrarily far.

Q: Predict: in the dataset $\{1, 2, 3, 4, 100\}$, how do the mean and median compare?
A: Median is 3 (the middle value after sorting). Mean is $(1+2+3+4+100)/5 = 22$. The outlier 100 pulls the mean up dramatically while leaving the median untouched.

C: The [breakdown point] of a statistic is the smallest fraction of observations that can be made arbitrarily extreme before the statistic itself becomes arbitrary — the mean has a breakdown point of $0$, and the median has a breakdown point of $50\%$.

Q: Why do we often report the median for income data rather than the mean?
A: Income distributions are strongly right-skewed: a small number of very high earners pull the mean far above where most people live. The median corresponds to the person "in the middle" and better reflects a typical income.

## 1.6 Measures of Spread: Range, IQR, Variance, Standard Deviation

Q: Why is a measure of center incomplete without a measure of spread?
A: Two datasets can share the same mean or median and yet differ dramatically — one tightly clustered, one widely dispersed. Spread quantifies how far observations typically stray from the center, which controls predictability and the precision of estimates.

C: The [range] of a dataset is the difference between the maximum and minimum values: $\text{range} = x_{\max} - x_{\min}$, where $x_{\max}$ and $x_{\min}$ are the largest and smallest observations.

C: The [interquartile range] (IQR) is $\text{IQR} = Q_3 - Q_1$, where $Q_1$ is the 25th percentile and $Q_3$ is the 75th percentile.

C: The [sample variance] $s^2$ measures the average squared deviation from the sample mean.

C: The [sample standard deviation] $s$ is the square root of the sample variance: $s = \sqrt{s^2}$, so $s$ is in the same units as the data.

Q: Why is the standard deviation often preferred over the variance for reporting?
A: Variance has units that are the square of the data's units (e.g., dollars squared), which is not intuitive. Standard deviation shares the data's units, so statements like "incomes are typically within $\$10{,}000$ of the mean" become interpretable.

Q: Why is range a poor measure of spread for large datasets?
A: Range depends only on the two most extreme values, so it is maximally sensitive to outliers and tells you nothing about how densely the rest of the data clusters. It also grows with sample size since adding more observations can only enlarge the extremes.

Q: Why is IQR more robust than the range?
A: IQR throws away the bottom $25\%$ and top $25\%$ of the data before measuring spread, so extreme values in the tails cannot affect it. It reflects the spread of the middle half of the data.

## 1.7 Sample Variance and Why $n-1$

Q: Before seeing the formula, predict: why might dividing by $n$ understate the true variability in a sample?
A: The sample mean $\bar{x}$ is, by construction, closer to the data than the unknown true mean $\mu$ is. Measuring deviations from $\bar{x}$ therefore gives smaller squared distances on average than measuring from $\mu$ would, so dividing by $n$ systematically underestimates the population variance.

C: The [sample variance] is $s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2$, where $x_i$ is the $i$-th observation, $\bar{x}$ is the sample mean, and $n$ is the sample size.

Q: Why do we divide by $n-1$ rather than $n$ in the sample variance formula?
A: Dividing by $n$ gives a biased estimator that systematically underestimates the population variance $\sigma^2$, because deviations are measured from $\bar{x}$ (which is itself fit to the sample) rather than from the true $\mu$. Dividing by $n-1$ corrects the bias so that $\mathbb{E}[s^2] = \sigma^2$.

C: The divisor $n-1$ in $s^2$ reflects the [degrees of freedom]: once $\bar{x}$ is computed, only $n-1$ of the deviations $(x_i - \bar{x})$ can vary freely, because they must sum to zero.

Q: Why does $\sum_{i=1}^{n}(x_i - \bar{x}) = 0$ reduce the degrees of freedom by one?
A: This constraint means the $n$ deviations are not independent — once you know $n-1$ of them, the last one is forced. So the effective number of independent squared deviations is $n-1$, which is the right divisor for an unbiased average.

C: An estimator is called [unbiased] if its expected value equals the parameter it is estimating. Using $n-1$ in $s^2$ makes it an unbiased estimator of $\sigma^2$.

Q: In the formula $s^2 = \frac{1}{n-1}\sum (x_i - \bar{x})^2$, why are deviations squared rather than taken in absolute value?
A: Squaring is smooth and algebraically tractable (it has a continuous derivative), leads to closed-form estimators, and matches the geometry of Euclidean distance. Absolute deviations give a valid alternative measure but produce less tractable theory.

## 1.8 Quantiles, Percentiles, Five-Number Summary

Q: Why are quantiles a useful generalization of the median?
A: The median cuts the data in half, but sometimes we want finer locations — "the value below which $10\%$ of the data falls" or "the value below which $90\%$ falls." Quantiles provide any such cutoff, giving a complete picture of how the data is distributed rather than just its center.

C: The [$p$-th quantile] of a dataset is the value below which a fraction $p$ of the data falls (with $0 \le p \le 1$).

C: A [percentile] is a quantile expressed as a percentage: the 25th percentile equals the $0.25$ quantile.

C: The first quartile $Q_1$ is the [25th percentile], the second quartile $Q_2$ is the median (50th percentile), and the third quartile $Q_3$ is the 75th percentile.

C: The [five-number summary] of a dataset consists of the minimum, $Q_1$, median, $Q_3$, and maximum.

Q: Why is the five-number summary often preferred over just reporting the mean and standard deviation?
A: The five-number summary makes no assumption about distribution shape: it describes center, spread, and skewness through actual data points. Mean and standard deviation assume roughly symmetric, well-behaved data and can badly mislead for skewed or outlier-heavy distributions.

## 1.9 Histograms and Density Plots

Q: Why is a histogram usually the first plot to make when exploring a numerical variable?
A: A histogram shows the shape of the entire distribution — modes, skewness, gaps, and outliers — in a single image. Summary statistics compress the distribution to a few numbers, but a histogram preserves the features that dictate which summaries and models are appropriate.

C: A [histogram] groups numerical data into adjacent intervals called bins, and draws a bar over each bin whose height represents the count (or density) of observations in that bin.

Q: Why does the choice of bin width matter for a histogram?
A: Too-wide bins oversmooth, hiding real structure (bimodality, gaps). Too-narrow bins are noisy, showing spurious spikes from sampling variation. Bin width is a bias-variance trade-off, and there is no single right choice — always try several.

C: A [density plot] (or kernel density estimate) replaces the jagged bars of a histogram with a smooth curve approximating the underlying distribution.

Q: Why might you use a density plot instead of a histogram?
A: Density plots avoid the binning artifacts of histograms and make it easier to compare the shapes of multiple distributions overlaid on the same axes. The trade-off is that they introduce their own smoothing parameter (bandwidth) and can hide sharp features.

## 1.10 Boxplots and Outlier Detection

Q: Why was the boxplot invented, given that we already have histograms?
A: Boxplots show the five-number summary compactly and make it easy to compare many distributions side by side — something histograms do poorly. They also flag outliers explicitly using a simple rule, which histograms do not.

C: A [boxplot] draws a box from $Q_1$ to $Q_3$ with a line at the median; "whiskers" extend to the most extreme non-outlier values, and outliers are plotted as individual points.

C: A common rule flags a data point as an [outlier] if it lies below $Q_1 - 1.5 \cdot \text{IQR}$ or above $Q_3 + 1.5 \cdot \text{IQR}$, where IQR is the interquartile range.

Q: Why is the $1.5 \cdot \text{IQR}$ outlier rule based on the IQR rather than the standard deviation?
A: IQR is robust: a single extreme value cannot inflate it, whereas one outlier can inflate the standard deviation and hide additional outliers. Using a robust yardstick lets you detect outliers without having outliers sabotage the detection.

Q: When comparing three groups, why is a side-by-side boxplot often more informative than three separate histograms?
A: Boxplots align center (median) and spread (IQR) on the same axis, making differences in location, spread, and skewness immediately visible. Three separate histograms require the eye to compare shapes across panels, which is harder.

Q: Does "outlier" always mean "bad data"?
A: No. An outlier is simply an observation far from the bulk of the data. It could be a data-entry error (remove it), a true but rare event (keep it and investigate), or a signal that the model is wrong (reconsider the model). Flagging prompts investigation, not automatic deletion.

## 1.11 Scatterplots and Sample Correlation

Q: Why is a scatterplot essential when exploring two numerical variables?
A: A scatterplot shows the joint distribution — whether the variables move together, the shape of any relationship (linear, curved, none), and which observations are unusual in two dimensions. No pair of univariate summaries can reveal these features.

C: A [scatterplot] plots pairs $(x_i, y_i)$ as points in a two-dimensional plane, where $x_i$ and $y_i$ are the $i$-th observations of two variables.

C: The [sample correlation coefficient] $r$ measures the strength and direction of the linear relationship between two numerical variables, with $-1 \le r \le 1$.

C: $r = [\frac{1}{n-1} \sum_{i=1}^{n} \frac{(x_i - \bar{x})}{s_x} \cdot \frac{(y_i - \bar{y})}{s_y}]$, where $x_i, y_i$ are paired observations, $\bar{x}, \bar{y}$ are the sample means, $s_x, s_y$ are the sample standard deviations, and $n$ is the sample size.

Q: Why does dividing by $s_x$ and $s_y$ make $r$ unit-free?
A: The terms $(x_i - \bar{x})/s_x$ and $(y_i - \bar{y})/s_y$ are standardized — dimensionless $z$-scores. Their product, and hence $r$, has no units and is invariant under changes of scale (e.g., converting inches to centimeters does not change $r$).

Q: Why does $r$ only measure linear association?
A: The formula is built from products of deviations from the mean, which quantifies whether above-average $x$ tends to accompany above-average $y$ in a straight-line sense. A strong curved relationship (like $y = x^2$ for $x$ near zero) can yield $r \approx 0$ because the association is not linear.

Q: What does $r = 0$ mean, and what does it not mean?
A: It means no linear association between $x$ and $y$. It does NOT mean the variables are unrelated — they may be strongly related in a nonlinear way. Always look at a scatterplot before trusting $r$ alone.

Q: Why does "correlation does not imply causation"?
A: Correlation is a statistical summary of co-variation in observed data. Two variables can covary because one causes the other, because a third variable causes both (confounding), because of selection effects, or by pure chance. Distinguishing these requires experimental or causal reasoning beyond what $r$ can provide.

## 1.12 Shape Descriptors: Skewness and Kurtosis

Q: Why do we need shape descriptors beyond center and spread?
A: Two distributions with identical means and standard deviations can look very different: one symmetric and bell-shaped, the other long-tailed or lopsided. Skewness and kurtosis quantify asymmetry and tail-weight, pinning down features that affect which models and inference procedures are appropriate.

C: [Skewness] measures the asymmetry of a distribution: positive skew means a long right tail, negative skew means a long left tail, and zero skew means symmetry.

Q: Why does a right-skewed distribution typically have $\text{mean} > \text{median}$?
A: A long right tail contains extreme large values that inflate the mean more than they shift the median (which only tracks the middle rank). So the mean is pulled toward the tail while the median stays anchored at the center.

Q: Predict: for a left-skewed distribution, how should the mean and median compare?
A: The mean should be less than the median. The long left tail pulls the mean toward smaller values while the median, rank-based, is largely unaffected.

C: [Kurtosis] measures the "tail-weight" of a distribution: high kurtosis indicates heavy tails and more extreme outliers; low kurtosis indicates light tails.

Q: Why does high kurtosis matter in practice?
A: High kurtosis means extreme events are more common than a normal distribution would predict. This is critical in finance, insurance, and engineering, where underestimating tail risk can be catastrophic. Tests that assume normality will understate the probability of extreme outcomes.

C: A distribution with the same kurtosis as the normal distribution is called [mesokurtic]; heavier-tailed is leptokurtic, and lighter-tailed is platykurtic.

## 1.13 Worked Problem: Summarizing a Small Dataset

P: Compute the five-number summary, mean, sample variance, and sample standard deviation for the dataset $\{2, 4, 4, 6, 8, 10, 12\}$, and comment on whether the mean or median is a better measure of center.

S:
**IDENTIFY**: Univariate descriptive statistics problem. Goal: produce center, spread, and five-number summary from a sorted list of $n = 7$ values.

**PLAN**:
- Sort (already sorted).
- Compute mean $\bar{x} = \frac{1}{n}\sum x_i$.
- Compute deviations $(x_i - \bar{x})$, square them, sum, divide by $n - 1$ for $s^2$.
- Take $\sqrt{s^2}$ for $s$.
- Read off min, median, max directly; locate $Q_1$ and $Q_3$ as medians of lower and upper halves.
- Compare mean and median in light of the distribution's symmetry.

**EXECUTE**:
1. Sorted data: $2, 4, 4, 6, 8, 10, 12$; $n = 7$.
2. Mean: $\bar{x} = (2 + 4 + 4 + 6 + 8 + 10 + 12)/7 = 46/7 \approx 6.571$.
3. Deviations $(x_i - \bar{x})$: $-4.571, -2.571, -2.571, -0.571, 1.429, 3.429, 5.429$.
4. Squared deviations: $20.898, 6.612, 6.612, 0.327, 2.041, 11.755, 29.469$; sum $\approx 77.714$.
5. Sample variance: $s^2 = 77.714 / (7 - 1) \approx 12.952$.
6. Sample standard deviation: $s \approx \sqrt{12.952} \approx 3.599$.
7. Five-number summary: min $= 2$; median (middle of 7) $= 6$; lower half $\{2, 4, 4\}$ so $Q_1 = 4$; upper half $\{8, 10, 12\}$ so $Q_3 = 10$; max $= 12$.

**EVALUATE**:
- Five-number summary: $(2, 4, 6, 10, 12)$.
- Mean $\approx 6.57$ vs median $= 6$: close, so the distribution is nearly symmetric.
- $s \approx 3.60$ has the same units as the data (reasonable — typical deviation around $3.6$ units from the mean).
- IQR $= Q_3 - Q_1 = 10 - 4 = 6$, and $1.5 \cdot \text{IQR} = 9$; fences at $Q_1 - 9 = -5$ and $Q_3 + 9 = 19$, so no outliers.
- With only mild asymmetry and no outliers, either mean or median is an acceptable measure of center; the mean uses all data and is slightly preferable here.
