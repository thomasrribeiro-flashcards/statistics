+++
order = 12
subject = "Math"
tags = ["math", "statistics", "regression", "multiple", "ols", "multicollinearity", "r-squared"]
+++

# Statistics — Multiple Linear Regression

## 12.1 Why Multiple Predictors?

Q: Why extend simple linear regression (one predictor) to multiple linear regression?
A: Real outcomes almost always depend on several variables at once. Using a single predictor leaves legitimate explanatory variables in the error term, where they can bias the slope and inflate the residual variance. Adding predictors lets us control for confounders and typically improves prediction accuracy.

Q: What is a confounder in a regression context?
A: A variable that is associated with both the outcome $Y$ and a predictor $X_j$, so that ignoring it distorts the apparent relationship between $X_j$ and $Y$. Including it as an additional predictor lets us estimate the effect of $X_j$ while holding the confounder fixed.

Q: Give a concrete example where a simple regression misleads but a multiple regression corrects it.
A: Regressing salary on years of education alone may overstate education's effect because older workers tend to be both more educated and more experienced. Adding experience as a second predictor separates the two effects, so each coefficient reflects the effect of its variable while holding the other constant.

C: Multiple regression can [control for confounding] by estimating the effect of each predictor while holding the other predictors fixed.

C: Compared with simple regression, multiple regression typically [improves prediction] because additional predictors explain variation that would otherwise be absorbed into the error term.

## 12.2 The Multiple Regression Model

Q: Before writing the model down, predict: what must the equation for multiple regression look like if it is a direct generalization of simple regression?
A: A linear combination of several predictors with their own slopes, plus an intercept and a random error term — one slope per predictor instead of just one slope total.

C: The [multiple linear regression model] with $p$ predictors is $Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \cdots + \beta_p X_p + \varepsilon$, where $Y$ is the response, $X_1, \ldots, X_p$ are predictors, $\beta_0$ is the intercept, $\beta_1, \ldots, \beta_p$ are slope coefficients, and $\varepsilon$ is a random error term.

C: In the model $Y = \beta_0 + \beta_1 X_1 + \cdots + \beta_p X_p + \varepsilon$, the intercept $\beta_0$ is the [expected value of $Y$] when all predictors equal zero.

C: In multiple regression, the error term $\varepsilon$ is assumed to have [mean zero] so that $E[Y \mid X_1, \ldots, X_p] = \beta_0 + \beta_1 X_1 + \cdots + \beta_p X_p$.

Q: What are the standard assumptions on the error term $\varepsilon$ in multiple linear regression?
A: $\varepsilon$ has mean zero, constant variance $\sigma^2$ (homoscedasticity), is uncorrelated across observations, and — for exact inference — is normally distributed. The predictors are treated as fixed or exogenous (uncorrelated with $\varepsilon$).

Q: Why is the model called "linear" even when a predictor like $X_1^2$ appears?
A: "Linear" refers to linearity in the parameters $\beta_j$, not in the predictors. The model is a linear combination of the $\beta_j$'s, so $X_1^2$ or $\log X_1$ can serve as predictors without violating linearity.

## 12.3 Matrix Form of the Model

Q: Why rewrite the multiple regression model in matrix form?
A: Writing every observation separately hides structure and scales badly when $n$ and $p$ are large. Matrix notation compresses $n$ equations into one, and lets us derive the OLS estimator with a few lines of linear algebra that work for any $p$.

C: The [matrix form] of the multiple regression model is $\mathbf{Y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\varepsilon}$, where $\mathbf{Y}$ is an $n \times 1$ response vector, $\mathbf{X}$ is an $n \times (p+1)$ design matrix, $\boldsymbol{\beta}$ is a $(p+1) \times 1$ coefficient vector, and $\boldsymbol{\varepsilon}$ is an $n \times 1$ error vector.

C: In $\mathbf{Y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\varepsilon}$, the response vector $\mathbf{Y}$ has dimension [$n \times 1$], where $n$ is the number of observations.

C: In $\mathbf{Y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\varepsilon}$, the coefficient vector $\boldsymbol{\beta}$ has dimension [$(p+1) \times 1$], where $p$ is the number of predictors (the extra entry is the intercept $\beta_0$).

