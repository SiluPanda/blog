---
title: Regression analysis; Ridge and Lasso (incomplete...)
---

### What is regression analysis?
In the terms of statistical modeling, regression analysis refers to a technique of determining the relationship between variables. We consider two types of variables, dependent and independent. More specifically speaking, regression analysis deals with the behavoiur of a dependent variable w.r.t to an indepedent variable. Behaviour as in, how does it vary when an independent variable is changed keeping other independent variables constant.
<br>
oh jeez!(I am just too addicted to Rick and Morty) that is a whole lot of Mathematics.
<br>

We can understand this by the simplest example, linear regression. Let's Bob is a real estate person and he has set of house sizes and their corresponding prices. Now, a client wants a price quote for a house with the given size expectation. Bob goes to his friend Paige, who is a math geek. She takes the data of size and price and fits a straight line. Now she gives an estimate of price quote by looking at the graph. Bob got impressed and buys her a chocolate. Win-win for everyone.

#### Linear Regression:
<pre>
	Y = W * X <br>
</pre>
I guess, we are pretty much familier with this equation. This is the equation of a straight line. Here, W denotes the set of weights, and X denotes the data point which can be a vector, if we have more than one features. In the above example, we only had one feature, i.e size.
For the ease of the discussion (or maybe not :P), we will refer features as dimesions of the data point. If you are wondering, where is the constant/bias term in the equation, we can just increase our dimension by 1 and the corresponding weight will serve as the bias term.
<br>
For fitting a straight line, we minimize something called Sum Squared error (SSE). Let's our hypothesis is `h` .
Then sum squared error can be written as: <br>
<pre>
	SSE = sum(Y[i] - h(X[i])) <br>
</pre>
Where, Y[i] denotes the i'th actual output and h(X[i]) is our predicted output for i'th data point. <br>
Now, how do we traditionally minimize a function? <br>
By taking partial derivatives w.r.t to variables and equating them to zero, right? <br>
Similarly, here, we want to tune our weights. Let's inialize weights to something random, for example, all ones.
Next, take partial drivative with respect to all weights, let's say we get `delta[k]` for k'th weight. <br>
Now, update, the corresponding weight as:
<pre>
	W[k] = W[k] - alpha * delta[k] <br>
</pre>
Here, `alpha` is the learning rate, it is upon us to choose an optimal learning rate. Note, that a smaller aplha can result in longer training time, and a larger alpha may miss out the minima. <br>
We need to do the above step for every weights repeatedly for `max_interations` times. We can choose the maximum iteration or can define an convergence condition. <br>
Here, convergence means, we can stop updating weights, when we a very insignificant difference than the previous weights.







