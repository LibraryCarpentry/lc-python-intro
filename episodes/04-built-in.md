---
title: Built-in Functions and Help
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose of functions.
- Correctly call built-in Python functions.
- Correctly nest calls to built-in functions.
- Use help to display documentation for built-in functions.
- Correctly describe situations in which SyntaxError and NameError occur.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I use built-in functions?
- How can I find out what they do?
- What kind of errors can occur in programs?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use comments to add documentation to programs.

It's helpful to add comments to our code so that our collaborators (and our future selves) will be able to understand what particular pieces of code are meant to accomplish or how they work

```python
# This sentence isn't executed by Python.
name = 'Library Carpentry'   # Neither is this comment
# Anything after '#' is ignored.
```

## A function may take zero or more arguments.

We have seen some functions such as `print()` and `len()` already but let's take a closer look at their structure. 

An *argument* is a value passed into a function. Any arguments you want to pass into a function must go into the `()`

```python
print("I am an argument and must go here.")
print()
print("Sometimes you don't need to pass an argument.")
```

```output
I am an argument and must go here.

Sometimes you don't need to pass an argument.
```
You always need to use parentheses at the end of a function, because this tells Python you are calling a function. Leave the parentheses empty if you don't want or need to pass any arguments.


## Commonly-used built-in functions include `max`, `min`, and `round`.

- Use `max()` to find the largest value of one or more values.
- Use `min()` to find the smallest.
- Both work on character strings as well as numbers.
  - "Larger" and "smaller" use (0-9, A-Z, a-z) to compare letters.
  - This means that:
    - `'a'` is smaller than `'b'`
    - `'A'` is smaller than `'a'`
    - `'0'` is smaller than `'a'`
  - This is useful for ordering alphabetically.

```python
print(max(1, 2, 3))
print(min('a', 'b', 'c'))
print(min('a', 'A'))
```

```output
3
a
A
```

## Functions may only work for certain (combinations of) arguments.

`max()` and `min()` must be given at least one argument and they must be given things that can meaningfully be compared.

```python
print(max(1, 'a'))
```

```error
TypeError: unorderable types: str() > int()
```

## Functions may have default values for some arguments.

`round()` will round off a floating-point number. By default, it will round to zero decimal places.

```python
round(3.712)
```

```output
4
```

But we cab use a second argument (or parameter) to specify the number of decimal places we want.

```python
round(3.712, 1)
```

```output
3.7
```

## Use the built-in function `help` to get help for a function.

Every built-in function has online documentation. You can access the documentation using the `help()` function or by adding a `?` at the end of your function name in Jupyter.

```python
help(round)
```

```python
round?
```

```output
Help on built-in function round in module builtins:

round(...)
    round(number[, ndigits]) -> number

    Round a number to a given precision in decimal digits (default 0 digits).
    This returns an int when called with one argument, otherwise the
    same type as the number. ndigits may be negative.
```

## Python reports a syntax error when Python's grammar rules have been violated.

You've already seen errors when you try to use a function incorrectly, but you can also have errors when you use punctuation incorrectly. Python will run a program up until a point where it encounters an error, and when the grammar of a line
  of code has produced an error, the program will shut down and output the error.

```python
# Forgot to close the quotation marks around the string.
name = 'Feng
```

```error
SyntaxError: EOL while scanning string literal
```

```python
# An extra '=' in the assignment.
age = = 52
```

```error
SyntaxError: invalid syntax
```

Let's breakdown each line of this error message:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- At the end of the first line of this error message it notes there is a problem on first line of the input ("line 1").
- The "ipython-input" section of the file name tells us that we are working with input into IPython and the `-6-` part of the filename indicates that the error occurred in cell 6 of our Notebook.
- Next is the problematic line of code - `print ("hello world"` -  indicating where the problem is found with a `^` pointer.
- Finally we get the SyntaxError message, which tells us that Python expected an 'EOF' or end of file. It's often helpful to look at the end of the Error message first. Our SyntaxError, in this case, indicates that Python ran through all of the code but expected to find more information. In this case it expected to encounter a closing parenthesis in the `print("hello world")` function. 

## Python reports a runtime error when something goes wrong while a program is executing.

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError: name 'aege' is not defined
```

You can fix syntax errors by reading the source and runtime errors by tracing execution.

## Every function returns something.

Every function call produces some result and if the function doesn't have a useful result to return, it usually returns the special value `None`.

```python
result = print('example')
print('result of print is', result)
```

```output
example
result of print is None
```

:::::::::::::::::::::::::::::::::::::::  challenge

## What Happens When

1. Explain in simple terms the order of operations in the following program:
  when does the addition happen, when does the subtraction happen,
  when is each function called, etc.
2. What is the final value of `word`?

```python
word = 'blah '
word = max(min(word * 2 + 'blur ', 'aaah '), 'ping')
print(word)
```

:::::::::::::::  solution

## Solution

```
ping
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Spot the Difference

1. Predict what each of the `print` statements in the program below will print.
2. Does `max(len(rich), poor)` run or produce an error message?
  If it runs, does its result make any sense?

```python
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

:::::::::::::::  solution

## Solution

```
tin
4
TypeError: '>' not supported between instances of 'str' and 'int'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Why Not?

Why don't `max` and `min` return `None` when they are given no arguments?

:::::::::::::::  solution

## Solution

Both functions require an argument to execute

```python
print(max())
```

```error
TypeError: max expected 1 arguments, got 0
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Last Character of a String

If Python starts counting from zero,
and `len` returns the number of characters in a string,
what index expression will get the last character in the string `name`?
(Note: we will see a simpler way to do this in a later episode.)

:::::::::::::::  solution

## Solution

`name[len(name) - 1]`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use comments to add documentation to programs.
- A function may take zero or more arguments.
- Commonly-used built-in functions include `max`, `min`, and `round`.
- Functions may only work for certain (combinations of) arguments.
- Functions may have default values for some arguments.
- Use the built-in function `help` to get help for a function.
- Every function returns something.
- Python reports a syntax error when it can't understand the source of a program.
- Python reports a runtime error when something goes wrong while a program is executing.
- Fix syntax errors by reading the source code, and runtime errors by tracing the program's execution.

::::::::::::::::::::::::::::::::::::::::::::::::::