Q: In matrix form, what does the $i$-th row of the equation $\mathbf{Y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\varepsilon}$ represent?
A: The equation for the $i$-th observation: $Y_i = \beta_0 + \beta_1 X_{i1} + \cdots + \beta_p X_{ip} + \varepsilon_i$. Stacking these $n$ equations row by row reproduces the full matrix form.

## 12.4 The Design Matrix

C: The [design matrix] $\mathbf{X}$ is the $n \times (p+1)$ matrix whose first column is all ones (for the intercept) and whose remaining $p$ columns hold the observed predictor values, one row per observation.

C: The first column of the design matrix $\mathbf{X}$ is a [column of ones], which multiplies the intercept $\beta_0$.

Q: Why does the design matrix have a column of 1s?
A: It lets the intercept $\beta_0$ be treated as just another coefficient in the product $\mathbf{X}\boldsymbol{\beta}$. Without that column, $\beta_0$ would have to be handled separately and the matrix formulas would need extra bookkeeping.

Q: For 3 observations and 2 predictors with values $(X_{i1}, X_{i2})$ equal to $(1, 4)$, $(2, 5)$, $(3, 6)$, what does the design matrix look like?
A: $\mathbf{X} = \begin{pmatrix} 1 & 1 & 4 \\ 1 & 2 & 5 \\ 1 & 3 & 6 \end{pmatrix}$ — a leading column of ones, then one column per predictor.

Q: What does it mean for the design matrix $\mathbf{X}$ to have full column rank?
A: Its columns are linearly independent, i.e. no predictor (and no 1-column) is an exact linear combination of the others. Full column rank is required for $\mathbf{X}^T \mathbf{X}$ to be invertible and hence for the OLS formula to produce a unique estimate.

## 12.5 Normal Equations and the OLS Solution

Q: Before deriving it, predict: what criterion do we minimize to estimate $\boldsymbol{\beta}$ in multiple regression?
A: The sum of squared residuals $\sum_{i=1}^n (Y_i - \hat{Y}_i)^2$ — the same least-squares criterion as in simple regression, just generalized to more predictors.

C: The [residual sum of squares] (RSS) as a function of $\boldsymbol{\beta}$ is $\text{RSS}(\boldsymbol{\beta}) = (\mathbf{Y} - \mathbf{X}\boldsymbol{\beta})^T (\mathbf{Y} - \mathbf{X}\boldsymbol{\beta})$.

C: Setting the gradient of RSS to zero gives the [normal equations] $\mathbf{X}^T \mathbf{X} \boldsymbol{\beta} = \mathbf{X}^T \mathbf{Y}$.

C: If $\mathbf{X}^T \mathbf{X}$ is invertible, the [OLS estimator] is $\hat{\boldsymbol{\beta}} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{Y}$, where $\mathbf{X}$ is the $n \times (p+1)$ design matrix and $\mathbf{Y}$ is the $n \times 1$ response vector.

Q: When is $\mathbf{X}^T \mathbf{X}$ not invertible, and what does that mean for OLS?
A: When the columns of $\mathbf{X}$ are linearly dependent — for example, one predictor is a linear combination of others, or a dummy variable trap is present. Then no unique OLS solution exists, and statistical software either drops a predictor or returns an error.

Q: Why does the OLS solution minimize RSS rather than some other loss?
A: Under the Gauss-Markov assumptions (linearity, zero-mean errors, constant variance, uncorrelated errors), OLS is the best linear unbiased estimator — it has the smallest variance among all linear unbiased estimators. Squared-error loss also gives a closed-form solution via linear algebra.

P: How do you compute the OLS estimate $\hat{\boldsymbol{\beta}}$ for a multiple regression given data $(\mathbf{X}, \mathbf{Y})$?

S:
**IDENTIFY**: Closed-form OLS estimation problem — need $\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{Y}$.

**PLAN**:
- Build the design matrix $\mathbf{X}$ (column of 1s + predictor columns).
- Compute $\mathbf{X}^T \mathbf{X}$ and $\mathbf{X}^T \mathbf{Y}$.
- Invert $\mathbf{X}^T \mathbf{X}$ and multiply.

