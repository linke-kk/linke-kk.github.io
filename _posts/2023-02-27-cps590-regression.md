---
layout: default
title: Data Science:Regression
---
# Regression
## Data Exploration
Data is distributed on multiple variables.
### Marginal Distribution
The probabilities of different values of the variables without reference to the values of the other variables. In another word, how data is distributed on single variable.\
"In a dataset of N differnet variables, it should have N different marginal distributions."
### Conditional Distribution
### Response Variable and Explanatory Variables
Response variables depent on explanatory variables.\
Manipulate explanatory variable, see the effect on the response variable.\
Can exchange when tasks change.
## Models
### Generalized Linear Model (GLM)
$$E[y|\mathbf{x}]=f(\mathbf{x}'\mathbf{\beta})$$
$f$ is the link function, potentially sigmoid or neural networks \
If $f$ is identity mapping, GLM is degraded to Linear Regression \
But given a covariate vectore, the model only gives us an conditional expectation instead of a conditional distribution.\
We can add a $\epsilon\sim N(0, \sigma^2)$ to model the conditional distribution.\
Central Limit Theorem?
#### Risiduals
$$\hat{y_i}=\mathbf{x_i}'\hat{\beta}$$
$$e_i=y_i-\hat{y_i}=y_i-\mathbf{x_i}'\hat{\beta}$$
#### Deviance
The difference between the fitted model and the data.\
Deviance = aggregate of residuals.\
- SST: Sum Squared Total Error $\Sigma_i{(y_i-\bar{y})^2}$, also called null deviance, assuming only use a gaussion model to model the response variable\
- SSE: Sum Squared Residual Error $\Sigma_i{e_i^2}$\
- MSE: Mean Squared Error $SSE/n$, where n is the sample size. Normalize SSE to facilitate comparison.
#### Metrics
$R^2=1-\frac{SSE}{SST}$ is the proportion of variability explained by the regression.\
A model explains $R^2\times100%$ of the variability in the data.


### Log-log Models and Elasticities
$$y=log(r)=\beta_0+\beta_1log(x)+\epsilon$$
$\beta_1=\frac{dy/y}{dx/x}$ is called the elasticity, meaning how changes of $x$ will result in change of $y$\
Why elasticity is not defined in $\frac{dy}{dx}$? Because is only cares single feature. "$\frac{dy}{dx}$ will be effected by other terms?" ?
### Logistic Regression 
## Interations within covariates
Covariates may not be independent from each other. Does it hurt?\
An interation term is the product of two inputs.
$$E[y|\texbf{x}]=\beta_0+...+\beta_kx_k+\beta_jx_j+x_jx_k\beta_{jk}$$

## Degrees of Freedom
- Model Degree of Freedom \
"the number of random observations a model can fit perfectly", in regression models, the number of coefficients
- Residual Degree of Freedom \
The number of opportunities that one has to observe variation around the fitted model. \
y = ax + b, two points will be used to fit the model, other used to observe variation

## Logit Link Function
$$E[y|\mathbf{x}]=f(\mathbf{x}'\beta)$$ \
$$E[y|\mathbf{x}]=p(y=1|\mathbf{x})\times1+p(y=0|\mathbf{x})\times0=p(y=1|\mathbf{x})$$ \
$$p(y=1|\mathbf{x})=f(\mathbf{x}'\beta)$$ \
$f$ needs to map from $(-\infty,\infty)$ to $[0, 1]$ \
Logit link function $f(z)=\frac{e^z}{1+e^z}$ \

## Mapping from $(-\infty, \infty)$ to [0, 1]
An engineering problem, candidates as below
- (Probit) Cumulative Normal Distribution Function: Costly in computation
- Logit $\frac{e^z}{1+e^z}$

## Odds $\frac{p}{1-p}$
Logistic regression is a linear model for log odds

## Relation between Data and Model
### Likelihood
The probability of the data given the estimated model \
Linear Regression + Gaussian Distribution -> Likelihood of a data point in the model \
Maximize likelihood -> Minimize Diviance
- Gaussian Deviance
- Logistic Deviance -> Cross Entropy?

## Regression in Time Series Data
TODO


