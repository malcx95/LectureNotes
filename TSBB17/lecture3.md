# CNN introduction

Blablabla en massa saker du redan kan

## Linear regression

Mean squared error:

```
J(theta) = 1/2N * sum(h(xi) - yi)^2
```

Gradient descent:

```
theta <= theta - alpha*grad(J(theta))
```

Vectorized form with L2 loss:

```
theta <= theta - alpha/N * X^T(X*theta - y)
```

## Activation functions

In order to have a deep network, we need activation functions.
This is because if we don't, the entire network will be just a linear
function, and it would not make any sense to add more layers. All
layers could then be easily expressed with one layer. Also, 
the derivative of a linear function is constant, which would mean that
the gradient in the training would be constant, and not depend on the error.

### Sigmoid function

```
1/(1 + e^-x)
```

Advantages:

- Smooth gradient
- Steep around -2 and 2, bringing the Y values to either end of the curve
- Always between 0 and 1, won't "blow up" the activations

Drawbacks:

- Vanishing gradients

Tanh is also bounded and has stronger gradient around 0.
Also has vanishing gradient problem.

### ReLu

```
max(0, x)
```

Advantages:

- Less computationally expensive
- Sparse activations
- No vanishing gradients
- Biological plausability

Disadvantages:

- Dying gradients
- Not differentiable at 0


## CNN:s

Advantages of strides:

- Statistical efficiency
- Reduced memory requirements
- Handling inputs of varying size

