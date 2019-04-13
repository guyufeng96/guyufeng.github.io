<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

*Yufeng Gu, Huajin Yu*

## Abstract

This paper extends the K-NN algorithm introduced in the class. The instructor has explained some basic ideas and steps to generate a K-NN method. here we aim to discuss this algorithm in detail, including its mathematical background, measures of distance, how to select $$K$$, and characteristic selection.

## 1 Introduction

The K-NN algorithm is regarded as a typical way of lazy learning. To start with, we shall recall that K-nearest neighbors algorithm is a nonparametric method used for classification and regression. A general procedure is shown as below:

1. Select $$K​$$ observations, $$(X_1, X_2, \cdots, X_K)​$$, that are similar (close) to $$X_0​$$. These observations are called neighbors of $$X_0​$$;
2. Calculate the mean (or weighted average, median) of the $$K​$$ neighbors' outputs, $$(y_1, y_2, \cdots, y_K)​$$. The mean, denoted as $$\hat{y}_0​$$, can be used as the predicted value for $$X_0​$$'s output $$y_0​$$.

In the two steps above, we only have to assume that $$\hat{y}_0$$ is a function of $$(y_1, y_2, \cdots, y_K)$$, i.e.
$$
\hat{y}_0=F(y_1, y_2, \cdots, y_K)
$$

Usually, the function $$F$$ is defined as:
$$
\hat{y}_0=\frac{1}{K}\sum_{X_i\in N_K(X_0)}{y_i}
$$

Where $$N_K(X_0)$$ denotes the set containing $$K$$ neighbors of $$X_0$$.

When we talk about K-NN, there always exist two key concerns:

1. How to measure the distance between $$X_0$$ and its neighbors;
2. How to determine the value of $$K$$.

This paper is organized as the following structure: chapter 2 provides several alternative measures of distance; chapter 3 discusses two ways of determining the value of $$K$$; chapter 4 gives a summary of what we have noticed.

## 2 Measure of Distance

This chapter mainly introduces five popular measurements for the distance in K-NN, including the Minkowski distance, Euclidean distance, Manhattan (absolute) distance, Chebychev distance and Cosine distance.

Here we make a simple definition. For two observed points $$x=(x_1, x_2, \cdots, x_k)​$$ and $$y=(y_1, y_2, \cdots, y_k)​$$, let $$x_i​$$ denotes the $$i^{th}​$$ observation for point $$x​$$, and $$y_i​$$ denotes the $$i^{th}​$$ observation for point $$y​$$.

### *2.1 Minkowski Distance*

The Minkowski distance is the $$k^{th}$$ root for the sum of the $$k^{th}$$ power of the difference between the absolute values of the $$p$$ observations of the two observations:
$$
MINKOWSKI(x,y)=\sqrt[k]{\sum_{i=1}^p|x_i-y_i|^k}
$$

### *2.2 Euclidean Distance*

The Euclidean distance is the square root of the sum of the squares of differences between the $$p$$ observations of the two observations:
$$
EUCLID(x,y)=\sqrt{\sum_{i=1}^p{(x_i-y_i)^2}}
$$

It's Intuitive that the Euclidean distance is a special case of Minkowski distance where $$k=2$$. In some cases, we assume that different variables have different weights in computing the distance. Then the modified distance formula is:
$$
EUCLID_{modified}(x,y)=\sqrt{\sum_{i=1}^p{w_{(i)}(x_i-y_i)^2}}
$$

Where $$w_{(i)}=\frac{FI_{(i)}}{\sum_{j=1}^p{FI_{(j)}}}$$ denotes the weight of $$i^{th}$$ variable, and $$FI_{(i)}$$ denotes the measure for significance of $$i^{th}$$ variable. If the input variable set contains $$p$$ variables, $$x_1, x_2, \cdots, x_p$$, we eliminate the $$i^{th}$$ variable and compute the classification error or predicting error for the other $$p-1$$ variables, denoted as $$e_i$$. In this way, the significance of the $$i^{th}$$ variable is defined as:
$$
FI_{(i)}=e_i+\frac{1}{p}
$$

It's intuitive that the larger weight $$w_{(i)}$$ correlates with larger significance. We can further transform the distance between $$X$$ and $$X_0$$ into the similarity using a function $$K(d)$$, which is also called the kernel function.

### *2.3 Manhattan Distance*

The Manhattan distance is another special case of Minkowski distance were $$k=1$$. Its mathematical expression is:
$$
CHEBYCHEV(x,y)=\sum_{i=1}^p{|x_i-y_i|}
$$

The difference between Euclidean distance and Manhattan distance is just like that between *L1* and *L2* function.

### *2.4 Cosine Distance*

The Cosine distance is different from the previous measuremnets. It measures the similarity of two variables' integral structure:
$$
COSINE(x,y)=\frac{\sum_{i=1}^p{(x_iy_i)^2}}{\sqrt{\sum_{i=1}^p{x_i^2}\sum_{i=1}^p{y_i^2}}}
$$

