# Cross Validation

## Why cross validation?

1. we need to use it to see whether the trained model is overfitting or underfittng to the unseen data.
2. we need to use it to tune our hyperparameters of the model, making it more accurate.
3. when the total training set is small, we use cross validation to make the validation result less noisy.

## What is cross validation?

Prior to what cross validation is, let's make clear first what training, validation, test dataset is.

1. training set: data that can be seen by the model.
2. validation set: split from the original training set, cannot seen in the process of training. The function of it is stated in the last section.
3. test set: used for test the performance of the trained model.

After figuring out the concepts of three sets, let's answer what the cross validation is.

For test the model before applied to the real test data, we need to prepare part of data to test it and tune the hyperparameters. For example, we can leave 1000 out of 50000 samples from training dataset for validation. However, since this method lead to the high error of the model, since reduced data will make the model not fully explore the pattern hidden behind the data. So what we do is the famous K-fold cross validation.

K-fold cross validation divide the whole training dataset into K fold, one of which is validation set and the remaining is the training set. Every time, we train our model on the training set, and then validate it on the validation set. Then after K iteration, we calculate the average validation error for some hyperparameter, then use the best one to tune the model.

## How to do cross validation?

1. split the whole **training** set into two equally K folds, use K-1 of it as the training set, and the one left as the validation set. The elements in the i-th validation set is $((x_{i1}, y_{i1}), \ldots, (x_{im_{i}}, y_{im_{i}}))$, where $i \in [1, K]$, and $m_{i}$ is the total number of samples in i-th validation set.

2. for each iteration i, train the model using the training dataset, apart from the i-th  validation ($i \in [1, K]$), and calculate the validation error on the dataset. $R_{i}(\theta) = \frac{1}{m_{i}} \sum_{1}^{m_{i}} L(h(x_{ij})-y_{ij})$.
3. after all K iterations, we can calculate the cross validation error. $R_{CV}(\theta) = \frac{1}{K}R_{i}(\theta)$.
4. According to the cross validation error for each value of some hyperparameter, we choose the one with the lower error rate, or the highest accuracy.