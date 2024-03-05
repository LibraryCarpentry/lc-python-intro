---
title: Programming Style
teaching: 15
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Provide sound justifications for basic rules of coding style.
- Refactor one-page programs to make them more readable and justify the changes.
- Use Python community coding standards (PEP-8).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I make my programs more readable?
- How do most programmers format their code?
- How can programs check their own operation?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Follow standard Python style in your code.

- [PEP8](https://www.python.org/dev/peps/pep-0008):
  a style guide for Python that discusses topics such as how you should name variables,
  how you should use indentation in your code,
  how you should structure your `import` statements,
  etc.
  Adhering to PEP8 makes it easier for other Python developers to read and understand your code,
  and to understand what their contributions should look like.
  The [PEP8 application and Python library](https://pypi.org/project/pep8/)
  can check your code for compliance with PEP8.

## Use assertions to check for internal errors.

Assertions are powerful method for making sure that the context in which your code is executing is as you expect.

```python
def calc_bulk_density(mass, volume):
    '''Return dry bulk density = powder mass / powder volume.'''
    assert volume > 0
    return mass / volume
```

If the assertion is `False`, the Python interpreter raises an `AssertionError` runtime exception. The source code for the expression that failed will be displayed as part of the error message. To ignore assertions in your code run the interpreter with the '-O' (optimize) switch. Assertions should contain only basic checks and never change the state of the program. For example, an assertion should never contain an assignment.

## Use docstrings to provide online help.

- If the first thing in a function is a character string
  that is not assigned to a variable,
  Python attaches it to the function as the online help.
- Called a *docstring* (short for "documentation string").

```python
def average(values):
    "Return average of values, or None if no values are supplied."

    if len(values) == 0:
        return None
    return sum(values) / average(values)

help(average)
```

```output
Help on function average in module __main__:

average(values)
    Return average of values, or None if no values are supplied.
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Multiline Strings

Often use *multiline strings* for documentation.
These start and end with three quote characters (either single or double)
and end with three matching characters.

```python
"""This string spans
multiple lines.

Blank lines are allowed."""
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## What Will Be Shown?

Highlight the lines in the code below that will be available as online help.
Are there lines that should be made available, but won't be?
Will any lines produce a syntax error or a runtime error?

```python
"Find maximum edit distance between multiple sequences."
# This finds the maximum distance between all sequences.

def overall_max(sequences):
    '''Determine overall maximum edit distance.'''

    highest = 0
    for left in sequences:
        for right in sequences:
            '''Avoid checking sequence against itself.'''
            if left != right:
                this = edit_distance(left, right)
                highest = max(highest, this)

    # Report.
    return highest
```

:::::::::::::::  solution

## Solution

These two lines will show up in online help:

```python
 '''Determine overall maximum edit distance.'''
 '''Avoid checking sequence against itself.'''
```

This line will not be made available because it is not in the docstring format: `"Find maximum edit distance between multiple sequences."` Docstrings should reside within the function definition, using three single quotes.

There is one syntax error:

```python
Traceback (most recent call last):
File "<interactive input>", line 1, in <module>
File "<module2>", line 11, in overall_max
NameError: global name 'edit_distance' is not defined
```

The `edit_distance` function has not been defined:

```python
 this = edit_distance(left, right)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Document This

Turn the comment on the following function into a docstring
and check that `help` displays it properly.

```python
def middle(a, b, c):
    # Return the middle value of three.
    # Assumes the values can actually be compared.
    values = [a, b, c]
    values.sort()
    return values[1]
```

:::::::::::::::  solution

## Solution

Change the `#` to `'''` to change to docstring:

```python
 def middle(a, b, c):
 ''' Return the middle value of three.
 Assumes the values can actually be compared.
 '''
 values = [a, b, c]
 values.sort()
 return values[1]  
```

Calling `help` on the `middle` function now shows the docstring:

```python
help (middle)
Help on function middle in module __main__:
middle(a, b, c)
   Return the middle value of three.
   Assumes the values can actually be compared. 
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Clean Up This Code

1. Read this short program and try to predict what it does.
2. Run it: how accurate was your prediction?
3. Refactor the program to make it more readable.
  Remember to run it after each change to ensure its behavior hasn't changed.
4. Compare your rewrite with your neighbor's.
  What did you do the same?
  What did you do differently, and why?

```python
import sys
n = int(sys.argv[1])
s = sys.argv[2]
print(s)
i = 0
while i < n:
    # print('at', j)
    new = ''
    for j in range(len(s)):
        left = j-1
        right = (j+1)%len(s)
        if s[left]==s[right]: new += '-'
        else: new += '*'
    s=''.join(new)
    print(s)
    i += 1
```

:::::::::::::::  solution

## Solution

Here's one solution.

```python
def string_machine(input_string, iterations):
    """
    Takes input_string and generates a new string with -'s and *'s
    corresponding to characters that have identical adjacent characters
    or not, respectively.  Iterates through this procedure with the resultant
    strings for the supplied number of iterations.
    """
    print(input_string)
    old = input_string
    for i in range(iterations):
        new = ''
        # iterate through characters in previous string
        for j in range(len(s)):
            left = j-1
            right = (j+1)%len(s) # ensure right index wraps around
            if old[left]==old[right]:
                new += '-'
            else:
                new += '*'
        print(new)
        # store new string as old
        old = new

string_machine('et cetera', 10)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Follow standard Python style in your code.
- Use docstrings to provide online help.

::::::::::::::::::::::::::::::::::::::::::::::::::


