## An Iterative Approach 
![An iterative approach to training a model.](../figures/GradientDescentDiagram.svg)
## Gradient Descent 
Suppose we had the time and the computing resources to calculate the loss for all possible values of $w_1$. For the kind of regression problems we've been examining, the resulting plot of loss vs. $w_1$ will always be **convex**. In other words, the plot will always be bowl-shaped, kind of like this:
![Regression problems yield convex loss vs. weight plots.](../figures/convex.svg)
Convex problems have only one minimum; that is, only one place where the slope is exactly 0. That minimum is where the loss function converges.

The first stage in gradient descent is to pick a starting value (a starting point) for $w_1$. The gradient descent algorithm then calculates the **gradient** of the loss curve at the starting point. When there are multiple weights, the gradient is a vector of **partial derivatives** with respect to the weights.

Intuitively, a partial derivative tells you how much the function changes when you perturb one variable a bit.

#### Gradients
The gradient of a function, denoted as follows, is the vector of partial derivatives with respect to all of the independent variables:$$\nabla{f}$$
For instance, if:$$f(x,y)=e^{2y}\sin{(x)}$$
then:$$\nabla{f(x,y)}=(\frac{\delta{f}}{\delta{x}}(x,y),\frac{\delta{f}}{\delta{y}}(x,y))=(e^{2y}\cos{(x)},2e^{2y}\sin{x})$$
In machine learning, gradients are used in gradient descent. We often have a loss function of many variables that we are trying to minimize, and we try to do this by following the negative of the gradient of the function.

The gradient always points in the direction of steepest increase in the loss function. The gradient descent algorithm takes a step in the direction of the negative gradient in order to reduce loss as quickly as possible.
![A gradient step moves us to the next point on the loss curve.](../figures/GradientDescentGradientStep.svg)
The gradient vector has both a **direction** and a **magnitude**. The magnitude is the value of the gradient with specific feature values.
## Learning Rate 
Gradient descent algorithms multiply the gradient by a scalar known as the learning rate (also sometimes called step size) to determine the next point. For example, if the gradient magnitude is 2.5 and the learning rate is 0.01, then the gradient descent algorithm will pick the next point 0.025 away from the previous point. 

**Learning rate is a Hyperparameter.** Most machine learning programmers spend a fair amount of time tuning the learning rate.
The ideal learning rate in one-dimension is $\frac{1}{f(x)^{''}}$(the inverse of the second derivative of f(x) at x). 
The ideal learning rate for 2 or more dimensions is the inverse of the **Hessian** (matrix of second partial derivatives).
The story for general convex functions is more complex.
## Stochastic Gradient Descent
In gradient descent, a **batch** is the total number of examples you use to calculate the gradient in a single iteration.
By choosing examples at random from our data set, we could estimate (albeit, noisily) a big average from a much smaller one. Stochastic gradient descent (SGD) takes this idea to the extreme--it uses only a single example (a batch size of 1) per iteration. 
Mini-batch stochastic gradient descent (mini-batch SGD) is a compromise between full-batch iteration and SGD. A mini-batch is typically between 10 and 1,000 examples, chosen at random. Mini-batch SGD reduces the amount of noise in SGD but is still more efficient than full-batch.