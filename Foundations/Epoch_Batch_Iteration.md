# The Difference between Epoch, Batch Size and Iteration

**Epoch:**  

In one epoch, we forward and backward pass the **entire** dataset **once**. 

**Why we need multiple epoch?** 

This is since there are a lot of parameters in a deep neural network which are learnable. However, we only have a dataset containing only a limited number of samples. Therefore, it is not enough for the whole neural network to find the optimal learnable parameter values if we only pass the entire dataset once. In other words, gradient descent can only extract the information included in the dataset step by step, so it needs multiple dataset pass to obtain all the information and fully train the whole neural network.

**Batch Size:**

We divide a entire dataset into several batches. In each batch, the number of the samples is the batch size.

**Why we need batch size?**

1. vs. gradient descent: We can divide the whole dataset into several mini-batch, which can decrease the number of samples processed at the same time, which saves the space of memory. In addition, we do not need to wait for the whole dataset being passed and update parameters, which is very slow.
2. vs. stochastic gradient descent: Stochastic gradient process one sample at the same time. It has two downsides: (1) too slow to converge and has a big proportion of noise, making the path to the local minimum very complicated. (2) cannot be implemented by the vectorization. Need a long time to iterate the  entire dataset. 

**Iteration:**

This concept is much easier than the aforementioned two. The number of the iteration is how many batches we need to complete one epoch. In other words, it is equal to the number of the data in the entire dataset / batch size.

