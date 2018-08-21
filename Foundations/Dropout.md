# Dropout

## Why dropout?

Dropout is one of the most important techniques in deep learning to do the regularization to avoid the overfitting problem.

## Motivation:

1. Model combination can always boost the performance of machine learning algorithms, like in VGG paper, they need several trained models to classify the final image.
2. The sexual reproduction process in the cell makes decreased-level co-adaptation, which is over asexual reproduction. 

## What is dropout?

### The Model

Let **y** be the output of some layer. Then, different from the traditional neural nets, we multiply **y** by **r** element-wise, where every element of **r** confirms to the **Bernoulli** distribution with the probability of p. In other words, every output of some layer can be retained with the probability of p. Apart from the Bernoulli distribution, we can also use **Gaussian** distribution noise, which adds $r_{i}*y_{i}$ to each $y_{i}$, where $r_{i}$ confirm to $\cal{N}(0, \sigma^{2})$ , or equivalently, the output is $r_{i}' * y_{i}$, where $r_{i}'$ confirms to $\cal{N}(1,\sigma^{2})$.

### How does dropout work?

#### Train time

In the training time, we use the aforementioned model, and use the dropout to every layer, sometimes include input layer, but not output layer. Since after dropout, there is only one "thinned" sub-network, the forward and backward propagation acts on this "thinned" sub-network. The gradients for each parameter are averaged over all the mini-batch training cases. 

#### Test time

In the test time, since we need the entire trained neural network to predict, classify or something else, we cannot use the dropout. However, to keep the expected value of each output stay the same, we need to multiply the outgoing weights of some neural by the probability p. Similarly, for Gaussian distribution, we need to multiply it by the  Gaussian variable.  

### The Relationship between $\sigma^{2}$ in Gaussian noise and the Bernoulli probability p?

The above model is equivalent to that we takes $r_{i}$ as 1/p with the probability of p and 0 elsewhere when the training time, and do not scale the weight as test time. Therefore, $E[r_{i}] = p*(1/p) = 1$ and $Var[r_{i}] = (1-p)/p$. For the Gaussian distribution, we set the variance $\sigma^2$ to be  $p(1-p)$, so for those two kinds of distributions, their expectation and variance are the same. Therefore, we can obtain the variance of the Gaussian noise $\sigma = \sqrt{\frac{1-p}{p}}$ .

### Dropout for CNN

According to the first [answer](https://www.reddit.com/r/MachineLearning/comments/42nnpe/why_do_i_never_see_dropout_applied_in/) of this page, we do not always use dropout for the convolution layers. It will slow down the training speed but not prevent co-adaptation. 

## How to Understand Dropout?

1. When eliminate the co-adaptations, the neighbor neurons becomes unreliable, so the "thinned" neural network should learn more **robust** features, which will benefit the result. 
2. Dropout can be seen as a way of **regularizing** a neural network by adding **noise** to its hidden units, as said in [the dropout paper](http://jmlr.org/papers/volume15/srivastava14a.old/srivastava14a.pdf). To see this, just like we add Gaussian noise, we can add $-y_{i}$ to the output of each layer with probability of p, which can be treated as the addictive Bernoulli(p) noise.  

## Extra Techniques

In [the dropout paper](http://jmlr.org/papers/volume15/srivastava14a.old/srivastava14a.pdf),  it mentioned two more techniques, one of which is **_max-norm constraint_ ** and the other one is **_unsupervised pre-training_**. 

1. Max-norm: since the large momentum and learning rate we use in training a dropout neural network, the weights of it are always very large, so we need to regularize the weights. Max-norm is $||w||<c$, where c is a hyper-parameter, which typically ranges form 3 to 4.
2. Unsupervised pre-training: to be simple, unsupervised pre-training can help initialize the weights, which will benefit the later gradient search process. It turns out that using unsupervised pre-training is better than only using random initialized parameters. See [this page](https://www.quora.com/What-is-unsupervised-pre-training) and  [this page](https://www.quora.com/Why-does-unsupervised-pre-training-help-deep-learning) for the details.

## Practical Guide Given by the Dropout Paper

1. Network Size: if an n-sized layer is optimal for a standard neural net on any given task, a good dropout net should have at least $\frac{n}{p}$ units.
2. Learning Rate and Momentum: to make up for the fact that a lot of gradients tend to cancel each other due to the noise introduced by dropout, a dropout net should typically use 10-100 times the learning rate that was optimal for a standard neural net. Also, we need to use a high momentum, whose value is around 0.95 to 0.99.
3. Dropout rate: typical values of the probability p for _hidden_ units are in the range 0.5 to 0.8. For real-valued _input_ units, a typical value is 0.8.



​      

 