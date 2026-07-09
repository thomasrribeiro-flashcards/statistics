+++
order = 11
subject = "Math"
tags = ["math", "statistics", "regression", "least-squares", "residuals", "r-squared"]
+++

# Statistics — Simple Linear Regression

## 11.1 Why Regression?

Q: Why do we study regression at all, given that we already have correlation?
A: Correlation tells us *whether* two quantitative variables move together and how strongly, but it does not give a rule for predicting one from the other. Regression goes further: it produces an explicit equation that models the expected value of a response variable as a function of a predictor, so we can predict new values, estimate effect sizes, and quantify uncertainty.

Q: What is the difference in role between the two variables in simple regression?
A: One variable (the predictor or explanatory variable $X$) is treated as known or controlled, and the other (the response variable $Y$) is modeled as depending on $X$. Regression is not symmetric — regressing $Y$ on $X$ is generally different from regressing $X$ on $Y$.

C: In simple linear regression, $X$ is called the [predictor] (or explanatory/independent) variable and $Y$ is called the response (or dependent) variable.

C: Simple regression models the relationship between [two] quantitative variables, using one predictor to explain the response.

## 11.2 The Simple Linear Model

Q: Before seeing the formula, predict: what is the simplest possible model for how $Y$ depends on $X$?
A: A straight line plus random noise — the mean of $Y$ changes linearly with $X$, and individual $Y$ values scatter around that line because of unmodeled factors and measurement error.

C: The [simple linear regression model] is $Y = \beta_0 + \beta_1 X + \varepsilon$, where $Y$ is the response, $X$ is the predictor, $\beta_0$ is the intercept, $\beta_1$ is the slope, and $\varepsilon$ is a random error term.

C: In the model $Y = \beta_0 + \beta_1 X + \varepsilon$, the parameter $\beta_0$ is the [intercept]: the mean value of $Y$ when $X = 0$.

C: In the model $Y = \beta_0 + \beta_1 X + \varepsilon$, the parameter $\beta_1$ is the [slope]: the change in the mean of $Y$ per one-unit increase in $X$.

Q: What does the error term $\varepsilon$ represent in $Y = \beta_0 + \beta_1 X + \varepsilon$?
A: The random deviation of an individual $Y$ from the mean line $\beta_0 + \beta_1 X$. It captures everything not explained by $X$: unmeasured variables, measurement noise, and intrinsic variability.

C: The regression line $E[Y \mid X] = \beta_0 + \beta_1 X$ is called the [population regression line], because $\beta_0$ and $\beta_1$ are unknown population parameters.

## 11.3 Assumptions of the Simple Linear Model

Q: Why must we state assumptions before estimating $\beta_0$ and $\beta_1$?
A: The methods we use (least squares, t-tests, confidence intervals) are only guaranteed to work — unbiased, efficient, and correctly calibrated — if certain conditions hold. When assumptions fail, estimates can be biased or inferences misleading, so we check assumptions before trusting the output.

C: The [linearity] assumption states that the mean of $Y$ is a linear function of $X$: $E[Y \mid X] = \beta_0 + \beta_1 X$.

C: The [independence] assumption states that the errors $\varepsilon_i$ for different observations are independent of one another.

C: The [equal variance] assumption (homoscedasticity) states that $\mathrm{Var}(\varepsilon_i) = \sigma^2$ is the same for every value of $X$.

C: The [normality] assumption states that the errors $\varepsilon_i$ are normally distributed: $\varepsilon_i \sim N(0, \sigma^2)$.

Q: What is homoscedasticity in plain English?
A: "Equal scatter" — the spread of $Y$ around the regression line is roughly the same for small, medium, and large values of $X$. If the scatter fans out or narrows as $X$ changes, the data are heteroscedastic and the equal-variance assumption fails.

Q: Which regression assumption is most important for producing unbiased estimates of the slope?
A: Linearity (and independence). Violations of equal variance or normality mainly affect standard errors and inference; violations of linearity mean we are fitting the wrong functional form, so the estimated slope no longer targets a meaningful quantity.

