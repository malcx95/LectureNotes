
# Cost functions

The gradient of the cost function must be large and predictable enough to serve as a good guide for the
learning. This means the function shouldn't saturate, as the gradients then become small. 
Output units tend to have exponential functions, which saturate when the input gets very negative.
The negative log-likelihood function solves this problem for many models, as the log undoes the exponentiation.

Mean square error and mean absolute error cost functions often lead to poor results with gradient-based,
optimization. Saturating output units combined with these functions tend to produce small gradients.
Cross-entropy cost function is therefore more popular.

# Output units

## Linear units for Gaussian output distributions

Affine transformation with no non-linearity.
```
\hat{y} = W^Th + b
```
Are often used to produce the mean of a conditional Gaussian distribution. Maximizing
the log-likelihood then becomes equivalent to minimizing the mean squared error.

+ May be used with a variety of optimization algorithms
+ Does not saturate

## Sigmoid units for Bernoulli output distributions

Used to produce a probability for a binary value being = 1.
```
\hat{y} = sigma(w^Th + b)
```
It's natural to use this in maximum likelihood learning, as the log in the cost function
undoes the exponentiation of the sigmoid. The resulting cost function is a softplus function,
which saturates only when the model already produces the correct answer.

## Softmax units for Multinoulli output distributions

Typically used for classification, to represent the probability distribution over n different classes.

```
z = W^Th + b
softmax(z)_i = exp(z_i) / sum_j{exp(z_j)}
```

This function is also suitable in maximum log-likelihood training, but can saturate in combination with
cost functions without a log to undo the exponentiation.

# Hidden units

ReLU:s are a good default activation function to use, as they don't saturate for positive input values,
and thus give a strong gradient. It's not differentiable at 0, but this is usually not a problem.
There are variations of ReLU to fix the zero gradients for negative inputs, such as a leaky ReLU,
absolute value rectification (useful when polarity of an image can change) or a parametric ReLU with
learnable slope on the negative side. It's good to initialize the biases input to the ReLU:s to a small
positive number, like 0.1, to make sure all neurons are activated from the start.



