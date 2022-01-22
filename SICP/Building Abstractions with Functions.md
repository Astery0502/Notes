# Chapter 1: Building Abstractions with Functions #
> Process oriented programming
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

2. General Functions: 
    - naming and functions allow us to abstract away a vast amount of complexity, the definition of the functions has been trivial.
    - Depending on the extreme general evaluation process that small components can be composed into complex processes.

the example shows an general iteration evaluation process.
```python
def iter_improve(test, update, guess=1):
    while not test(guess):
        guess = update(guess)
    return guess
```

3. Nested Functions: 

two problems exists for taking functions as arguments:  
    1. names of functions cluttering in the global environment.
    2. contained with particular function signatures, which is supposed to take particular arguments.

Use Nested Functions to wrap the procedure.

```python
def square_root(x):
    def update(guess):
        return (guess + x/guess)/2
    def test(guess):
        return approx_eq(square(guess), x)
    return iter_improve(test, update)
```

the transfer of an environment associated with a function to the local frame in which that function is evaluated.

lexical scope: the functions have access to the environment where they are defined, not they're called.  
- the names of the local function do not interface with names external to the function in which it is defined.
- A local function can access the environment of the enclosing function.

4. Functions as returned values

An important feature of lexically scoped programming language is that locally defined functions keep their associated environment when they are returned.

Function below keeps the associated environment created along with while being returned.

```python
def compose1(f,g):
    def h(x):
        return f(g(x))
    return h
```

input functions and output function.  
the "1" character means only one argument is taken and one result returned.

### Lambda Expressions ###

So far as to create functions, we need to name the function or the sub functions. But for the expression, there is no requirement to name the sub expressions and the full expression either. Similarily, we have **lambda** expressions to create function values on the fly. 

A lambda expression evaluates to the function that has a single return expression as its body. Assignments and control statements are not allowed.

For a substitution of taking functions as return:
```python
def compose1(f,g):
    return lambda x: f(g(x))

compose1 = lambda f,g: lambda x: f(g(x))
```

### Newton's method ###

Newton's method is a classic iterative approach to finding the arguments of a mathematical function that yield a return value of 0. 

```python
# the basic framework of the iteration process
def iter_improve(update, test, guess=1):
    while not test(guess):
        guess = update(guess)
    return guess

# a function evaluating to the derivative of a function at x
def approx_derivative(f, x, delta=1e-5):
    df = f(x+delta) - f(x)
    return df/dx

# update function component (also can be defined in the find_root() as nested functions)
def newton_update(f):
    def update(x):
        return x - f(x)/approx_derivative(f,x)
    return update

def find_root(f, initial_guess=10):
    def test(x):
        return approx_eq(f(x), 0)
    return iter_improve(newton_update(f), test, initial_guess)
```

### Abstractions and First-Class Functions ###

Identify the underlying abstractions inside our programs, to build upon them, and generize them to create more powerful abstractions.  
Also, choose appropriate abstraction levels for your project.

Elements with fewest restrictions are said to have first-class status:  
- They maybe bound to names.
- They maybe passed as arguments to functions.
- They maybe returned as results from functions.
- They maybe included in data structures.

Functions of python are almost full first-class.

### Function Decorators ###

```python
def trace(f1):
    def wrapped(x):
        print('->', f1, '(', x, ')')
        return f1(x)
    return wrapped

@trace
def triple(x):
    return 3 * x
```

the name triple is not bound to the function created below, but the returned function from trace() taking functions below as argument.  
useful for tracing the functions used, and which to call from command line.

## Statements ##

Compound Statements: can be decomposed into several clauses (a header and a suite of statements)  
Sequence: recursively defined, decomposed into the first element and the rest of the elements, the rest is itself a sequence of statements: the unity contains the first element and other elements serving as a unity.


