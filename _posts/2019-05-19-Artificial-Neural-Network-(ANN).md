<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

<script type="text/x-mathjax-config">
 MathJax.Hub.Config({	
tex2jax: {inlineMath: [['$', '$']]},	
messageStyle: "none"	
});	
</script>
*Yufeng Gu & Huajin Yu, WISE*



## 1 Introduction

Artificial neural network(ANN) is a mathematical model or calculation model that mimics the structure and function of biological neural network. Neural networks are calculated by a large number of artificial neuronal connections. In most cases, the artificial neural network can change the internal structure on the basis of external information, which is an adaptive system. Modern neural network is a nonlinear statistical data modeling tool, which is often used to model complex relationships between input and output or to explore data.  

Neural network is an operation model, which is composed of a large number of nodes (or "neurons") and the connection between them. Each node represents a specific output function, called an incentive function, and the activation function. The connection between each two nodes represents a weighted value of the signal through the connection, which is equivalent to the memory of the artificial neural network. The output of the network varies according to the connection mode of the network, the weight value and the excitation function. And the network itself is usually an approach to an algorithm or function in nature, or it may be a logic. The expression of strategy.

Its construction concept is inspired by the operation of biological (human or other animal) neural network function. Artificial neural network is usually optimized by a learning method based on mathematical statistics, so artificial neural network is also a practical application of mathematical statistics method. Through the standard mathematical method of statistics, we can get a large number of local structural spaces that can be expressed by functions, on the other hand, in the field of artificial perception of artificial intelligence. We can make artificial perception decisions through the application of mathematical statistics (that is, through statistical methods, artificial neural networks can be similar to people. It has the same simple decision ability and simple judgment ability), and this method has more advantages than the formal logical reasoning calculus.

## 2 Perceptron 

Perceptual machines are a kind of artificial neurons. In many neural networks, the main neuron model is sigmoid neurons. But to know why sigmoid is defined like this, it takes us some time to understand the perceptual machine.

How does the perceptual machine work? A perceptual machine produces a binary output through some binary input x1, x2, and then produces a binary output:

![Figure1: Perceptron](/homework/6-1.jpg)



In the figure above, the perceptual machine has three inputs $x1, x2, x3$. usually it can have more or less input. Rosenblatt proposes a simple rule to calculate the output, which uses the weight $w1, w2...$ . To show the importance of each input to the output. The output of the neuron, either 0 or 1, is less than or greater than a certain threshold by the weight and the value of the $\sum_{j}w_jx_j$. Like the weight, the threshold is a real number, which is a parameter of the neuron. The expression in algebra is:

![Figure2: Perceptron](/homework/6-2.jpg)

The above is the working principle of perceptual machine.

Obviously, the human decision-making model is more than just perceptual machines. But this example shows how perceptual machines make decisions. It seems reasonable that a complex network of perceptors can make more accurate decisions:

![Figure3: Perceptron](/homework/6-3.jpg)

In this network, the first list of perceptors, known as layer 1 perceptors, are used to make three very simple decisions by weighing inputs. So what does the second floor perceptual machine do? Each of these sensors makes a decision by weighing the results of the first layer of output as input. In this way, the second layer of perceptual machines can make more complex and abstract decisions than the first layer. More complex decisions can be made at the third level. In this way, a first layer perceptual network can make very complex decisions.

## 3 Sigmoid Neuron

The learning algorithm looks very good. But how can we design such an algorithm for neural networks? Suppose we have a network of perceptors, and we want it to learn to solve some problems. For example, the input to the network may be the original scanned pixel data of a handwritten number. We want this network to learn a parameter and deviation that can identify the corresponding number. To understand how to learn, suppose we make some minor changes in the weight and deviation in the network. We want this small weight change to cause a change in the corresponding output in the network, a feature that makes learning possible. The following figure shows what we think Yes (this network is too simple to recognize handwritten numbers):

![Figure4: Perceptron](/homework/6-4.jpg)

If we know that adjusting the weight and deviation can cause a small change in the output, then we can modify the weight and deviation according to this fact, so that our network can do more in the way we want. For example, assuming that the network always classifies 9 as 8, we can find a way to make some small changes in the weight and deviation of the network, so that the network can divide the picture into 9. Then we do this again and again, changing the weight and deviation again and again, so that the output is getting better and better, and the network is learned.

The problem is that this doesn't happen when your network contains a perceptual machine. In fact, a small change on any perceptual machine can sometimes lead to the result of the perceptual flip (either flipped or unchanged), from 0 to 1 or the opposite. Such a reversal could cause a series of chain reactions, resulting in complex changes in all other perceptual machines. That is, when you may adjust the number 9 to be well recognized, the behavior of the network on other images has become completely uncontrollable. This makes it difficult for us to make the network closer to the desired behavior by debugging parameters and biases. Maybe there's some ingenuity. Method to solve this problem, but how to use a perceptual machine network learning is not so easy.

We can solve the above problem with a new artificial neuron-sigmoid neuron. Sigmoid neuron is very similar to perceptual neuron, but it can realize that when small changes are made to weight and deviation, the change of output is also small. This will make it possible for sigmoid neural networks to learn.

The sigmoid neurons are described below. We will describe the sigmoid neuron as we describe the perceptual machine:

![Figure1: Perceptron](/homework/6-1.jpg)

Like a perceptual machine, the sigmoid function has an input vector, but its input vector is no longer limited to 0 and 1, but a continuous value between 0 and 1. For example, 0.1314 can be used as the input value of sigmoid neurons. Similarly, sigmoid neurons have assigned weights and a total deviation for each input. But the output is no longer 0 and 1, but the output is $σ(wx)+b$, where $σ​$ is called the sigmoid function, which is defined as:

![Figure5: Perceptron](/homework/6-5.jpg)

One with input $x1, x2...$ Weight $w1, w2...$ . The output of the sigmoid neuron of the deviation b is:

![Figure6: Perceptron](/homework/6-6.jpg)

This formula is much more complicated than the formula of the perceptual machine. In fact, it is very similar to the perceptual machine. In order to reflect the similarity with the perceptual machine, suppose that$z=wx+b$ is a large positive number, then $e^{-z} \approx 0$, then $σ (z) \approx 1$. That is to say, when  $z=wx+b$ is a large positive number, the output of sigmoid neurons is close to 1, which is like a perceptual machine. On the contrary, the output of sigmoid tends to be close to 0 when $z=wx+b$ is a very small negative number. This is very similar to the behavior of perceptual machines. The output of sigmoid is not the same as that of the perceptual machine only when the value of $wx +b$ is not too small.

## References

1. CSDN. Neural network and deep learning. 
2. Simon S Haykin. "Neural Networks: A Comprehensive Foundation." (1994)
3. Christopher M Bishop. "Neural networks for pattern recognition." (1995)

