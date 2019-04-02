<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>
# Notes for Model Selection & Regularization

## Cross Validation

Setting $$K=N$$ yields the **leave-one out cross-validation (LOOCV)** error:

$$CV_{N}(H)=\frac{1}{N}\sum_{i=1}^{N}{E_{in}^{i}(g^{-i}(H))}​$$

*5-fold cv, 10-fold cv, …*

***N-fold cv***: each time, you pick one data point as validation, to fit other *N-1* data.

***Advantage***: LOOCV gives almost <u>unbiased estimate</u> of the out-of-sample error, since its training set contains almost the entire data set.

***Disadvantage***: the LOOCV estimate has <u>high variance</u>: when we perform LOOCV, we are in effect averaging the outputs of *N* fitted models, each of which is trained on an almost identical set of observations. Therefore, these outputs are highly positive correlated with each other.

### Cross-Validation for Regression

$$ P(y=1)=\sigma(x',\beta)=\sigma(\beta_{1}+\beta_{2}x_1+\beta_{2}x_2+\beta_3x_1^2+\beta_4x_2^2+...) $$

We just use higher power to fit the model and reduce the out-of sample error.

### Note on Cross-Validation

### Alternatives to CV: Information Criteria ###

***Null Model***: a linear model which contains no predictors (only constant).

***Full Model***: a linear model which contains all potential predictors.

*Akaike's Information Criterion (AIC)*

$$AIC=\frac{1}{N}\sum_i{(y-\beta x)^2}+2p=Deviance +2p$$

$$BIC=\frac{1}{N}\sum_i{(y-\beta x)^2}+p \log{N}=Deviance +p \log{N}$$

- For both AIC and BIC, smaller values are better (how to choose the model with the minimum AIC or BIC).
- The term $$2p$$ in AIC and $$p \log{N}​$$ in BIC can be regarded as **penalty** terms that favor simpler models over more complicated ones.

### Subset Selection

*Forward Stepwise Selection*

1. Let $$M_0$$ denote the null model.
2. Fit all univariate models.
3. Fit all bivariate models that include $$x_{(1)}$$.
4. Continue until your model selection rule is lower for the current model than for any of the models that add one variable.

### Credit Card Balance (Codes)

```R
require (AER)
credit <- read.csv("Credit.csv")
fit <- lm(Balance~.,credit)
coeftest(fit)
```

```R
require (leaps)
all.fit <- regsubsets(Balance~., credit)
all <- summary(all.fit)
all$outmat
```

## Bias-Variance Trade-off

The **goal** of model selection is to choose the model (out of the set of candidate models) that can best balance the bias-variance tradeoff to achieve the **smallest out-of-sample error**.

In the case of linear models, we have:

$$ E[(y-x'\hat{\beta})]^2=Var(x'\hat{\beta})+[bias(x'\hat{\beta})]^2+Var(e) ​$$

### The Gauss-Markov Theorem

For linear model $$y=\beta x+e$$

OLS: $$\hat{\beta}=(X'X)^{-1}X'Y​$$

$$ E[(y-\beta x)^2]=Var(\beta x)+bias^2+\sigma^2 ​$$

For OLS, the $$bias^2​$$ term equals *zero*.

Gauss-Marcov BLUE: the best linar unbiased estimator.

*Gauss-Markov Theorem*

Under the assumption that

1. The true CEF is linear: $$E[y\vert x]=x'\beta^*​$$
2. Homoskedasticity: $$E[(e^*)^2\vert x]=\sigma^2​$$

The OLS estimator $$\hat{\beta}^{LS}$$ is **BLUE**: Best Linear Unbiased Estimator.

If unbiased and smallest variance, then the mean of error is smallest.

***A way to get better linear estimaor: increase the bias, until the variance term becomes much smaller.***

### Exploring the Bias-Variance Trade-off ###

$$\rightarrow E_{D,x}[\left(y-x'\hat{\beta}^{LS}\right)^2]\approx \frac{1}{N}\sum_{i=1}^{N}{E_D\left[\left(y_i-x_i'\hat{\beta}^{LS}\right)^2\right]}\approx \frac{1}{N}(1+p)\sigma^2+\sigma^2$$

- Each additional predictor adds the same amount of variance $$\frac{\sigma^2}{N}​$$, regardless of whether its true coefficient is large or mall (or zero).
- We can do better by `shrinking` small coefficients towards zero, incurring some bias, so as to reduce the variance. Methods that do this are called **shrinkage methods**.

### Ridge Regression ###

$$\hat{\beta}^R=\arg {\min_{\beta}{\sum_{i=1}^{N}{(y_i-\beta_0-\sum_{j=1}^{p}{\beta_jx_{ij}})^2}+\lambda\sum_{j=1}^{p}{\beta_j^2}}}​$$

where $$\lambda \geq 0​$$ is a **tuning parameter** that controls the strength of the penalty term, which has the effect of shrinking the estimates towards zero.

$$\lambda=0 \rightarrow \hat{\beta}^R=\hat{\beta}^{LS}$$

$$\lambda=\infty \rightarrow \hat{\beta_1}^R = \cdots =\hat{\beta_p}^R=0$$



An equivalent way to write the ridge problem is:

$$\hat{\beta}^R=\arg {\min_{\beta}{\sum_{i=1}^{N}{(y_i-\beta_0-\sum_{j=1}^{p}{\beta_jx_{ij}})^2}}}$$

subject to $$\sum_{j=1}^p{\beta_j^2}\leq C$$

$$\hat{\beta_j}^R=\frac{\hat{\beta_j}^{LS}}{1+\lambda}$$

- To choose $$\lambda$$, we can treat $$\lambda$$ as a hyperparameter and select its value via cross-validation.