## 11.4 Least Squares Estimates

Q: Why do we estimate $\beta_0$ and $\beta_1$ by minimizing the sum of squared residuals rather than, say, the sum of absolute residuals?
A: Squared errors make the loss differentiable, give a unique closed-form solution, and — under the normality assumption — coincide with the maximum likelihood estimates. Squaring also penalizes large deviations more heavily, which matches the Gaussian error model.

C: The [least squares criterion] chooses $\hat\beta_0, \hat\beta_1$ to minimize $\sum_{i=1}^n (Y_i - \beta_0 - \beta_1 X_i)^2$, where $(X_i, Y_i)$ are the $n$ observed data pairs.

C: The sum $S_{XX} = \sum_{i=1}^n (X_i - \bar X)^2$ is the [sum of squared deviations] of $X$ from its mean $\bar X$.

C: The sum $S_{XY} = \sum_{i=1}^n (X_i - \bar X)(Y_i - \bar Y)$ is the [sum of cross-products] of deviations, where $\bar X$ and $\bar Y$ are the sample means of $X$ and $Y$.

C: The least squares estimate of the slope is $\hat\beta_1 = [S_{XY}/S_{XX}]$, where $S_{XY}$ is the sum of cross-products and $S_{XX}$ is the sum of squared deviations of $X$.

C: The least squares estimate of the intercept is $\hat\beta_0 = [\bar Y - \hat\beta_1 \bar X]$, where $\bar X$ and $\bar Y$ are the sample means.

Q: Why does the least-squares regression line always pass through the point $(\bar X, \bar Y)$?
A: Because $\hat\beta_0 = \bar Y - \hat\beta_1 \bar X$ rearranges to $\bar Y = \hat\beta_0 + \hat\beta_1 \bar X$. Plugging $X = \bar X$ into the fitted line gives exactly $\bar Y$, so the line is anchored at the centroid of the data.

Q: How do $\hat\beta_1$ and the sample correlation coefficient $r$ relate?
A: $\hat\beta_1 = r \cdot (s_Y / s_X)$, where $s_X$ and $s_Y$ are the sample standard deviations of $X$ and $Y$. The slope equals the correlation rescaled by the ratio of spreads.

## 11.5 Fitted Values and Residuals

C: The [fitted value] for observation $i$ is $\hat Y_i = \hat\beta_0 + \hat\beta_1 X_i$ — the predicted response from the fitted line at $X = X_i$.

C: The [residual] for observation $i$ is $e_i = Y_i - \hat Y_i$, where $Y_i$ is the observed response and $\hat Y_i$ is the fitted value.

Q: What is the difference between an error $\varepsilon_i$ and a residual $e_i$?
A: The error $\varepsilon_i = Y_i - (\beta_0 + \beta_1 X_i)$ is the unobservable deviation from the true population line. The residual $e_i = Y_i - \hat Y_i$ is its observable estimate, using the fitted line computed from the sample. We can only see residuals; they serve as proxies for the errors when we check assumptions.

Q: Why do the least-squares residuals always sum to zero (when the model includes an intercept)?
A: Setting the derivative of $\sum (Y_i - \beta_0 - \beta_1 X_i)^2$ with respect to $\beta_0$ to zero gives $\sum (Y_i - \hat Y_i) = 0$. Including an intercept forces the residuals to have zero mean by construction.

C: For the least-squares fit with an intercept, $\sum_{i=1}^n e_i = [0]$ and $\sum_{i=1}^n X_i e_i = 0$.

## 11.6 Sums of Squares

C: The [residual sum of squares] is $\mathrm{RSS} = \sum_{i=1}^n (Y_i - \hat Y_i)^2$, where $Y_i$ is observed and $\hat Y_i$ is fitted; it measures variation left unexplained by the regression.

C: The [total sum of squares] is $\mathrm{SST} = \sum_{i=1}^n (Y_i - \bar Y)^2$, where $\bar Y$ is the sample mean; it measures total variation in $Y$.

