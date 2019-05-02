<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {inlineMath: [['$', '$']]},
        messageStyle: "none"
    });
</script>

*Yufeng Gu & Huajin Yu, WISE*

## Abstract

The growth of classification and regression trees (CART) brings about two main concerns. One is how to choose a proper indicator, and the other is how we can find the best spilt point for the variable we choose. In this report, we introduce two widely used measures of CART, including their basic ideas, mathematical insights and processing strategy.

## 1 Introduction

Decision tree is one of the most popular methods of machine learning. As its name suggests, a decision tree consists of one root and lots of  leaves, as well as some internal nodes linking them. Each leaf corresponds to one decision result, while each internal node represents an attribute test.

The tree  follows a recursive process applying  "divide-and-conquer" strategy. People compare their observations with the initial-set critical value for these variables. It's obvious that tree methods strongly lie on the mathematical background.

## 2 Measures for Classification Tree

The optimal grouping variable and optimal spilt point are defined as those who lead to largest decrease in node impurity. Because of different types of input variables, measures for classification trees and regression trees are not exactly the same. In this section, we focus on classification.

### 2.1 Gini Coefficient

The Gini coefficient is defined as:

$$
G=1-\sum_{j=1}^k{p^2(j)}
$$

Where $k$ denotes the amount of classes for inputs, and $p(j)$ the proportion of outputs that fall in class $j$ . Particularly, if all the outputs in the sample belong to the same class, there exists $G_{\min}=0$ . If each class has a proportion equal to $\frac{1}{k}$ , we can get the largest Gini coefficient $G_{\max}=1-\frac{1}{k}$ .

In a classification tree, the Gini coefficient for a node $$t$$ is defined as:

$$
G(t)=1-\sum_{j=1}^k{p^2(j|t)}
$$

Where $p(j|t)=\frac{p(j,t)}{\sum_j{p(j,t)}}$ , $p(j,t)=\frac{N_{j,t}}{N_j}$ . $p(j|t)$ can be interpreted as conditional probability and $N_{j,t}$ denotes the sample size of those inputs belong to class $j$ . The clustering operation $\sum_j{p(j,t)}$ aims to make the Gini coefficients of different nodes comparable.

Based on these concepts, people use the reduction of Gini coefficient to measure the decrease of impurity, whose mathematical form is:

$$
\Delta G(t)=G(t)-\{\frac{N_r}{N}G(t_r)+\frac{N_l}{N}G(t_l)\}
$$

Where $G(t)$ and $N$ is respectively the Gini coefficient and sample size of initial node $t$ , and $G(t_l) , N_l$ and $G(t_r) , N_r$ denote those of two subnodes. The big parentheses denote the weighted average of two subnodes. The optimal category variable and spilt point can be obtained through the function $\arg_{r,l}\max{\Delta G(t)}​$ .

### 2.2 Information Entropy and Gain Ratio

The information entropy is the most commonly used indicator for measuring the impurity of a sample set. Information theory is first proposed by C. E. Shannon (1948), which mainly deals with problems in information transfer.

There are two points worth noting:

1. Information transfer is achieved through a delivery system consisting of source, channel and sink. The source is the sender of the information, and the sink is the receiver of the information
2. The delivery system exists in a random interference environment, and thus there is a random error in the transmission of information.

Let $U$ denote the message sent and $V$ denote the message received, then we can define a channel model $P(U|V)$ . The channel transmission probability matrix $P(U|V)$ is a conditional probability matrix:

$$
\begin{bmatrix}P(u_1|v_1) & P(u_2|v_1) & \cdots & P(u_r|v_1)\\P(u_1|v_2) & P(u_2|v_2) & \cdots & P(u_r|v_2)\\ \vdots & \vdots & \ & \vdots\\P(u_1|v_q) & P(u_2|v_q) & \cdots & P(u_r|v_q)\end{bmatrix}
$$

Where $P(u_i|v_j)$ denotes the probability of sending $u_i$ conditional on receiving $v_j$ , and there should exist $\sum_{i=1}^r{P(u_i|v_j)}=1\ (j=1,2,\cdots,q)$ .

The amount of information is defined as:

$$
I(u_i)=\log_2{\frac{1}{P(u_i)}}=-\log_2{P(u_i)}
$$

Given all the definition above, the information entropy is the expectation of the amount of information:

$$
Ent(U)=\sum_i{P(u_i)\log_2{\frac{1}{P(u_i)}}}=-\sum_i{P(u_i)\log_2{P(u_i)}}
$$

