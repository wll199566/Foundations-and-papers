# Non-trivial Details in papers

## Models

1. For the binary classification problem, if the number of the final output is one, then the activation function is sigmoid function, if it is two or more, then softmax function.
2. 

## Training

1. according to the [seq2seq paper](https://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf), reversing input sequence can generate better performance for NMT.
2. LSTM tend to not suffer from gradient vanish. For exploding gradient, we need to clip the gradient. There is a great [note](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/lecture_notes/cs224n-2017-notes5.pdf) from Stanford CS224N about how to solve exploding and vanishing gradient problem in RNN.  
3. To accelerate the training speed for RNN for NLP, it is important to make sure sentences in the same mini-batch to keep almost same. 

## Evaluation

1. Awesome and vivid [explanation](https://towardsdatascience.com/understanding-confusion-matrix-a9ad42dcfd62) of Confusion Matrix, which includes **recall** and **precision**.
2. AUC-ROC curve is always used to evaluate the performance of **classification** model. An awesome explanation can be found [here](https://www.dataschool.io/roc-curves-and-auc-explained/), and the recommended paper is [here](https://people.inf.elte.hu/kiss/13dwhdm/roc.pdf).