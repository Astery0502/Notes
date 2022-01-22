# Chapter 1: Building Abstractions with Functions #
> important points and tips while reading the chapter

## Basic Concepts ##

1. Statements and Expressions:
    - Statements carry out action: instruct computer to an action
    - Expressions carry out value: evaluation with operator and operand
2. Functions and Objects:
    - Functions encapsulate logic that manipulates data.
    - Object seamlessly bundles the together the data and the logic that manipulates data.
    - In a way, the function and Object are equalled to each other.
3. Guiding principles of debugging (interpret errors and diagnose the cause of unexpected errors)
    - Test incremently -- test the small component (code block) step by step, this also means you should manage your codes from separated pieces which implements individual applications into the final process meeting your need.
    - Isolate errors -- trace the error to the smallest component of the code. (pieceful coding as the first)
    - Check your assumptions -- verify your expections of the code is held.
    - Consult others -- your community never let you down!

4. Elements of Programming
    - primitive expressions and statements -- the simplest code blocks, reflecting the idea formation process of from many simple thoughts to the meaningful thinking.
    - means of combination -- by which elements are built from the simpler ones, the glue serves for the primitive ones and more complex ones.
    - means of abstraction -- by which elements are named and manipulated as units, reflecting the idea formation process of abstraction from the concrete objects.
    * another idea formation process: separated from multiple ideas; by comparing with other ideas; divide the complex idea into multiple parts.

## Functions ##

1. built-in data and functions are in the global frame of environment, always at the out of each local frame created by one function.
2. Nested function operations provides means of combining operations.
3. Binding names to values, functions and other objects provides a limited means of abstraction.

Once a *call expression* is evaluated:  
- First evaluate to the subexpression which can be found in the earliest frame which can be found.
- Apply the operator (often the user-defined call function) to the operand.
- Bind the operand values to the names of the function formal parameters in a new local frame.
- Evaluate the body of the function beginning from the local frame and last to the global frame.

Test:  
test each single unit function after it is implemented.

### The Art of the Function ###
1. how to efficiently take function as abstractions:
    - each function has exactly one job. 
    - don't repeat yourself, otherwise a function to be created can replace.
    - defined generally 
2. docstring: conventionally triple quoted; use help() to display
3. default function values: not provided with the call function but taken from the def statement defaults:
```
def(a,b,c=1)
function body 
return result
```

### Higher order functions ###

Functions manipulating functions:
1. Functions as arguments: take functions as the input part of the function integrating to express itself.

```python
# sum the kth term(k) with the k+1th = next(k)

def summation(n, term, next):
    total, k = 0, 1
    total, k = total+term(k), next(k)
```

2. 

## Statements ##

Compound Statements: can be decomposed into several clauses (a header and a suite of statements)  
Sequence: recursively defined, decomposed into the first element and the rest of the elements, the rest is itself a sequence of statements: the unity contains the first element and other elements serving as a unity.


