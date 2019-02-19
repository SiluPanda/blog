---
title: Ensemble learning, Bagging and Boosting
---

### What is ensemble learning?

Ensemble learning is a machine learning technique, where multiple hypotheses combined to give the final output. For example, for classifying red and green balls, instead of using one perceptron, we may use multiple weak perceptrons and combine their output. Let's say we have 5 perceptrons and three of them classified a point as green. Thus, there is a better chance of that point being actually green than a single perceptron classifying it as green. There are multiple ensembling algorithms. We will discuss about two of those in this article.

### 1. Bootstrap aggregating (Bagging)

This is the simplest ensemble algorithm. In Bagging, K number of weak hypothesis are trained randomly sampled data and simple voting is done among their output to get the final output for a data point. 
The Algorithm for Bagging is:

1. Choose a K for the number of weak hypotheses to train. We can validate over different values of K later to see the optimal value of K
2. For all K hypotheses, choose a random sampled data set from the traning data set and train the hypothesis.
The size of sampled data can be adjusted according to the performance.
3. For all data points in test data, find the prediction of all K hypotheses. 
4. Do a simple voting to get the majority among the ouput to give it the crown of the final output of that data point

### 2. Adaptive Boosting (AdaBoost)

In Boosting, we give weights to each data point while training. The weight is basically the probability of it getting picked up by the next hypothesis while training. When a point is mis-classified, the weight of that data point is increased, so that it gets picked by the next hypothesis. Also, every hypothesis is given a weight which is simply the effectiveness of that hypothesis. We can visualize this situation as, Let's say we have 5 Experts on a specific issue in a room and two of them perform very well than the other three. It is obvious that, we will tend to listen and give more emphasis to the better performing experts more than other three. That is what is implemented in AdaBoost where better performing models are given more weights so that the output of that hypothesis has a significant role in deciding the final output.
The Algorithm for AdaBoost is:

1. Choose a K for the number of weak hypotheses to train. We can validate over different values of K later to see the optimal value of K
2. Initialize a weight vector W for the traing data points. As we use these weights as probability values, Ideally initialize all values to (1 / length of weight vector), so that, all the elements sum to 1.
3. Initialize another vector Z and initialize all the elements to 0. This is the effectiveness of the hypotheses.
4. For all values of K, choose a random sample of data according the weight vector W from that training data set. The size of the sampled data can be adjusted according to the performance of the model. Initially something between 0.5-1.5 * size of training data is good. Train the hypothesis with the sampled data.
- Now for each training data point, match the output of the the hypothesis. If the point is mis-classified, increse the weight of that data point.
- Change the corresponding value of Z according to the performance of the hypothesis,
5. Now for each data point, return the weighted majority.

### Advantages over single hypothesis

The Ensemble learning gives better results than a single classifier because, let's say we have 5 perceptrons in an ensemble learning and P is the probability of a point being mis_classified by a single perceptron. For a data point to get mis-classified in ensemble, it has to be mis-classified by atleast 3 of the perceptrons, the probabability of which is, p1 * p2 * p3 . This is significantly lesser than P in most of the cases. This argues the better performance of ensemble over single hypothesis.

