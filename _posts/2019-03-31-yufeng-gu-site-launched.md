---
layout: post
title: "An Overview on the Bootstrap"
date: 2019-03-31
---
## *Yufeng Gu, Huajin Yu*
---
## Abstract
In this paper, we try to illustrate the basic ideas and methods of the bootstrap by means of which people have access to estimation of the sampling distribution of almost any statistic using random sampling methods. The first two sections show its origin and theoretical background, and then provide a general process to apply the bootstrap. A simple case is shown for you to understand the ideas. In the end, we briefly discuss the advantages and disadvantages of the bootstrap.
## 1 Introduction
In statistics, bootstrapping is any test or metric that relies on random sampling with replacement. It allows assigning measures of accuracy (defined in terms of bias, variance,confidence intervals, prediction error or some other such measure) to sample estimates. This technique allows estimation of the sampling distribution of almost any statistic using random sampling methods. Generally, it falls in the broader class of re-sampling methods.
The idea of bootstrapping was initially introduced by Bradley Efron (1979). In his book published in 1993, Efron gives a complete framework of statistical inference using bootstrap, including estimate of standard errors, bias, establishment of regression models and confidence intervals, hypothesis testing, etc.
In general, the bootstrap can be classified into two groups:
i. Parametric bootstrap. While applying a parametric method, people usually make some assumptions on the probability density (mass) function, $f(x\vert\theta)$ or $p(x\vert\theta)$ , of population. The estimated function $f(x\vert\hat{\theta})$ is called a plug-in distribution.
ii. Non-parametric bootstrap. In contrast to parametric ways, non-parametric bootstrap estimates the population properties without assuming any function forms. It just re-sampling from a given sample and get the inferences about population.
In the next section, we will provide some statistical process and a simple practice of the bootstrap.
