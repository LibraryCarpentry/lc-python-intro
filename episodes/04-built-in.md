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

```python
# This sentence isn't executed by Python.
name = 'Library Carpentry'   # Neither is this comment - anything after '#' is ignored.
```

## A function may take zero or more arguments.

- We have seen some functions already --- now let's take a closer look.
- An *argument* is a value passed into a function.
- Any arguments you want to pass into a function must go into the `()`
  - `print("I am an argument and must go here.")`
- You must always use parentheses, because this is how Python knows you are calling a function.
  - You leave them empty if you don't want or need to pass any arguments in.
- `len` takes exactly one.
- `int`, `str`, and `float` create a new value from an existing one.
- `print` takes zero or more.
  - `print()` prints a blank line.

```python
print('before')
print()
print('after')
```

```output
before

after
```

## Commonly-used built-in functions include `max`, `min`, and `round`.

- Use `max` to find the largest value of one or more values.
- Use `min` to find the smallest.
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

- `max` and `min` must be given at least one argument.
- And they must be given things that can meaningfully be compared.

```python
print(max(1, 'a'))
```

```error
TypeError: unorderable types: str() > int()
```

## Functions may have default values for some arguments.

- `round` will round off a floating-point number.
- By default, rounds to zero decimal places.

```python
round(3.712)
```

```output
4
```

- We can specify the number of decimal places we want.

```python
round(3.712, 1)
```

```output
3.7
```

## Use the built-in function `help` to get help for a function.

- Every built-in function has online documentation.

```python
help(round)
```

```output
Help on built-in function round in module builtins:

round(...)
    round(number[, ndigits]) -> number

    Round a number to a given precision in decimal digits (default 0 digits).
    This returns an int when called with one argument, otherwise the
    same type as the number. ndigits may be negative.
```

## Python reports a syntax error when grammar rules (that's Python grammar, not English grammar) have been violated.

- You've seen errors when you try to use a function incorrectly.
  - Can also have errors when you use punctuation incorrectly.
- Python will run the program up until that point, but if the grammar of that line
  of code has produced an error, then the program will shut down with an error.

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

- Look more closely at the error message:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- The message indicates a problem on first line of the input ("line 1").
  - In this case the "ipython-input" section of the file name tells us that
    we are working with input into IPython.
- The `-6-` part of the filename indicates that
  the error occurred in cell 6 of our Notebook.
- Next is the problematic line of code,
  indicating the problem with a `^` pointer.

## Python reports a runtime error when something goes wrong while a program is executing.

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError: name 'aege' is not defined
```

- Fix syntax errors by reading the source and runtime errors by tracing execution.

## Every function returns something.

- Every function call produces some result.
- If the function doesn't have a useful result to return,
  it usually returns the special value `None`.

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


