# Objects #

## Intro ##

### Object Metaphor ###

Objects represent information, but also behave like the abstract concepts they represent including the logic manipulating the data.  

Objects are both information and processes, bundled together to represent the properties, interactions, and behaviors of complex things.  

Individual things of class is called an instance of the class, and they can be constructed by calling the class as a function on arguments that characterize the instance.  

Objects characteristics:
- attributes: which are named values that are part of object.
- methods: function-valued attributes, methods compute their results from both the arguments and object. Data specified logic is applied with the method to yield the result.

### Native Data Types ###

Most of the objects are defined by the means of combination and abstraction.

Properties of Native Data Types:  
- There are primitive expressions that evaluate to objects of these types, called literals. -- for the data 
- There are built-in functions, operators, and methods to manipulate these objects.  -- for the process

## Data Abstraction ##

Compound data: bundle together the multiple datas into one concept correlated with the fact and the way we manipulate.

Isolating the programs that how datas are represented from the programs that how those datas are manipulated.  

Compared with function abstraction: separate the way how functions are used from how they are implemented.

Data abstraction is a methodology that enable us to isolate how a compound data is used from the details of how it is constructed.  

When creating an object, make as few auumptions as possible. A concrete data representation is defined, independent of the program about to use it. The interface between the two sections of system will be set of functions, called **selectors and constructers**, that implement the abstract data in terms of the concrete representation.

### Tuples ###

With constructor "make_rat" and selectors "numer', "denom", and some other behavior conditions, we obtain the concrete representation of the "rat" object.

### Abstraction Barriers ###

At each level, the barrier separates the functions (above) use the data abstraction and the functions (below) implement the data abstractions.

The functions in the box between the barriers enforces the abstraction barriers because they are the only functions that depend on both the representation above them (by their use) and the impletation below them (by their definitions). In this way, abstraction barriers are expressed as sets of functions.

### The Properties of Data ###

An abstract data type is constructed of some collections of construnctors and selectors, along with some behavior conditions.

```python
# one way to implement tuples with functions to behave like the index properties
def make_pair(x,y):
    """ Returns a value that behaves like pairs"""
    def dispatch(m):
        if m == 0:
            return x
        elif m == 1:
            return y
        return dispatch
def getitem_pair(p,i):
    """ Return the ith value of pair p"""
    return p(i)
```
The functional representation, although obscure, fufills the only conditions to fufill.

## Sequences ##

A sequence, unlike pairs, have an arbitrary (but finite) number of ordered elements.


A sequence is not a particular data type, but instead a collection of behaviors that different types share. There are many types of sequences and they share the certain properties.  
The properties of sequences:
- **Length** A sequence has a finite length.
- **Element selection** A sequence has an element corresponding to any non-negative integar index less than its length, starting at 0 for the first element.

The sequences is a collection of behaviors that does not fully specify an object (i.e., with constructors and selectors), but may shared within many types.  
Sequences provide a abstraction layers hide the details of exactly which type of sequence is being manipulated by a particular program.


