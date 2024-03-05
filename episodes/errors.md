---
title: Errors (and other sandbox items)
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives


- Correctly describe situations in which SyntaxError and NameError occur.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions


- What kind of errors can occur in programs?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Python reports a syntax error when Python's grammar rules have been violated.

You've already seen errors when you try to use a function incorrectly, but you can also have errors when you use punctuation incorrectly. Python will run a program up until a point where it encounters an error, and when the grammar of a line of code has produced an error, the program will shut down and output the error.

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

- Python reports a syntax error when it can't understand the source of a program.
- Python reports a runtime error when something goes wrong while a program is executing.
- Fix syntax errors by reading the source code, and runtime errors by tracing the program's execution.

::::::::::::::::::::::::::::::::::::::::::::::::::