Particularly, if $P(u_i)=1$ , the probability of sending $u_i$ is 100%, and there is no uncertainty in transmission, $Ent(U)=0$ . If $r$ messages have the same sending probability, i.e. $P(u_i)=\frac{1}{r}\ (I=1,2,\cdots,r)$ , we have the largest uncertainty in transmission and $Ent(U)=-\log_2{\frac{1}{r}}$ .

We can further derive the posterior entropy given receiving message $v_j$:

$$
Ent(U|v_j)=\sum_i{P(u_i|v_j)\log_2{\frac{1}{P(u_i|v_j)}}}=-\sum_i{P(u_i|v_j)\log_2{P(u_i|v_j)}}
$$

The expectation of posterior entropy can be written as:

$$
Ent(U|V)=\sum_j{P(v_j)[-\sum_i{P(u_i|v_j)\log_2{P(u_i|v_j)}}]}
$$

This formula is also called conditional entropy or channel equivocation. Usually, there exists $Ent(U|V)<Ent(U)$ . Thus, we can take difference between these two entropy, obtaining the gain ratio:

$$
Gains(U,V)=Ent(U)-Ent(U,V)
$$

The gain ratio captures how much uncertainty information $V$ eliminates.

In a classification tree, if we regard the value of input as $V$ and output as $U$, the measure for decrease of impurity can be defined:

$$
Gains(t)=Ent(t)-\{\frac{N_r}{N}Ent(t_r)+\frac{N_l}{N}Ent(t_l)\}
$$

The interpretation for notations is the same as that for Gini coefficient. The optimal category variable and spilt point can be obtained through the function $\arg_{r,l}\max{Gains(t)}​$.

## 3 Measure for Regression Tree

Here we only talk about the case of numerical inputs. Since the outputs for a regression tree are numerical, the variance may be an ideal indicator, which can be written in the following form:

$$
R(t)=\frac{1}{N_t-1}\sum_{i=1}^N{[y_i(t)-\bar{y}(t)]^2}
$$

Where $N_t$ denotes the sample size of node $t$ and $y_i(t)$ is the output for the $i^{th}$ observation in node $t$. We also calculate the average for all outputs in node $t$, $\bar{y}(t)$.

In this way, the reduction of variance can be used to measure the decrease of impurity:

$$
\Delta R(t)=R(t)-\{\frac{N_r}{N}R(t_r)+\frac{N_l}{N}R(t_l)\}
$$

The interpretation here is similar to that for Gini coefficient.

## 4 Summary

We mainly introduce two measures for node impurity: the Gini coefficient and information entropy. In spite of different theoretical background, they still have something in common. In general, both of them try to maximize the expectation of impurity decrease. Equivalently, when we are applying one of these two measures, we actually want to find the best strategy that accounts for minimal bias.

## References

1. Freund, Yoav, and Llew Mason. "The alternating decision tree learning algorithm." *icml*. Vol. 99. 1999.
2. Friedl, Mark A., and Carla E. Brodley. "Decision tree classification of land cover from remotely sensed data." *Remote sensing of environment* 61.3 (1997): 399-409.
3. Gastwirth, Joseph L. "The estimation of the Lorenz curve and Gini index." *The review of economics and statistics* (1972): 306-316.
4. Knuth, Donald E., and Ronald W. Moore. "An analysis of alpha-beta pruning." *Artificial intelligence* 6.4 (1975): 293-326.
5. Kohavi, Ron. "Scaling up the accuracy of naive-bayes classifiers: A decision-tree hybrid." *Kdd*. Vol. 96. 1996.
6. Lerman, Robert I., and Shlomo Yitzhaki. "A note on the calculation and interpretation of the Gini index." *Economics Letters* 15.3-4 (1984): 363-368.
7. Quinlan, J. Ross. "Bagging, boosting, and C4. 5." *AAAI/IAAI, Vol. 1*. 1996.
8. Quinlan, J. Ross. "Induction of decision trees." *Machine learning* 1.1 (1986): 81-106.
9. Safavian, S. Rasoul, and David Landgrebe. "A survey of decision tree classifier methodology." *IEEE transactions on systems, man, and cybernetics* 21.3 (1991): 660-674.
10. Walke, Rainer. "Example For A Piecewise Constant Hazard Data Simulation in R." *Max Planck Institute for Demographic Research* (2010).
11. Wang, Guo-yin, Hong Yu, and D. C. Yang. "Decision table reduction based on conditional information entropy." *CHINESE JOURNAL OF COMPUTERS-CHINESE EDITION-*25.7 (2002): 759-766.
12. Xue, Wei. *Data Mining with R*. China Renmin University Press: 150-186.
13. Zhou, Zhihua. *Machine Learning*. Tsinghua University Press (2016): 73-95.

