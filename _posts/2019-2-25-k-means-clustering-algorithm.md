---
title: K-Means clustering algorithm 
---

K-means clustering is an unsupervised machine learning technique to cluster data sets into specified number of clusters. It can be used in both classification and regression problems. This article is broadly divided into three subparts. Firstly, the problem statement, then the algorithm to solve it and analysis of different approaches, and lastly, the convergence of the algorithm. By convergence, we mean, the algorithm finally produces an optimal cluster after finite number of iterations.

### The k-means clustering problem:

We have n data points of a d-dimensional data. we need to divide these n points to k different clusters so that each cluster is as "tight" as possible. 

How do we define tightness of a cluster?

Generally, to measure the performance of any machine learning algorithm, we define an error function. Here, for k-means clustering, we have sum squared error (SSE) which is simply the sqaured sum of Euclidean distance of each point from it's cluster centroid.

The goal of the algorithm is to minimize the SSE.

Unfortunately, it turns out that, even for k = 2, finding an optimal cluster is NP-hard. 

NP-hardness (non-deterministic polynomial-time hardness) in computational complexity theory, is the defining property of a class of problems that are, informally, "atleast as hard as the hardest problems in NP".

But if we change our goal from optimal to finding a resonable clustering, it turns out that it can be done quite easily. The algorithm is an iterative one, which produces a local minima to the SSE.

### The k-means clustering algorithm:

The algorithm involves two tasks, first, initializing k cluster centroids, and update centroids with each iteration until convergence.

There are multiple ways of choosing the initial set of k clusters. 

1. **Forgy**: 
- In this technique, k random data points are choosen from the n data points and made as the initial centroid of the k clusters.
- For all data points, the distance to each centroid is calculated and the data point is assigned to the cluster having the nearest centroid. When there is a tie, random choice can be done.
- After each point is assigned to a cluster, new centroid is calculated.
- Steps 2 and 3 are repeated until convergence.


2. **K-means++** : 
- The difference here lies in the initiliazation of cluster centroids. The first centroid is choosen randomly. Then rest k-1 centroids are choosen iteratively one by one from the rest of the data points with a probability distribution. </br>
Probabilty = (squared distance from the nearest already choosen centroids) / (sum of squared distance from the nearest already choosen centroids for all points)
- Same as the first method until convergence.

Here is a performance comparison between two methods from my course work:

Dataset     |  Initialization | Average SSE  | Average Iterations
------------|-----------------|--------------|--------------------
   100.csv  |        forgy    |8472.63311469| 2.43
   100.csv  |        kmeans++ |8472.63311469| 2.0
  1000.csv  |        forgy    |21337462.2968| 3.28
  1000.csv  |        kmeans++ |19887301.0042| 3.16
 10000.csv  |        forgy    |168842238.612| 21.1
 10000.csv  |        kmeans++ |22323178.8625| 7.5

 Another possible way of calculating centroid can be, median instead of mean. Apparently, the k-medians method is more robust to outliers as compared to k-mean++. 

### Convergence of the algorithm:

Let's denote a clustering by the letter C, centroids with Z and iterations with t. Our goal is to prove that: 
</br>

> SSE(C[t+1], Z[t+1]) < SSE(C[t], Z[t]) -- equation(1)

Here, C[i] and Z[i] denotes ith clustering and set of centroids. SSE means, Sum Squared Error, the one discussed above.
We can prove this with two steps.

1. On a specific set centroids, we move to a new clustering when we can find atleast one such data point which is closer to a new cluster centroid than the assigned one. Hence,

> SSE(C[t+1], Z[t]) < SSE(C[t], Z[t]) -- equation(2)

2. For a set of points (cluster), SSE to the centroid is lowest as compared to any other point. Now, in a same clustering, as we are updating the centroid, it is obvious that new centroid gives lower SSE than the previous centroid. This follows for all the clusters in the clustering. Hence,

> SSE(C[t+1], Z[t+1]) < SSE(C[t+1], Z[t]) -- equation(3)

Combining equation 1 and 2, we get the equation 3 which proves the convergence of k-means clustering algorithm.

### Implementation:

The code for k-means clustering can be found [here](https://github.com/SiluPanda/k-means-clustering).
Thanks to our prof. [Mr. Shivaram Kalyanakrishnan](https://www.cse.iitb.ac.in/~shivaram/)















