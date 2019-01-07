# Introduction

# Computational models

## PRAM

The PRAM model is a MIMD-parallel computer model with an arbitrary number
of processors p. Each processor has it's own local memory (optional)
and all processors have access to a shared memory. There are no caches and
all processors run on the same clock, which means that a PRAM machine is
guaranteed by the hardware to be synchronized.

This model is overly simplified due to that memory in the real world
is not always accessible in one clock cycle it's natural synchronous 
execution is and unbounded number of processors is unrealistic.

It is however still useful, since it provides an upper bound on the
performance of a parallel algorithm on ideal hardware.

A parallel algorithm that does not scale under the PRAM model will not
scale well anywhere else!

There are several variants, like Exclusive Read, Exclusive Write PRAM
(EREW), as well as CREW and CRCW PRAM. The latter has several
subvariants to describe how write conflicts are solved.

## Circuit / DAG-model

Describes the order the tasks are performed by which processors in a
parallel algorithm. The task graph is a directed acyclic graph, 
where vertices are elementary tasks taking time unit 1, and the
directed edges describe dependencies.

The critical path is the longest path from an entry to an exit node,
and is the lower bound for the parallel time complexity. The actual
parallel time can be longer if the number of processors is limited.

# Analysis of data locality

If we say a variable v is live between the first and last time it's
accessed, then the working set of an algorithm A at time t (WSa(t))
is the set of all live variables at time A.

The worst case working set size (WSS) is the size of the set at the time
the most variables are live.

Rule of thumb: An algorithm has a good cache locality if
the WSS is less than 90% of the available space in the last-level cache,
assuming fully associative cache.

# Analysis of Parallel Algorithms

Parallel execution time denotes the time it takes between when the first
processor starts executing and when the last processor ends execution. 
The time T it takes for processor i to execute from start to end is 
composed of the computation time Tcomp, communication/synchronization
time Tcomm and idle time Tidle.

- Work: the total number of performed elementary operations.
- Cost: parallel execution time * number of processors
- Speed-up: the factor by which the program gets faster with p
    processors compared to using 1 processor.
- Parallel efficiency: Speed-up / number of processors.
- Throughput: number of operations finished per second.
- Scalability: does speedup keep growing well when the number of 
    processors gets large?

A parallel algorithm A is asymptotically work-optimal iff
```
w(p, n) = O(t_seq(n))
```

A parallel algorithm A is asymptotically cost-optimal iff
```
c(p, n) = O(t_seq(n))
```

## Brent's theorem

Any PRAM algorithm A which runs in `t_A(n)` time steps and performs
`w_A(n)` work can be implemented to run on a PRAM with p processors in
```
O(t_A(n) + w_A(n)/p)
```
time steps.

## Speedup

`T_s` = the time it takes to execute the best serial algorithm for P
        on one processor of the parallel machine

T(1) = time to execute parallel algorithm A on 1 processor.
T(p) = time to execute parallel algorithm A on p processors.

Absolute speedup `S_abs` = `T_s/T(p)`
Relative speedup `S_rel` = `T(1)/T(p)`

The absolute speedup is smaller than or equal to the relative speedup.

Trivially parallel problems, like matrix multiplication and ray tracing,
get an ideal speedup, that is, the relative speedup is equal 
to the number of processors added.

Algorithms with tree-like task graphs are sublinear, their speedup curves
eventually flatten out. (`S \in Theta(p/log(p))`)

When p grows very large all algorithms eventually saturate due to
communication and synchronization overhead, after which the speed
decreases with more processors.

### Amdahl's law

If a parallel algorithm A has a sequential part A^s, where only
one processor is active, and a parallel part A^p that can be
perfectly sped up by p processors. The total work is then
```
w_A(n) = w_A^s(n) + w_A^p(n)
```
and time `T = T_A^s + T_A^p/p`

Amdahl's law:

If A^s is a constant fraction beta of the total work, that is if
```
beta = w_A^s(n)/w_A(n) <= 1
```
is constant, then the relative speedup of A with p processors is limited by
```
S(p) = p/(beta*p + (1 - beta)) < 1/beta
```

Proof:

```
S_rel = T(1)/T(p) = T(1)/(T_A^s + T_A^p(p))
```

Since A^p can be perfectly parallelized:
```
T_A^p(p) = (1 - beta)T(1)/p
```

```
S_rel = T(1)/(beta*T(1) + (1 - beta)T(1)/p) = 1/(beta + (1-beta)/p)
    = p/(p*beta + (1-beta)) < 1/beta
```

# Further fundamental parallel algorithms

## The prefix-sums problem

Given a sequence of n items, and a binary associative operator (+), compute
the sequence `y_i = x_0 (+) x_1 (+) ... (+) x_i` for 0 <= i < n.

### Upper-lower parallel prefix

Split the array in two, `[x_0, x_1, ... x_ceil(n/2)-2]` and 
`[x_ceil(n/2)-1, ... x_n-1]`. Recursively compute the parallel prefix 
sum of the two halves in parallel, as they are independent. 
If there is only one element in the array, return just that element 
as the result. The upper half does not contain the sum of the bottom
half, so add the last element of the computed prefix sum for the bottom
half (`y_ceil(n/2)-2`) to all elements in the upper half in parallel.

The parallel time is theta(log(n)), it's work and parallel 
cost is in theta(nlog(n)).

It does not work with the EREW PRAM model, as it needs to concurrently
read the `y_ceil(n/2)-2` element.

### Recursive doubling parallel prefix

Start with a stride with 1. Repeat the following until the stride is
greater or equal to N. For all i in [stride, N-1] in parallel, add
the element at position i to the element at position i-stride. Double
the stride.

This algorithm works with EREW processors, as it never reads from the
same location concurrently. It performs log2(n) iterations with constant
work so the parallel time is in theta(log(n)) and work in theta(nlog(n)).
Thus, it's not work optimal either.

### Odd-Even

x1 -> y1, x1 + x2 -> y2; x3 -> y3, x3 + x4 -> y4 etc...
Recursive call on y2, y4, y6...
y2 -> y2, y2+y3 -> y3; y4 -> y4, y4+y5 -> y5 etc...

Base case if 4 inputs.

Works on EREW, 2log(n) - 2 time steps, 2n - logn - 2 work,
theta(nlog(n)) cost. If rescheduled using Brent's theorem it can be
cost optimal (theta(n)) if we use theta(n/log(n)) virtual processors.

## Parallel list ranking

Compute, for each element in a linked list, a pointer to the last
element in the linked list, as well as the distance to the last element.
Each thread starts at a list element.

Each element has a next pointer, a chum pointer and a length.

```

for k in [1..N] in parallel:
    chum[k] = next[k]
    length[k] = 1
    while chum[k] != end:
        chum[k] = chum[k]->chum
        length += chum[k]->length
```

