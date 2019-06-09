<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

<script type="text/x-mathjax-config">
 MathJax.Hub.Config({	
tex2jax: {inlineMath: [['$', '$']]},	
messageStyle: "none"	
});	
</script>

*Yufeng Gu & Huajin Yu*

## Abstract

Economists always care about internal and external validity when they make causal inference. In reality, causal effects also depend on the time length of your data. This paper provides an extension on the traditional causal inference framework by attaching time horizon effects to it. We use a case of tobacco taxation to analyze this additional effect. Our conclusion is that, different choices of time length may account for ambiguous results.

## 1 Introduction

Causal inference refers to a set of tools used in causal effect learning and causal mechanism learning. Econometric researchers want to specify the effects of inputs on the outputs. Theoretical literature mainly focuses on how to capture the real treatment effects, and empirical paper is usually concerned with the internal and external validity of the results. However, few people think about the differences between short- and long-run effects. In particular, many economic policies have lagged effects, which may bring lots of difficulty to policy evaluation, because the selection of time horizon often depends on people's prior beliefs about when the policies will work.

In this paper, we want to establish a theoretical framework to explain the time horizon effects in causal inference. Part 1 is an introduction on causal inference and time horizon effects. In part 2, we try to analyze the effects of tobacco taxation on the demand of cigarettes. At last, we summarize our work in this paper and give a conclusion.

## 2 Case Study: Tobacco Taxes

The tobacco taxation is launched for reducing illnesses and deaths from smoking as well as the externalities imposed by those illnesses on the rest of society. That key idea is to tax cigarettes so heavily that current smokers cut back and potential new smokers are discouraged from taking up the habit. Policy makers want to figure out the marginal effect of tax size on cigarette consumption in order to set the tax properly. An effective tax increase should both increase prices of tobacco products and make them less affordable.

![price_demand_cancer](/homework/price_demand_cancer.png)

That economists care about tobacco taxes is not strange. Firstly, the demand of tobacco responds to price changes relative to the price of other products, real income changes, and changes in tastes and preferences. Secondly, about 75 percent of tobacco leaves grown globally are used for cigarettes and it has few close substitutes. Thirdly, tobacco is not like most other products, which is addictive and harmful to users and to others in society. Moreover, tobacco industry is an oligopoly, including a large number of consumers and relative smaller number of producers. Under this situation, industry tends to fully shift the tax increase to consumers rather than absorbing it. We can see cases of overshifting when the industry ends up increasing the price by more than the consequence of the tax increase to augment its profit margin.

![tax_prevalence](/homework/tax_prevalence.png)

Using price elasticity of demand, we get the formula

$$
\frac{\Delta Q/Q}{\Delta P/P}=\frac{Q_2-Q_1}{P_2-P_1}\times \frac{P_1}{Q_1}
$$

Because of addictive nature of tobacco products, tobacco demand is not very sensitive to price changes. i.e., the short-term price elasticity of demand for tobacco is between 0 and -1, while that in the long run is estimated to be higher (more sensitive) than in the short run. As time goes by, people adjust to a price change and are expected to reduce their consumption further.

Another concern is for the cross price elasticity. Demand will also be affected by changes in prices of alternative products such as fine cut tobacco for roll your own for pipes, or cigars or bidis, etc.

Furthermore, we should also care about different price elasticity among various age groups. For instance, the youth who have no wage may show a rather high price elasticity. If we increase the time horizon, they will become adults after 5 or 10 years and earn substantial salaries. It indicates that income elasticity is an endogenous variable for this research.

## 3 Conclusion

Time horizon effect is a problem that is often overlooked in causal inference. This paper explores the differences between short- and long-run effects that may exist in policy evaluation through a simple theoretical framework.It's worth noting that, because of the price elasticity of demand and the sticky prices in the short-run as well as potential change in income elasticity, the impacts of many economic policies that may affect the supply and demand are related to the length of time. Therefore, people should take it seriously when they conduct policy evaluation using econometrics tools.

## References

1. Den Broeke, M. V., De Baets, S., Vereecke, A., Baecke, P., & Vanderheyden, K. (2018). Judgmental forecast adjustments over different time horizons. *Omega-international Journal of Management Science*.
2. Perucic, A. M. (2012). The demand for cigarettes and other tobacco products. *TobTaxy Capacity Building Workshop*, 20-22 February 2012, Dublin, Ireland.
3. Stock, J. H., & Watson, M. W. (2003). *Introduction to econometrics* (Vol. 104). Boston: Addison Wesley.
