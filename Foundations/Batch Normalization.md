# Batch Normalization

## Why we need batch normalization?

In the training process of a neural network, the parameters of it are changing all the time, leading to the severe problem called **Internal Covariate Shift**. This phenomenon will give two problems which make training even harder:

1. every layer needs to adapt to a new input distribution.
2. it is likely to make $|x|$ increase, leading to a lower learning speed when we use sigmoid function. 

After using batch normalization for the activations for each layer, we can:

1. decrease the level of dependence between layers.
2. make it possible to use saturating nonlinear activation functions like sigmoid.
3. use a higher training rates.
4. skip Dropout for regularization.

## What is Batch Normalization?

In [Batch Normalization paper](https://arxiv.org/pdf/1502.03167.pdf), they applied the batch normalization to the input $x = Wu+b$ for the activation function for each layer. Although I think this does not make any sense, since it will change the distribution **after** the activation function, **before** the activation function is chosen for the rest of this article as stated in the original paper. 

### Train

![Batch normalization in training time](/media/wll/F2A46F30A46EF68F/Computer Science/机器学习/Paper and Fundamental Summary/Foundations/BN_train.png)  

Note:

* As mentioned in the paper, the above operations all work on the different dimensions respectively. Every dimension only take expectation for that dimension, and $\gamma$ and $\beta$ are also different for each dimension. 
* Why use mini-batch instead of the whole training dataset? Since when we train a neural network, it is reasonable for us to use mini-batch SGD. In every mini-batch, the network can only "see" the data in that mini-batch rather than the whole dataset. So for fully use the statistics of mini-batch, we use mini-batch samples for computing the expectation and the variance. 
* Why use $y = \gamma \hat{x}_{i} + \beta$? In Batch Normalization, we normalize every input for the activation function to $E[x] = 0, Var[x] = 1$. For some activation functions, such as sigmoid function, if the data are always in $(-1, 1)$, then they are located in the linear area of it, leading to the case that the entire neural network can only approximate the linear functions. Therefore, to solve this problem, we add **learnable** parameters $\gamma$ and $\beta$ to boost the representation ability of the neural network.
* Why use $\epsilon$ in the denominator of the third step? To avoid the numerical error which makes the denominator be zero. 

### Test

![Batch Normalization in test time](/media/wll/F2A46F30A46EF68F/Computer Science/机器学习/Paper and Fundamental Summary/Foundations/BN_test.png)

Note:

* In test time, since we do not have mini-batch, we use the moving average of the training expectation and variance to fix those in test time. The embodied formulas are in step 10.  

### Batch Normalization for CNN

For CNN, we do not apply the batch normalization to each activation, but to the whole feature map, which means we jointly normalize all the activations in a mini-batch over all locations. In Alg.1, $\mathcal{B}$ is the set of all values in a feature map across both the elements of a mini-batch and spatial locations. Therefore, if the feature map is of the size $p*q$, then we normalize every element in a feature map over $m'=|\mathcal{B}|=m*p*q$ elements from feature maps produced for this mini-batch. In addition, $\gamma$ and $\beta$ are for per feature map instead of per activation.  