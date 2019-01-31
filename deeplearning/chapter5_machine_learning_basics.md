# The Kernel Trick

The kernel trick consists of observing that many machine learning algorithms can be written in terms
of dot products between examples.

It can be shown, for instance, that the function used by the support vector machine can be re-written as
```
w^Tx + b = b + \sum_i alpha_i*x^Tx^(i)
```
where x^(i) is a training example and alpha is a vector of coefficients. We can now replace
x with a feature function phi(x), and the dot-product with `k(x, x^(i)) = phi(x)*phi(x^(i))` (the kernel).