C: The [regression sum of squares] is $\mathrm{SSR} = \sum_{i=1}^n (\hat Y_i - \bar Y)^2$; it measures the variation in $Y$ explained by the fitted line.

Q: What is the fundamental sum-of-squares identity in simple linear regression?
A: $\mathrm{SST} = \mathrm{SSR} + \mathrm{RSS}$. Total variation in $Y$ decomposes into variation explained by the regression plus variation left in the residuals.

C: The [residual standard error] is $\hat\sigma = \sqrt{\mathrm{RSS}/(n-2)}$, which estimates the error standard deviation $\sigma$; the divisor is $n - 2$ because two parameters ($\beta_0, \beta_1$) are estimated.

Q: Why divide RSS by $n - 2$ rather than $n$ when estimating $\sigma^2$?
A: Each estimated parameter consumes one degree of freedom. With two parameters estimated ($\hat\beta_0$ and $\hat\beta_1$), only $n - 2$ independent pieces of information remain in the residuals, and dividing by $n - 2$ makes $\hat\sigma^2$ an unbiased estimator of $\sigma^2$.

## 11.7 Coefficient of Determination $R^2$

C: The [coefficient of determination] is $R^2 = 1 - \mathrm{RSS}/\mathrm{SST}$, where RSS is residual sum of squares and SST is total sum of squares.

C: $R^2$ equals the [proportion] of the total variation in $Y$ that is explained by the fitted regression on $X$.

Q: What are the possible values of $R^2$ and what do the extremes mean?
A: $R^2 \in [0, 1]$. $R^2 = 1$ means RSS = 0: every point lies exactly on the fitted line. $R^2 = 0$ means SSR = 0: the fitted line is horizontal at $\bar Y$ and $X$ explains none of the variation in $Y$.

Q: Does a high $R^2$ mean the linear model is appropriate?
A: Not necessarily. $R^2$ measures only how much variance the straight line accounts for; a curved relationship can still produce a moderately high $R^2$ even when linearity is clearly violated. Residual plots — not $R^2$ alone — diagnose model fit.

## 11.8 Inference for the Slope

C: The [standard error of $\hat\beta_1$] is $\mathrm{SE}(\hat\beta_1) = \hat\sigma / \sqrt{S_{XX}}$, where $\hat\sigma$ is the residual standard error and $S_{XX} = \sum (X_i - \bar X)^2$.

Q: Why does $\mathrm{SE}(\hat\beta_1)$ get smaller as $S_{XX}$ grows?
A: $S_{XX}$ measures the spread of the predictor. The more widely the $X_i$ are spread out, the more leverage the data give for pinning down the slope, so the same noise level produces a tighter estimate. Clustered $X$ values, by contrast, leave the slope poorly identified.

C: Under the regression assumptions, the test statistic $t = (\hat\beta_1 - \beta_1^0)/\mathrm{SE}(\hat\beta_1)$ follows a $t$-distribution with [$n - 2$] degrees of freedom, where $\beta_1^0$ is the hypothesized slope.

Q: What null hypothesis does the standard $t$-test for the slope usually test, and what does rejecting it mean?
A: $H_0: \beta_1 = 0$ versus $H_1: \beta_1 \neq 0$. Rejecting $H_0$ means there is statistically significant evidence that $X$ has a linear relationship with the mean of $Y$ — the slope is not zero.

## 11.9 Confidence Interval for the Slope

C: A [$(1-\alpha)$ confidence interval] for $\beta_1$ is $\hat\beta_1 \pm t_{\alpha/2,\, n-2} \cdot \mathrm{SE}(\hat\beta_1)$, where $t_{\alpha/2, n-2}$ is the upper-$\alpha/2$ critical value of the $t$-distribution with $n - 2$ degrees of freedom.

