# Information theory

We define the self-information of an event to be

```
I(x) = -log P(x=x)
```

This deals only with a single outcome. The __Shannon entropy__ quantifies the uncertainty in an entire probability
distribution:
```
H(x) = E_x~P{I(x)} = -E_x~P{log(P(x))}
```

If we have two separable probability distributions P(x) and Q(x) over the same random variable x, we can
define the __Kullback-Leibler (KL) divergence__ as a measure of how different these two distributions are:

```
D_KL(P||Q) = E_x~P{log(P(x)/Q(x))} = E_x~P{log(P(x)) - log(Q(x))}
```
If x is discrete, it's the extra amount of information needed to send a message containing symbols drawn from
P when using a code optimized for Q.
Properties:

- Non-negative
- 0 iff Q = P
- Not a true distance since `D_KL(P||Q) != D_KL(Q||P)`

A related quantity is the __cross-entropy__:
```
H(P, Q) = H(P) + D_KL(P||Q) = -E_x~P{log(Q(x))}
```
Minimizing this w.r.t. Q is the same as minimizing the KL divergence.

