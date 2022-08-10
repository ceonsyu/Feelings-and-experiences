# Linear Regression
![Chirps per Minute vs. Temperature in Celsius](../figures/CricketPoints.svg)
![A linear relationship](../figures/CricketLine.svg)
The line does clearly show the relationship between chirps and temperature. Using the equation for a line, you could write down this relationship as follows:
$$y=mx+b$$
This is the most simple ML model.
By convention in machine learning, you'll write the equation for a model slightly differently:
$$y'=b+w_1x_1$$
where:
 $y'$ is the predicted label (a desired output).
 $b$ is the bias (the y-intercept), sometimes referred to as $w_0$.
 $w_1$ is the weight of feature 1. Weight is the same concept as the "slope" $m$ in the traditional equation of a line.
 $x_1$ is a feature (a known input).
# Training and Loss
- Training a model simply means learning (determining) good values for all the weights and the bias(`m` and `b` in equation above) from labeled examples. 
- In supervised learning, a machine learning algorithm builds a model by examining many examples and attempting to find a model that minimizes loss; 
- This process is called empirical risk minimization.
- Loss is a number indicating how bad the model's prediction was on a **single example**. 

The goal of training a model is to find a set of weights and biases that have low loss, on average, across all examples.

Squared loss: A loss function that would aggregate the individual losses in a meaningful fashion. The linear regression models use a loss function called squared loss (also known as **$L_2$ loss**). A simple square loss for a single example:
>the square of the difference between the label and the prediction:
>$=(observation-prediction(x))^2$
>$=(y-y')^2$

Mean square error (MSE) is the average squared loss per example over the whole dataset. To calculate MSE, sum up all the squared losses for individual examples and then divide by the number of examples:
$$MSE=\frac{1}{N}\sum_{(x,y)\in D}{(y-prediction(x))^2}$$
where:

 - $(x,y)$ is an example in which
   - $x$ is the set of features (for example, chirps/minute, age, gender) that the model uses to make predictions.
   - $y$ is the example's label (for example, temperature).
 - $prediction(x)$ is a function of the weights and bias in combination with the set of features $x$.
 - $D$ is a data set containing many labeled examples, which are $(x,y)$ pairs.
 - $N$ is the number of examples in $D$.


Although MSE is commonly-used in machine learning, it is neither the only practical loss function nor the best loss function for all circumstances.