Q: How does a confidence interval for $\beta_1$ relate to a two-sided $t$-test of $H_0: \beta_1 = 0$?
A: If the $(1-\alpha)$ confidence interval excludes zero, the two-sided $t$-test rejects $H_0$ at level $\alpha$; if it contains zero, the test fails to reject. The interval and the test use the same $t$-distribution and give consistent conclusions.

Q: What does a confidence interval for the slope actually tell us in plain terms?
A: A range of plausible values for the true change in mean $Y$ per unit change in $X$, at a chosen confidence level. It communicates both the estimated effect size and the uncertainty around it — much more informative than a bare significant/not-significant verdict.

## 11.10 Confidence vs Prediction Intervals

C: A [confidence interval for the mean response] at $X = x_0$ estimates $E[Y \mid X = x_0]$, the average $Y$ over all units with predictor value $x_0$.

C: A [prediction interval for an individual response] at $X = x_0$ estimates a single new $Y$ value for one unit with predictor value $x_0$.

Q: Why is the prediction interval always wider than the confidence interval for the mean at the same $x_0$?
A: The confidence interval captures only uncertainty in estimating the mean line $\beta_0 + \beta_1 x_0$. The prediction interval must additionally capture the intrinsic error $\varepsilon$ of a single observation around that line, adding $\sigma^2$ to the variance and widening the interval.

C: The standard error for the mean response at $x_0$ is $\hat\sigma \sqrt{\tfrac{1}{n} + \tfrac{(x_0 - \bar X)^2}{S_{XX}}}$, while for a new individual response it is $\hat\sigma \sqrt{[1] + \tfrac{1}{n} + \tfrac{(x_0 - \bar X)^2}{S_{XX}}}$; the extra "1" reflects the variance of a single new observation.

Q: Why do both intervals get wider as $x_0$ moves away from $\bar X$?
A: The term $(x_0 - \bar X)^2 / S_{XX}$ in the standard error grows quadratically with distance from $\bar X$. Small errors in the slope are amplified the farther we extrapolate, so uncertainty balloons outside the range of observed $X$ values.

Q: Why is extrapolating a regression line far beyond the observed range of $X$ risky?
A: We have no data to verify the linearity assumption outside the observed range, and the intervals balloon quadratically with distance from $\bar X$. The straight-line relationship may not hold, and even if it does, predictions there are enormously uncertain.

## 11.11 Residual Analysis

Q: Why are residual plots more useful than $R^2$ for assessing a regression fit?
A: $R^2$ is a single number that can hide systematic problems (curvature, unequal variance, outliers) behind an overall-looking good summary. Plots of residuals reveal the shape of the misfit: patterns you can see at a glance tell you *which* assumption is violated and how.

Q: What does a plot of residuals $e_i$ versus fitted values $\hat Y_i$ look like when the model fits well?
A: A random, patternless band of points scattered around zero with roughly constant vertical spread across all fitted values — no curvature, no fan shape, no clusters.

Q: What does a U-shaped or curved pattern in a residuals-vs-fitted plot indicate?
A: A violation of the linearity assumption — the true relationship between $X$ and $Y$ is curved, and a straight line systematically under- or over-predicts in different regions.

Q: What does a fan-shaped (funnel) pattern in a residuals-vs-fitted plot indicate?
A: Heteroscedasticity — the variance of the errors changes with the fitted value (and hence with $X$), violating the equal-variance assumption. A transformation of $Y$ (such as log) often helps.

Q: What does a Q-Q plot (normal quantile plot) of residuals check, and what does a good one look like?
A: It checks the normality assumption for the errors. If residuals are approximately normal, the points fall close to a straight 45-degree reference line. Systematic curvature or heavy tails suggest non-normality.

C: A plot of residuals against [time or observation order] is used to check the independence assumption; runs of positive or negative residuals suggest autocorrelation.

## 11.12 Correlation and Simple Regression

C: In simple linear regression, the coefficient of determination equals the square of the sample correlation: $R^2 = [r^2]$, where $r$ is the Pearson correlation between $X$ and $Y$.

