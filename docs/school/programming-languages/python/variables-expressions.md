---
tags:
  - PYTHON
---

# Python section 2.1 Variables and Expressions

You used that box to remember the number of people as you proceeded through each step. Likewise, a program uses a _variable_ to remember values as the program executes instructions. (By the way, the real riddle's ending question is actually "What is the bus driver's name?"— the subject usually says "How should I know?". The riddler then says "I said, YOU are driving a bus.")

> A **variable** is used to remember a value for later use. The statement `age = 15` defines a variable named age, which the interpreter uses to refer to a new object with integer value 15. When a statement executes that assigns a value to an existing variable, the interpreter updates the variable to refer to the newly assigned object. Likewise, reading a variable's value reads the value of the object referred to by the variable

## Objects

```python
Each Python object has three defining properties: value, type, and identity.

1. Value: A value such as "20", "abcdef", or 55.
2. Type: The type of the object, such as integer or string.
3. Identity: A unique identifier that describes the object.

The _value_ of an object is the data associated with the object. For example, evaluating the expression 2 + 2 creates a new object whose value is 4. The value of an object can generally be examined by printing that object.

The _type_ of an object determines the object's supported behavior. For example, integers can be added and multiplied, while strings can be appended with additional text or concatenated together. An object's type never changes once created. The built-in function type() prints the type of an object. The type of an object also determines the mutability of an object. **Mutability** indicates whether the object's value is allowed to change, and is explored in another section.

The _identity_ of an object is a unique numeric identifier, such as 1, 500, or 505534. Only one object at any time may have a particular identifier. The identity normally refers to the memory address where the object is stored. Python provides a built-in function id() that gives the value of an object's identity.
```

## Names

A programmer gives `names` to various items, such as variables (and also functions, described later). For example, `x = 5` uses the name "x" to refer to the value 5. A `name`, also called an `identifier`, is a sequence of letters `(a-z, A-Z, _)` and digits `(0-9)`, and must start with a letter. Note that `_` , called an `underscore`, is considered to be a letter.

Upper and lower case letters differ, i.e., Python is case sensitive, so "cat" and "Cat" are different. The following are valid names: c, cat, Cat, n1m1, short1, and _hello. The following are invalid names: 42c (doesn't start with a letter), hi there (has a space), and cat$ (has a symbol other than a letter or digit).

Names that start and end with double underscores (for example, **init**) are allowed but should be avoided, because Python has special usages for double underscore names, explained elsewhere. A good variable name should describe the purpose of the variable, such as "temperature" or "age", rather than just "t" or "A".

Certain words, like "and" or "True" can not be used as names. Those words are part of the language and are called reserved words and thus cannot be used as a programmer-defined name. Reserved words are also known as keywords. Many language editors will automatically color a program's reserved words. A list of reserved words appears at the end of this section.

A good practice when naming variables is to use all lowercase letters and to place underscores between words. This lowercase and underscore convention for naming variables originates from the Python style guide, [PEP 8](http://www.python.org/dev/peps/pep-0008/#descriptive-naming-styles).
PEP 8 (PEP is an acronym for Python Enhancement Proposal) is a document that outlines the basics of how to write Python code neatly and consistently. Code is read more often than written, so having a consistent variable naming scheme helps to ensure that programmers can understand each others' code.

Programmers should create meaningful names that describe an item's purpose. If a variable will store a person's age, then a name like "age" is better than "a". A good practice when dealing with scientific or engineering names is to append the unit of measure, for example instead of temperature, use temperature_celsius. Abbreviations should only be used if widely understandable, as in tv_model or ios_app. While meaningful names are important, very long variable names, such as "average_age_of_a_UCLA_graduate_student," can make subsequent statements too long and thus hard to read, so programmers find a balance between meaningful names and short names. Below are some examples of names that perhaps are less meaningful and more meaningful.

| Purpose                                                      | Less meaningful names | More meaningful names   |
| ------------------------------------------------------------ | --------------------- | ----------------------- |
| The number of students attending UCLA                        | ucla, num, nu         | num_students_UCLA       |
| The size of a television set measured as its diagonal length | sz_tv, size           | diagonal_tv_size_inches |
| The word for the ratio of a circle's circumference/diameter  | p                     | pi                      |
| The number of jelly beans in a jar, as guessed by a user     | guess, num, njb       | num_guessed_jelly_beans |
|                                                              |                       | user_guess_jelly_beans                        |

## Numeric types: Floating-point

In addition to storing integer numbers, variables are sometimes used to store floating-point numbers like -1.05 or +6.02x1023. Thus, an additional data type exists for floating-point numbers known as float.

A floating-point literal is written with the fractional part even if that fraction is 0, as in 1.0, 0.0, or 99.0.

When doing floating-point calculations, the programmer should be aware of the difference between integer constants and floating-point literals. 500 will be represented as an integer in memory (e.g., using an int type), whereas 500.0 will be represented as a floating-point number (using a float type).

Scientific notation is useful for representing floating-point numbers that are much greater than or much less than 0, such as 6.02x1023. A floating-point literal using scientific notation is written using an e preceding the power-of-10 exponent, as in 6.02e23 to represent 6.02x1023. The e stands for exponent. Likewise, 0.001 is 1x10-3 so can be written as 1.0e-3.

![[Pasted image 20230207152124.png]]

Float type objects have a limited range of values that can be represented. For a standard 32-bit installation of Python, the maximum floating point value is approximately 1.8x10308, and the minimum floating point value is 2.3x10-308. Assigning a floating point value outside of this range generates an _OverflowError_. _Overflow_ occurs when a value is too large to be stored in the memory allocated by the interpreter. For example, the below program tries to store the value 2.01024, which causes an overflow error.

---

In general, floating-point types should be used to represent quantities that are measured, such as distances, temperatures, volumes, weights, etc., whereas integer types should be used to represent quantities that are counted, such as numbers of cars, students, cities, hours, minutes, etc.

### Chaz notes from discord

```py
`import math` means `hey Python give this program access to the stuff from this module called 'math'
```

1. implicit vs explicit:

    ```py
    >>> import math
    >>> foo = math.pi
    ```

    `foo` is now a float containing pi:

    ```py
    >>> type(foo)
    <class 'float'>
    ```

    which we can let python implicitly convert to a string:

    ```py
    >>> print(foo)
    3.141592653589793
    ```

    Maybe we don't want all those decimals, though, so we can explicitly convert it to a string with some formatting:

    ```py
    >>> bar = f"{foo:6.4f}"
    >>> type(bar)
    <class 'str'>
    >>> print(bar)
    '3.1416'
    ```

    Or maybe more decimals:

    ```py
    >>> baz = f"{foo:30.28f}"
    >>> print(baz)
    '3.1415926535897931159979634685'
    ```

    (edited)

2.  

Or the same sort of thing with int to float and so forth as shown in that link above.

This is fine in Python:

```py
foo = "Bing"
foo = 12
foo = 123.456
foo = ['an', 'array', 'of', 'strings']
foo = {'bing': 'bang', 'boing': 12}
```

`foo` is just whatever you put in it. It has no type. As opposed to a statically typed language like Java where you'd write:

```py
String foo = "Bing"
```

And an attempt to set it to 12 would cause an error since foo can only ever hold a string.

1. Difference is basically:
2. Implicit: "Hey Python go ahead and convert this thing to a string however you see fit" - probably fine for simple cases.
3. Explicit: "I have special requirements or guardrails I need to implement so I need to manage converting this thing into a string." OR "I need to do this manually since it can't be implicitly converted"

link to helpful python stuff: [Yonder](https://www.geeksforgeeks.org/type-casting-in-python-implicit-and-explicit-with-examples/)
