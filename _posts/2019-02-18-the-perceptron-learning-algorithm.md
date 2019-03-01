---
title: The Perceptron Learning Algorithm
---

### What is a Perceptron?
The Perceptron is a parameterised function which takes a real-valed vector as input and gives a Boolean output. It was introduced by Rosenblatt over half a century ago.
The output of the perceptron is given by thresholding a linear function of the input vector. The parameters are the coefficients of the linear function. 
                               
Let's say the vector of weights is W, and and d-dimensional data point is X, then the output of a perceptron can be described as:
							
y = sign(W.X)

where for P in set of real numbers, sign(P) = 1 if P >= 0
																sign(P) = 0 if P < 0

Sometimes, bias term is added and the output is given by y = sign(W.X + b), but the bias term can also be implemented by adding another dimension, i.e d+1 dimensions.

The perceptron can also be visualized as a single layer neural network, where the features are the neurons and the input vector W is the weight.

### Algorithm
>k ← 1; w[k] ← 0.
>While there exists i ∈ {1, 2, . . . , n} such that y[i](w[k]·x[i] ) ≤ 0:
>	Pick an arbitrary j ∈ {1, 2, . . . , n} such that y j (w k · x j ) ≤ 0.
>		w[k+1] ← w[k]+ y[j] x[j].
>		k ← k + 1
>Return w[k] 

The algorithm initially maintains a weight vector which is initailized to 0. If the weight vector already separates the different classes, all good, we are done. Else, it picks a arbitary misclassified point and updates the weight vector accordingly.

## Code

The complete implementation of perceptron can be found at <https://github.com/SiluPanda/perceptron-classifier>

## Credits and References

Thanks to prof. Shivaram Kalyanakrishnan. <https://www.cse.iitb.ac.in/~shivaram>