Q: Why does $R^2 = r^2$ hold for simple linear regression but not in general for multiple regression?
A: In simple regression there is only one predictor, so "variation in $Y$ explained by the regression" reduces to the squared linear association between $X$ and $Y$, which is exactly $r^2$. With multiple predictors, $R^2$ summarizes the combined explanatory power of all of them and no longer equals a single pairwise correlation.

Q: If $\hat\beta_1 > 0$, what is the sign of the correlation $r$ between $X$ and $Y$?
A: Positive. Since $\hat\beta_1 = r \cdot (s_Y / s_X)$ and the standard deviations are non-negative, $\hat\beta_1$ and $r$ must share the same sign.

Q: Does a strong correlation between $X$ and $Y$ imply that $X$ causes $Y$?
A: No. Correlation (and regression) measures statistical association only. A nonzero slope can arise from $X$ causing $Y$, from $Y$ causing $X$, from a common cause (confounding), or from coincidence. Causal conclusions require a study design (experiment, controlled confounders), not just a regression.

## 11.13 Procedure: Fitting and Interpreting a Simple Regression

P: You are given $n$ paired observations $(X_i, Y_i)$ and want to fit a simple linear regression of $Y$ on $X$, test whether $X$ is a useful predictor, and report the result. How do you proceed?

S:
**IDENTIFY**: Simple linear regression task — one quantitative response $Y$, one quantitative predictor $X$, paired observations. Goal: estimate slope and intercept, quantify fit, test significance, check assumptions.

**PLAN**:
- Compute descriptive summaries $\bar X, \bar Y, S_{XX}, S_{XY}$.
- Fit the least-squares line using closed-form formulas.
- Compute fitted values, residuals, RSS, SST.
- Summarize fit with $R^2$ and $\hat\sigma$.
- Conduct inference on the slope ($t$-test and/or confidence interval).
- Diagnose assumptions with residual plots.

**EXECUTE**:
1. Compute means: $\bar X = \frac{1}{n}\sum X_i$, $\bar Y = \frac{1}{n}\sum Y_i$.
2. Compute $S_{XX} = \sum (X_i - \bar X)^2$ and $S_{XY} = \sum (X_i - \bar X)(Y_i - \bar Y)$.
3. Slope: $\hat\beta_1 = S_{XY}/S_{XX}$. Intercept: $\hat\beta_0 = \bar Y - \hat\beta_1 \bar X$.
4. Fitted values $\hat Y_i = \hat\beta_0 + \hat\beta_1 X_i$; residuals $e_i = Y_i - \hat Y_i$.
5. $\mathrm{RSS} = \sum e_i^2$; $\mathrm{SST} = \sum (Y_i - \bar Y)^2$; $R^2 = 1 - \mathrm{RSS}/\mathrm{SST}$.
6. $\hat\sigma = \sqrt{\mathrm{RSS}/(n-2)}$; $\mathrm{SE}(\hat\beta_1) = \hat\sigma/\sqrt{S_{XX}}$.
7. $t = \hat\beta_1 / \mathrm{SE}(\hat\beta_1)$ on $n - 2$ df; compute $p$-value for $H_0: \beta_1 = 0$.
8. 95% CI: $\hat\beta_1 \pm t_{0.025,\, n-2} \cdot \mathrm{SE}(\hat\beta_1)$.
9. Plot residuals vs fitted values (linearity, equal variance) and a Q-Q plot (normality).

**EVALUATE**:
- Interpret $\hat\beta_1$ in units: "a one-unit increase in $X$ is associated with a change of $\hat\beta_1$ units in the mean of $Y$."
- Report $R^2$ as the fraction of variation in $Y$ explained by $X$.
- Assess significance: if the CI excludes zero (equivalently $p < \alpha$), there is evidence $X$ is linearly associated with $Y$.
- Inspect residual plots: patterns indicate assumption violations and warn against trusting the inference or extrapolating.
- Do not claim causation from regression alone; state the association and the conditions under which it was observed.
