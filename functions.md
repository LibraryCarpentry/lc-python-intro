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

An *argument* is a value passed into a function. Any arguments you want to pass into a function must go into the `()`.

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

## Commonly-used built-in functions include `max()` and `min()`.

- Use `max()` to find the largest value of one or more values.
- Use `min()` to find the smallest.

Both `max()` and `min()` work on character strings as well as numbers, so can be used for numerical and alphabetical comparisons. Note that numerical and alphabetical comparisons follow some specific rules about what is larger or smaller: numbers are smaller than letters and upper case letters are smaller than lower case letters, so the order of operations in Python is 0-9, A-Z, a-z when comparing numbers and letters.

```python
print(max(1, 2, 3)) # notice that functions are nestable
print(min('a', 'b', max('c', 'd'))) # nest with care since code gets less readable
print(min('a', 'A', '2')) # numbers and letters can be compared if they are the same data type
```

```output
3
a
2
```

## Functions may only work for certain (combinations of) arguments.

`max()` and `min()` must be given at least one argument and they must be given things that can meaningfully be compared.

```python
max(1, 'a')
```

```error
TypeError                                 Traceback (most recent call last)
Cell In[6], line 1
----> 1 max(1, 'a')

TypeError: '>' not supported between instances of 'str' and 'int'
```

## Function argument default values, and `round()`.

`round()` will round off a floating-point number. By default, it will round to zero decimal places, which is how it will operate if you don't pass a second argument.

```python
round(3.712)
```

```output
4
```

We can use a second argument (or parameter) to specify the number of decimal places we want though.

```python
round(3.712, 1)
```

```output
3.7
```

## Use the built-in function `help` to get help for a function.

Every built-in function has online documentation. You can always access the documentation using the built-in `help()` function. In the jupyter environment, you can access help by either adding a `?` at the end of your function and running it or Hold down <kbd>Shift</kbd>, and press <kbd>Tab</kbd> when your insertion cursor is in or near the function name.

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

## Every function returns something.

Every function call produces some result and if the function doesn't have a useful result to return, it usually returns the special value `None`. Each line of Python code is executed in order. In this case, the second line call to `{result}` returns 'None' since the `print` statement in the previous line didn't return a value to the `result` variable.

```python
result = print('example')
print(f'result of print is {result}')
```

```output
example
result of print is None
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Spot the Difference

1. Predict what each of the `print` statements in the program below will print.
2. Does `max(len(cataloger), assistant_librarian)` run or produce an error message?
  If it runs, does its result make any sense?

```python
cataloger = "metadata_curation"
assistant_librarian = "archives"
print(max(cataloger, assistant_librarian))
print(max(len(cataloger), assistant_librarian))
```

:::::::::::::::  solution

## Solution

```output
metadata_curation
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[2], line 4
      2 assistant_librarian = "archives"
      3 print(max(cataloger, assistant_librarian))
----> 4 print(max(len(cataloger), assistant_librarian))

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



:::::::::::::::::::::::::::::::::::::::: keypoints

- Use comments to add documentation to programs.
- A function may take zero or more arguments.
- Commonly-used built-in functions include `max`, `min`, and `round`.
- Functions may only work for certain (combinations of) arguments.
- Functions may have default values for some arguments.
- Use the built-in function `help` to get help for a function.
- Every function returns something.

::::::::::::::::::::::::::::::::::::::::::::::::::


