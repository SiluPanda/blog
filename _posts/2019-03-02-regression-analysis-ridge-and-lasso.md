---
title: Regression analysis; Ridge and Lasso (incomplete...)
---

### What is regression analysis?
In the terms of statistical modeling, regression analysis refers to a technique of determining the relationship between variables. We consider two types of variables, dependent and independent. More specifically speaking, regression analysis deals with the behavoiur of a dependent variable w.r.t to an indepedent variable. Behaviour as in, how does it vary when an independent variable is changed keeping other independent variables constant.
<br>
oh jeez!(I am just too addicted to Rick and Morty) that is a whole lot of Mathematics.
<br>

We can understand this by the simplest example, linear regression. Let's Bob is a real estate person and he has a set of house sizes and their corresponding prices. Now, a client wants a price quote for a house with the given size expectation. Bob goes to his friend Paige, who is a math geek. She takes the data of size and price and fits a straight line. Now she gives an estimate of price quote by looking at the graph. It impresses Bob and he buys her a chocolate. Win-win for everyone.

#### Linear Regression:
<pre>
	Y = W * X <br>
</pre>
I guess, we are pretty much familier with this equation. This is the equation of a straight line. Here, W denotes the set of weights, and X denotes the data point which can be a vector, if we have more than one features. In the above example, we only had one feature, i.e size.
For the ease of the discussion (or maybe not :P), we will refer features as dimesions of the data point. If you are wondering, where is the constant/bias term in the equation, we can just increase our dimension by 1 and the corresponding weight will serve as the bias term.
<br>
For fitting a straight line, we minimize something called Sum Squared error (SSE). Let's our hypothesis is `h` .
Then sum squared error can be written as: <br>

> SSE = sum((Y[i] - h(X[i])^2) <br>

Where, Y[i] denotes the i'th actual output and h(X[i]) is our predicted output for i'th data point. <br>
Now, how do we traditionally minimize a function? <br>
By taking partial derivatives w.r.t to variables and equating them to zero, right? <br>
Similarly, here, we want to tune our weights. Let's initialize weights to something random, for example, all ones.
Next, take the partial drivative with respect to all weights, let's say, we get `delta[k]` for k'th weight. <br>
Now, update, the corresponding weight as:

> W[k] = W[k] - alpha * delta[k] <br>

Here, `alpha` is the learning rate, it is on us to pick an optimal learning rate. Note that, a smaller alpha can result in longer training time, and a larger alpha may miss out the minima. <br>
We need to do the above step for every weights repeatedly for `max_interations` times. We can choose the maximum iteration or can define an convergence condition. <br>
Here, convergence means, we can stop updating weights, when we get a very insignificant difference than the previous weights.

### Ridge Regression:
Ridge regression is quite similar to the linear regression, but here, instead of minimizing the SSE, we introduce a newer function, called, loss fucntion and it is given by: <br>

> Loss = SSE + lambda (|W|^2)

<br>
Here, labmda is a constant and needs to be tuned with validation. The later can be called as a penalty term. This method is called as Regularization. It is used to control the complexity of the function and avoid overfitting.
Here is a code snippet for the gradient of the loss function:

<pre>

def grad_ridge(W, X, Y, _lambda):
	''' 
	W = weight vector [D X 1]
	X = input feature matrix [N X D]
	Y = output values [N X 1]
	_lambda = scalar parameter lambda
	Return the gradient of ridge objective function (||Y - X W||^2  + lambda*||w||^2 )
	'''
	X = X.astype(np.float32)
	Y = Y.astype(np.float32)
	W = W.astype(np.float32)
	D = W.shape[0]
	N = X.shape[0]
	grad_desc = (-2) * np.matmul(np.transpose(X), np.subtract(Y, np.matmul(X, W))) + 2 * _lambda * W
	return grad_desc
</pre>

We need to repeat this process for a certain number of times, oh, `max_iteration` again. Here is another code snippet doing that stuff.
 <br>
 <pre>
 	def ridge_grad_descent(X, Y, _lambda, max_iter=30000, lr=0.00001, epsilon = 1e-4):
	
	X 			= input feature matrix [N X D]
	Y 			= output values [N X 1]
	_lambda 	= scalar parameter lambda
	max_iter 	= maximum number of iterations of gradient descent to run in case of no convergence
	lr 			= learning rate
	epsilon 	= gradient norm below which we can say that the algorithm has converged 
	Return the trained weight vector [D X 1] after performing gradient descent using Ridge Loss Function 
	NOTE: You may precompure some values to make computation faster
	'''
	N = X.shape[0]
	D = X.shape[1]


	W = np.ones((D,1))
	def isconverged(W_prev, W_new, epsilon):
		for i in range(len(W_prev)):
			if abs(W_prev[i] - W_new[i]) > epsilon:
				return False

		return True

	for i in range(max_iter):
		
		W_old = W.copy()
		W -= lr * grad_ridge(W, X, Y, _lambda)
		if isconverged(W_old, W, epsilon) == True:
			return W
</pre>

### Lasso regression:
Lasso regression is too similar to ridge regression but the main difference lies in the loss function. The loss function for lasso is given by:

> Loss = SSE + lambda * | W |

The derivative of the loss function and updation of weights for lasso is a bit complex. I would give resources to that, if anyone wants dive deep into the Maths.

There is another regression called elastic net which combines the penalty of both lasso and ridge regression.

### Anlysis of the methods:
We can observe a fact that, Ridge can not zero out any weight where Lasso can. This is actually an advantage of Lasso because, it can remove the parameters which are not much relevent for the output. This actually makes our model more robust and needless to say, computationally, a little lighter. On the other hand, Ridge applies a heavy penalty over the weights by taking the squares.

### Sources for diving deep into this:

To get a basic visualization of the idea of the ridge regression, [this](https://www.youtube.com/watch?v=Q81RR3yKn30) youtube video is quite helpful and is of beginner level. [This](https://www.youtube.com/watch?v=NGf0voTMlcs) is a very nice video on Lasso and [this](https://www.youtube.com/watch?v=1dKRdX9bfIo&t=256s)
is for Elastic net.
<br>
[This](https://www.coursera.org/lecture/ml-regression/computing-the-gradient-of-the-ridge-objective-kvaqc) is a excellent video by University of Washington on coursera. I would highly recommend to watch [this](https://www.coursera.org/lecture/ml-regression/computing-the-gradient-of-the-ridge-objective-kvaqc) too, which dives deep into the derivation of gradient of Lasso regression.

### Implementation:
Checkout my implementation [here](https://github.com/SiluPanda/ridge-and-lasso-regression). If you have any question or just have something to say about the code, I would highly appreciate opening up an issue, so that we can discuss there.  













