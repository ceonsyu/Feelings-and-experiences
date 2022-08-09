## Key ML Terminology
### supervised machine learning
ML system learn how to combine input to produce useful predictions on never-before-seen data.
### Labels
A label is the thing we're predicting-the `y` variable in simple linear regression. The label could be the future price of wheat, the kind of animal shown in picture, the meaning of an audio clip, or just about anything.
### Features
A feature is an input variable-the `x` variable in simple linear regression. A simple machine learning project might use a single feature, while a more sophisticated machine learning project could use millions of features, specified as:
$$x_1,x_2,\ldots,x_N $$
### Examples
An example is a particular instance of data, **x**(We put x in boldface to indicate that it is a vector). We break examples into two categories:
* labeled examples
* unlabeled examples 

A labeled example includes both features and the label. Use labeled examples to train the model. An unlabeled example contains features but not the label.
### Models
A model defines the relationship between features and label. Let's highlight two phases of a model's life:
- **Training** means creating or **learning** the model. That is, you show the model labeled examples and enable the model to gradually learn the relationship between features and label.
- **Inference** means applying the trained model to unlabeled examples. That is, you use the trained model to make useful predictions(`y`). 
### Regression vs. classification
A **regression** model predicts continuous values. For example, regression models make predictions that answer questions like the following:
- What is the value of a house in Beijing?
- What is the probability that a user will click on this ad?

A **classification** model predicts discrete values. For example, classification models make predictions that answer questions like the following:
- Is a given email message spam or not spam?
- Is this an image of a dog, a cat, or a hamster?