**EXECUTE**:
1. Form $\mathbf{X}$ of size $n \times (p+1)$ and $\mathbf{Y}$ of size $n \times 1$.
2. Compute the $(p+1) \times (p+1)$ matrix $\mathbf{X}^T \mathbf{X}$.
3. Compute the $(p+1) \times 1$ vector $\mathbf{X}^T \mathbf{Y}$.
4. Check that $\mathbf{X}^T \mathbf{X}$ is invertible (full column rank).
5. Compute $\hat{\boldsymbol{\beta}} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{Y}$.

**EVALUATE**:
- $\hat{\boldsymbol{\beta}}$ has one entry per column of $\mathbf{X}$ (intercept plus each predictor's slope).
- Fitted values: $\hat{\mathbf{Y}} = \mathbf{X}\hat{\boldsymbol{\beta}}$; residuals: $\mathbf{e} = \mathbf{Y} - \hat{\mathbf{Y}}$.
- By construction, $\mathbf{X}^T \mathbf{e} = \mathbf{0}$, so residuals are orthogonal to every predictor column.

## 12.6 Interpreting $\hat{\beta}_j$

Q: Why does the interpretation of a slope change when going from simple to multiple regression?
A: In simple regression, $\hat{\beta}_1$ captures the total association between $X_1$ and $Y$. In multiple regression, $\hat{\beta}_j$ captures only the part of the association with $X_j$ that remains after removing the linear effects of the other predictors — a partial, not total, effect.

C: In multiple regression, $\hat{\beta}_j$ is the estimated change in $Y$ per one-unit increase in $X_j$, [holding all other predictors fixed].

C: The coefficient $\hat{\beta}_j$ in multiple regression is called a [partial regression coefficient] because it reflects the effect of $X_j$ after controlling for the other predictors.

Q: A simple regression gives $\hat{\beta}_1 = 5$ for education on wage, but adding experience drops it to $\hat{\beta}_1 = 2$. What does this mean?
A: Part of what looked like an "education effect" was actually experience acting through education (older, more-experienced workers also tend to have more schooling). After holding experience fixed, each extra year of education is associated with only a \$2 wage increase, not \$5.

Q: Why is the phrase "holding other predictors fixed" a ceteris paribus statement, not a causal one?
A: OLS describes an association pattern in the data assuming the linear model. "Holding fixed" means statistical adjustment, not an actual intervention. Causal interpretation requires additional assumptions (no unmeasured confounders, correct functional form, etc.).

## 12.7 $R^2$ and Adjusted $R^2$

C: In multiple regression, [$R^2$] is the fraction of total variation in $Y$ explained by the fitted model: $R^2 = 1 - \frac{\text{RSS}}{\text{TSS}}$, where $\text{RSS} = \sum (Y_i - \hat{Y}_i)^2$ and $\text{TSS} = \sum (Y_i - \bar{Y})^2$.

C: In the formulas $\text{RSS} = \sum (Y_i - \hat{Y}_i)^2$ and $\text{TSS} = \sum (Y_i - \bar{Y})^2$, $Y_i$ is the [observed response], $\hat{Y}_i$ is the fitted value, and $\bar{Y}$ is the sample mean of the responses.

Q: Why is plain $R^2$ misleading when comparing models with different numbers of predictors?
A: $R^2$ can only stay the same or increase when you add predictors, even if those predictors are pure noise. So it always rewards bigger models and never penalizes overfitting.

C: [Adjusted $R^2$] penalizes extra predictors: $R^2_{\text{adj}} = 1 - \frac{\text{RSS}/(n - p - 1)}{\text{TSS}/(n - 1)}$, where $n$ is the sample size and $p$ is the number of predictors (excluding the intercept).

Q: How does adjusted $R^2$ differ from $R^2$ when you add a useless predictor?
A: $R^2$ cannot decrease. Adjusted $R^2$ divides RSS by $n - p - 1$ instead of $n$: adding a predictor increases $p$, shrinking the denominator and inflating RSS/(n - p - 1) unless the predictor reduces RSS enough to compensate. So adjusted $R^2$ can — and usually does — decrease when a useless predictor is added.

Q: Can adjusted $R^2$ be negative? What would that mean?
A: Yes. If the fitted model explains less variation than a model containing only the mean, adjusted $R^2$ can fall below zero, signaling the predictors collectively hurt rather than help.

## 12.8 F-Test for Overall Regression

Q: What question does the overall F-test answer?
A: Does the set of predictors, taken together, explain a statistically significant amount of variation in $Y$? Equivalently: is at least one slope nonzero?

C: The [null hypothesis] of the overall F-test is $H_0: \beta_1 = \beta_2 = \cdots = \beta_p = 0$ — every slope (not the intercept) is zero.

C: The [alternative hypothesis] of the overall F-test is $H_1$: [at least one $\beta_j \neq 0$], for $j = 1, \ldots, p$.

C: The F-statistic for the overall regression is $F = [\frac{(\text{TSS} - \text{RSS})/p}{\text{RSS}/(n - p - 1)}]$, where $n$ is the sample size and $p$ is the number of predictors.

Q: Under $H_0$, what distribution does the overall F-statistic follow?
A: An F-distribution with $p$ numerator degrees of freedom and $n - p - 1$ denominator degrees of freedom, assuming normal errors.

Q: Why use an F-test for "at least one slope is nonzero" rather than a bunch of t-tests?
A: Running $p$ separate t-tests at level $\alpha$ inflates the overall false-positive rate. The F-test gives a single, joint assessment of whether the predictors together improve on the intercept-only model, at the stated $\alpha$.

## 12.9 t-Tests for Individual Coefficients

C: The [t-statistic] for testing $H_0: \beta_j = 0$ in multiple regression is $t_j = \frac{\hat{\beta}_j}{\text{SE}(\hat{\beta}_j)}$, where $\hat{\beta}_j$ is the estimated coefficient and $\text{SE}(\hat{\beta}_j)$ is its standard error.

C: Under $H_0: \beta_j = 0$ with normal errors, $t_j$ follows a $t$-distribution with [$n - p - 1$] degrees of freedom, where $n$ is the sample size and $p$ is the number of predictors.

Q: What does the p-value next to an individual coefficient in regression output tell you?
A: The probability, assuming $\beta_j = 0$ and the other predictors are in the model, of observing a t-statistic at least as extreme as the one computed. A small p-value suggests $X_j$ adds explanatory power beyond the other predictors.

Q: Can the overall F-test reject $H_0$ while no individual t-test does? What does that signal?
A: Yes — this is a classic sign of multicollinearity. Predictors jointly explain a lot of variation in $Y$, but because they overlap, each one's unique contribution looks small, inflating their standard errors.

## 12.10 Multicollinearity

C: [Multicollinearity] occurs when two or more predictors in a regression are highly linearly correlated with each other.

Q: Why is multicollinearity a problem for OLS?
A: When predictors are nearly linearly dependent, $\mathbf{X}^T\mathbf{X}$ is close to singular, so its inverse has large entries. This blows up the standard errors of $\hat{\beta}_j$, making coefficients unstable and individual t-tests unlikely to reject — even when the predictors are jointly important.

Q: Does multicollinearity bias the OLS coefficient estimates?
A: No. OLS remains unbiased under multicollinearity (assuming $\mathbf{X}^T\mathbf{X}$ is still invertible). The problem is variance, not bias: the coefficients are correct on average but very imprecise.

C: The [variance inflation factor] ($\text{VIF}_j$) measures how much the variance of $\hat{\beta}_j$ is inflated by multicollinearity: $\text{VIF}_j = \frac{1}{1 - R_j^2}$, where $R_j^2$ is the $R^2$ from regressing $X_j$ on all other predictors.

C: A common rule of thumb flags multicollinearity when $\text{VIF}_j$ exceeds [10] (some texts use 5 as a stricter threshold).

Q: What does $\text{VIF}_j = 1$ mean?
A: $X_j$ is uncorrelated (in the linear sense) with the other predictors, so multicollinearity is not inflating $\hat{\beta}_j$'s variance at all — the best-case scenario.

Q: Name three practical fixes for severe multicollinearity.
A: (1) Drop one of the correlated predictors; (2) combine correlated predictors into a single composite (e.g., an index or principal component); (3) collect more data, which can reduce variance even when predictors remain correlated.

## 12.11 Categorical Predictors and Dummy Variables

Q: Why can't we simply plug a categorical variable like "color = red/green/blue" into a regression as numbers 1, 2, 3?
A: Numeric codes like 1, 2, 3 impose an artificial ordering and equal spacing that usually have no meaning for categories. The fitted slope would force "green" to be halfway between "red" and "blue" in its effect on $Y$, which is nonsense for unordered categories.

C: A [dummy variable] (or indicator variable) is a 0/1 variable that encodes whether an observation belongs to a particular category.

C: For a categorical predictor with $k$ levels, we create [$k - 1$] dummy variables and treat one level as the reference (baseline) category.

Q: Why use only $k - 1$ dummy variables for a $k$-level categorical predictor?
A: Including a dummy for every level plus the intercept creates perfect collinearity — the $k$ dummies sum to the column of 1s. This is the "dummy variable trap." Dropping one dummy breaks the collinearity and makes its category the baseline.

Q: In a regression with a dummy variable $D$ for "treatment" (1 = treated, 0 = control), how do you interpret $\hat{\beta}_D$?
A: The estimated difference in mean $Y$ between the treated group and the control group, holding all other predictors fixed. The control group (coded 0) serves as the baseline.

Q: If "season" has four levels (Spring, Summer, Fall, Winter) with Winter as the reference, how are the dummy coefficients interpreted?
A: The three slopes on $D_{\text{Spring}}$, $D_{\text{Summer}}$, $D_{\text{Fall}}$ each give the estimated difference in mean $Y$ between that season and Winter, holding other predictors fixed. Winter's effect is absorbed into the intercept.

## 12.12 Model Selection

Q: Why do we need model selection procedures instead of just including every possible predictor?
A: Extra predictors inflate variance, increase multicollinearity risk, and can overfit the training sample, hurting out-of-sample prediction. Model selection seeks a balance: include predictors that genuinely improve fit, exclude those whose cost in variance outweighs their benefit.

C: [Forward stepwise selection] starts from the intercept-only model and repeatedly adds the predictor that most improves a chosen criterion, stopping when no addition improves it.

C: [Backward stepwise selection] starts from the full model (all predictors) and repeatedly removes the predictor whose removal most improves (or least worsens) the criterion, stopping when no removal helps.

C: [AIC] (Akaike Information Criterion) is defined as $\text{AIC} = -2 \ln L + 2 k$, where $L$ is the maximized likelihood of the model and $k$ is the number of estimated parameters; smaller AIC is preferred.

C: [BIC] (Bayesian Information Criterion) is defined as $\text{BIC} = -2 \ln L + k \ln n$, where $L$ is the maximized likelihood, $k$ is the number of parameters, and $n$ is the sample size; smaller BIC is preferred.

Q: How do AIC and BIC differ in their penalty, and what does that mean in practice?
A: AIC penalizes each extra parameter by $2$, while BIC penalizes by $\ln n$. For any $n \geq 8$, $\ln n > 2$, so BIC imposes a heavier penalty and tends to select smaller models. AIC is more prediction-oriented; BIC is more conservative and asymptotically picks the "true" model when it is among the candidates.

Q: Name two important limitations of stepwise selection.
A: (1) The reported p-values and standard errors are no longer valid — they ignore the selection process. (2) Stepwise is a greedy search and can miss the best subset entirely, especially when predictors are correlated.

Q: When choosing between two nested models, what's the connection between comparing $R^2_{\text{adj}}$, AIC, and a partial F-test?
A: All three trade off fit against complexity, just with different penalties. A partial F-test formalizes "is the extra variance explained more than expected by chance"; adjusted $R^2$ and AIC/BIC provide continuous penalized-fit scores for non-nested or exploratory comparisons. For nested models with Gaussian errors, they often agree but can disagree on borderline cases.
