---
title: Variable Scope
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Identify local and global variables.
- Identify parameters as local variables.
- Read a traceback and determine the file, function, and line number on which the error occurred, the type of error, and the error message.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How do function calls actually work?
- How can I determine where errors occurred?

::::::::::::::::::::::::::::::::::::::::::::::::::

## The scope of a variable is the part of a program that can 'see' that variable.

When we define a variable inside of a function in Python, it's known as a `local` variable, which means that it's not visible to (or "known" by) the rest of the program. Variables that we define outside of functions are "global" and are therefore visible throughout the program, *including* from within other functions. 

There are only so many sensible names for variables.
- People using functions shouldn't have to worry about
  what variable names the author of the function used.
- People writing functions shouldn't have to worry about
  what variable names the function's caller uses.
- The part of a program in which a variable is visible is called its *scope*.

```python
initial_fine = 0.25
late_fine = 0.50

def calc_fine(days_overdue):
    if days_overdue <= 10:
        days_overdue =  days_overdue * initial_fine
    else:
        days_overdue = (days_overdue * initial_fine) + (days_overdue * late_fine)
    return days_overdue
    
```

- `initial_fine` and `late_fine` are *global variables*.
- `days_overdue` is a *local variable* in `calc_fine`. Note that a function parameter is a variable that is automatically assigned a value when the function is called and so acts as a local variable.

```python
fine = calc_fine(12)
print('Fine owed:', fine)
print('Fine rates:', initial_fine, late_fine)
print('Days overdue:', days_overdue)
```

```output
Fine owed: 9.0
Fine rates: 0.25 0.5
```

```error
NameError                                 Traceback (most recent call last)
Cell In[23], line 14
     12 print('Fine owed:', fine)
     13 print('Fine rates:', initial_fine, late_fine)
---> 14 print('Days overdue:', days_overdue)

NameError: name 'days_overdue' is not defined
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Local and Global Variable Use

Trace the values of all variables in this program as it is executed.
(Use '---' as the value of variables before and after they exist.)

```python
limit = 100

def clip(value):
    return min(max(0.0, value), limit)

value = -22.5
print(clip(value))
```

:::::::::::::::  solution

## Solution

```python
# limit = ---
# value = ---

limit = 100   

def clip(value):  
  return min(max(0.0, value), limit)

# limit = 100
# value = ---

value = -22.5    # value = -22.5, limit = 100

print(clip(value))   # result is 0.0

# value = -22.5
# limit = 100
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Syntax Errors

1. Read the code below and try to identify what the errors are
  *without* running it.
2. Run the code and read the error message.
  Is it a `SyntaxError` or an `IndentationError`?
3. Fix the error.
4. Repeat steps 2 and 3 until you have fixed all the errors.

```python
def another_function
  print("Syntax errors are annoying.")
   print("But at least Python tells us about them!")
  print("So they are usually not too hard to fix.")
```

:::::::::::::::  solution

## Solution

There are missing parentheses and colon `():` after the function call, and the print messages don't appear aligned via whitespace

```error
   File "<stdin>", line 1
def another_function
                   ^
SyntaxError: invalid syntax
```

```error
  File "<stdin>", line 1
  print("Syntax errors are annoying.")
^
IndentationError: unexpected indent  
```

```error
  File "<stdin>", line 1
  print("But at least Python tells us about them!")
^
IndentationError: unexpected indent  
```

Working function:

```python
def another_function():
    print("Syntax errors are annoying.")
    print("But at least Python tells us about them!")
    print("So they are usually not too hard to fix.")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reading Error Messages

Read the traceback below, and identify the following:

1. How many levels does the traceback have?
2. What is the file name where the error occurred?
3. What is the function name where the error occurred?
4. On which line number in this function did the error occur?
5. What is the type of error?
6. What is the error message?

```error
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-2-e4c4cbafeeb5> in <module>()
      1 import errors_02
----> 2 errors_02.print_friday_message()

/Users/ghopper/thesis/code/errors_02.py in print_friday_message()
     13
     14 def print_friday_message():
---> 15     print_message("Friday")

/Users/ghopper/thesis/code/errors_02.py in print_message(day)
      9         "sunday": "Aw, the weekend is almost over."
     10     }
---> 11     print(messages[day])
     12
     13

KeyError: 'Friday'
```

:::::::::::::::  solution

## Solution

1. 3 levels, since there are 3 arrows
2. The file is `errors_02.py`
3. The function is `print_message()`
4. Line 11
5. It is a `KeyError`
6. There isn't really a message; you're supposed to infer that `Friday` is not a key in `messages`.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- The scope of a variable is the part of a program that can 'see' that variable.

::::::::::::::::::::::::::::::::::::::::::::::::::

