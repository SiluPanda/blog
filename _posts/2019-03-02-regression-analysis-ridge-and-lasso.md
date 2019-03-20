---
title: Regression analysis: Ridge and Lasso
---

## What is regression analysis?
In the terms of statistical modeling, regression analysis refers to a technique of determining the relationship between variables. We consider two types of variables, dependent and independent. More specifically speaking, regression analysis deals with the behavoiur of a dependent variable w.r.t to an indepedent variable. Behaviour as in, how does it vary when an independent variable is changed keeping other independent variables constant.
<br>
oh jeez!(I am just too addicted to Rick and Morty) that is a whole lot of Mathematics.
<br>

We can understand this by the simplest example, linear regression. Let's Bob is a real estate person and he has set of house sizes and their corresponding prices. Now, a client wants a price quote for a house with the given size expectation. Bob goes to his friend Paige, who is a math geek. She takes the data of size and price and fits a straight line. Now she gives an estimate of price quote by looking at the graph. Bob got impressed and buys her a chocolate. Win-win for everyone.

### Linear Regression:
<pre>
	Y = W * X <br>
</pre>
I guess, we are pretty much familier with this equation. This is the equation of a straight line. Here, W denotes the set of weights, and X denotes the data point which can be a vector, if we have more than one features. In the above example, we only had one feature, i.e size.
For the ease of the discussion (or maybe not :P), we will refer features as dimesions of the data point. If you are wondering, where is the constant/bias term in the equation, we can just increase our dimension by 1 and the corresponding weight will serve as the bias term.
<br>



