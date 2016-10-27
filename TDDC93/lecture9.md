# Testing

## Validation vs Verification

Validation - are we building the right system?

Verification - are we building the system right?

## Software testing

Software testing is an activity in which a program is executed under
specified conditions, the results are observed, and an evaluation
is made of the program.

## Basic definitions

- __Error__: People make errors, a good synonym is mistake. Errors tend to propagate, 
that is, a requirement error may be magnified during design and amplified even
more during coding.

- __Fault__: The result, or more precisely, the representation of an error. A good synonym is
defect or bug. A fault of _commission_ occurs when we fail to enter correct information. 
Faults of _ommission_ occur when we fail to enter correct information. Faults of omission
are more difficult to detect and resolve.

- __Failure (anomaly)__: Occurs when a fault executes. A failure defined this way
only occcur in an executable representation, and only relates to faults of commission.

## Who should do the testing?

- __Independent tester__: Must learn about the system, but will attempt to break it and
is driven by quality.

- __Developer__: Understands the system, but might test it more gently, and is driven
by delivery.

## Types of faults

- __Algorithmic__: divide by zero

- __Computation and Precision__: order of operations

- __Documentation__

- __Stress/Overload__: data-structure size

- __Capacity/Boundary__

- __Timing/Coordination__

- __Throughout/Performance__

- __Recovery__

- __Hardware and System Software__

- __Standards and Procedure__

## Blackbox/closed box testing

Testing only on specification.

### Exhaustive testing

Testing with every member of the input value space - the set of all possible input
values to the program.

### Equivalence class testing

A technique used to reduce the number of test cases while still maintaining a 
reasonable coverage. The input space is divided into equivalence classes, where all
members of each class are should be equivalently handled by the program.