Generally speaking, larger Cosine distance represents higher structural similarity. It's worth noting that the variables with a larger magnitude make more contributions to the distance than those with smaller magnitude.

### *2.4 Comparison among Different Measurements*

There is no any strictly dominant or dominated measurement. In other words, the measurement you choose depends on your objectives and the properties of your data. For example, if your data has some outliers, it's better to use Manhattan rather than Euclidean. In other cases, however, if the observed points are very close to each other, a proper way is to apply the Euclidean measurement. We won't spend too mch time on this question.

## 3 How to Select an Appropriate $K$

In the previous chapter, we have discussed some ways to measure the distance in K-NN algorithm. Another problem that concerns us is that, how we can properly select the size of neighbors. i.e., we want to find some criteria that ensures the accuracy and efficiency of model fitting.

Consider a very simple situation, where the parameter $$K=1$$. It's also called 1-NN method. Since we only care about the single point that is closest to $$X_0$$, there exists $$\hat{y}_0=y_i$$. Cover and Hart (1967) evaluate the efficiency of 1-NN using the out-sample error. They assume a binary output, where $$y_0=1$$ or $$0$$. Through mathematical derivation using probability theory, they proposed the following equation:
$$
E_{out_1}=P(y=1|X)[1-P(y=1|X)]+P(y=0|X)[1-P(y=0|X)]=2P(y=1|X)[1-P(y=1|X)]
$$

Cover and Hart (1967) also compared the out-sample error of 1-NN with Naive Bayesian method. Recall that the predicting error of Naive Bayesian is:
$$
E_{out_2}=1-P(y=1|X)
$$

A significant finding is that, the out-sample error of 1-NN is smaller than twice of Naive Bayesian. Although the simple 1-NN has a relatively small error, it's strongly influenced by the differences bettwen neighbors, accounting for large variance and poor robustness. A feasible way is to increase the parameter $$K$$. However, when we select a larger $$K$$, we are actually faced with a tradeoff between the out-sample error and the robustness. In other words, small $$K$$ has an advantage on out-sample error, while large $$K$$ has better robustness. Hence, the parameter $$K$$ we choose represents our acceptable ceiling of out-sample error or floor of robustness.

In regression prediction, the mean square error (MSE) is often used as the out-sample error. The formula of MSE can be written as below:
$$
MSE=\frac{1}{n}\sum_{i=1}^n{(y_i-\hat{y}_i)^2}
$$

Where $$n$$ denotes the size of sample, $$y_i$$ is the $$i^{th}$$ observations and $$\hat{y}_i$$ is the prediction using K-NN. There are two widely used estimating methods: (1) hold out; (2) leave one out. In the rest of this chapter, we will discuss them respectively.

### *3.1 Hold Out*

One way to estimate the out-sample error is random dividing the dataset into two sets: a training dataset and a test dataset. The basic idea is that, we use the training data to fit the model, apply the fitted model to predicted the outputs of test data, and then compare them with real observations.

In practice, the hold out method can overcome the problem of underestimated predicting error. Although this method is in some way efficient, it can only be used when the sample size is large, because there is a tradeoff between fitting accuracy and estimating variance.

### *3.2 Leave One Out*

Another way is called leave one out. As the name suggests, we select one observation as test data, and then use the rest $$n-1$$ observations to fit the model, repeating $$n$$ times. Compared with the first method, leave one out has an advantage on model fitting accuracy for small sample size, and it provides a rather small variance of estimated out-sample error. However, this method also has some shortcomings. First, if the observvations are not evenly distributed among different classes, there will be many mistakes in predicting the classes with fewer observations. Besides, since the procedure is repeated $$n$$ times, the cost of computing is very large, especially for large sample.

## 4 Summary

In this paper, we mainly discuss some alternative ways to measure the distance in K-NN as well as two ideas about estimating the out-sample error. The key point of discussion is that, there is no such strictly dominant method for us to apply. Whenever we are doing a classification or regression study using K-NN, we should always think carefully about both our most concerned question and limitations of our dataset. A tradeoff between the out-sample error and robustness is necessary all the time.

## References

Altman, N. S. (1992). "An introduction to kernel and nearest-neighbor nonparametric regression". *The American Statistician*. 46 (3): 175-185.

Cover, T. and Hart, P. (1967). "Nearest Neighbor Pattern Classification". *IEEE Transactions on Information Theory*. 13: 21-27.

Hechenbichler, Klaus, and Klaus Schliep (2004). "Weighted k-Nearest-Neighbor Techniques and Ordinal Classification". *Discussion Paper Sfb*.

Xue, Wei (2018). *Data Mining Using R*. China Renmin University Press. 129-149.

Zhou, Zhihua (2016). *Machine Learning*. Tsinghua University Press. 225-226.
