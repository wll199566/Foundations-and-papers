# Non-trivial Details in papers

## Input Data

1. For discrete data, we represent them as one-hot vector.

## Models

1. For the binary classification problem, if the number of the final output is one, then the activation function is sigmoid function, if it is two or more, then softmax function.
2. Effects of $1\times1$ conv layer: (1) reduce the depth (2) increase the non-linearity (3) change the spatial size using different strides (ResNet). 

## Training

### General

1. before training the network, weights initialization is very important, since it can avoid the instability of the gradient. About weight initialization, please refer to [this paper](http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf) by Y. Bengio and [this paper](https://arxiv.org/abs/1502.01852) by K. He. [Here](https://www.jefkine.com/deep/2016/08/08/initialization-of-deep-networks-case-of-rectifiers/) is an awesome blog about it.

### CNN

1. to reduce overfitting, first augment dataset.
2. when the network need to deal with different input size, then use Fully Convolutional layers. If we need to get the fixed size output, then we can make channel size as this fixed size, and compute the spatial average for each channel. (VGG) 
3. learning a residual function can accelerate the training convergence, which will reduce the training error (ResNet).

### RNN

1. according to the [seq2seq paper](https://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf), reversing input sequence can generate better performance for NMT.
2. LSTM tend to not suffer from gradient vanish. For exploding gradient, we need to clip the gradient. There is a great [note](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/lecture_notes/cs224n-2017-notes5.pdf) from Stanford CS224N about how to solve exploding and vanishing gradient problem in RNN.  
3. To accelerate the training speed for RNN for NLP, it is important to make sure sentences in the same mini-batch to keep almost same. 

## Evaluation

1. Awesome and vivid [explanation](https://towardsdatascience.com/understanding-confusion-matrix-a9ad42dcfd62) of Confusion Matrix, which includes **recall** and **precision**.
2. AUC-ROC curve is always used to evaluate the performance of **classification** model. An awesome explanation can be found [here](https://www.dataschool.io/roc-curves-and-auc-explained/), and the recommended paper is [here](https://people.inf.elte.hu/kiss/13dwhdm/roc.pdf).