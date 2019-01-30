---
title: "Variable Scope"
teaching: 10
exercises: 10
questions:
- "How do function calls actually work?"
- "How can I determine where errors occurred?"
objectives:
- "Identify local and global variables."
- "Identify parameters as local variables."
- "Read a traceback and determine the file, function, and line number on which the error occurred, the type of error, and the error message."
keypoints:
- "The scope of a variable is the part of a program that can 'see' that variable."
---
## The scope of a variable is the part of a program that can 'see' that variable.

*   There are only so many sensible names for variables.
*   People using functions shouldn't have to worry about
    what variable names the author of the function used.
*   People writing functions shouldn't have to worry about
    what variable names the function's caller uses.
*   The part of a program in which a variable is visible is called its *scope*.

~~~
pressure = 103.9

def adjust(t):
    temperature = t * 1.43 / pressure
    return temperature
~~~
{: .python}

*   `pressure` is a *global variable*.
    *   Defined outside any particular function.
    *   Visible everywhere.
*   `t` and `temperature` are *local variables* in `adjust`.
    *   Defined in the function.
    *   Not visible in the main program.
    *   Remember: a function parameter is a variable
        that is automatically assigned a value when the function is called.

~~~
print('adjusted:', adjust(0.9))
print('temperature after call:', temperature)
~~~
{: .python}
~~~
adjusted: 0.01238691049085659
~~~
{: .output}
~~~
Traceback (most recent call last):
  File "/Users/swcarpentry/foo.py", line 8, in <module>
    print('temperature after call:', temperature)
NameError: name 'temperature' is not defined
~~~
{: .error}

> ## Local and Global Variable Use
>
> Trace the values of all variables in this program as it is executed.
> (Use '---' as the value of variables before and after they exist.)
>
> ~~~
> limit = 100
>
> def clip(value):
>     return min(max(0.0, value), limit)
>
> value = -22.5
> print(clip(value))
> ~~~
> {: .python}
> > ## Solution
> > ~~~
> > # limit = ---
> > # value = ---
> > 
> > limit = 100   
> > 
> > def clip(value):  
> >   return min(max(0.0, value), limit)
> > 
> > # limit = 100
> > # value = ---
> > 
> > value = -22.5    # value = -22.5, limit = 100
> > 
> > print(clip(value))   # result is 0.0
> > 
> > # value = -22.5
> > # limit = 100
> > ~~~
> > {: .python}
> >
> {: .solution}
{: .challenge}

> ## Identifying Syntax Errors
>
> 1. Read the code below and try to identify what the errors are
>    *without* running it.
> 2. Run the code and read the error message.
>    Is it a `SyntaxError` or an `IndentationError`?
> 3. Fix the error.
> 4. Repeat steps 2 and 3 until you have fixed all the errors.
>
> ~~~
> def another_function
>   print("Syntax errors are annoying.")
>    print("But at least Python tells us about them!")
>   print("So they are usually not too hard to fix.")
> ~~~
> {: .python}
> > ## Solution
> > There are missing parentheses and colon `():` after the function call, and the print messages don't appear aligned via whitespace
> > ~~~
> >    File "<stdin>", line 1
    def another_function
                       ^
SyntaxError: invalid syntax
> > ~~~
> > {: .error}
> > ~~~
> >   File "<stdin>", line 1
    print("Syntax errors are annoying.")
    ^
IndentationError: unexpected indent  
> > ~~~
> > {: .error}
> > ~~~
> >   File "<stdin>", line 1
    print("But at least Python tells us about them!")
    ^
IndentationError: unexpected indent  
> > ~~~
> > {: .error}
> > Working function:  
> > ~~~
> > def another_function():
  print("Syntax errors are annoying.")
  print("But at least Python tells us about them!")
  print("So they are usually not too hard to fix.")
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Reading Error Messages
>
> Read the traceback below, and identify the following:
>
> 1. How many levels does the traceback have?
> 2. What is the file name where the error occurred?
> 3. What is the function name where the error occurred?
> 4. On which line number in this function did the error occur?
> 5. What is the type of error?
> 6. What is the error message?
>
> ~~~
> ---------------------------------------------------------------------------
> KeyError                                  Traceback (most recent call last)
> <ipython-input-2-e4c4cbafeeb5> in <module>()
>       1 import errors_02
> ----> 2 errors_02.print_friday_message()
>
> /Users/ghopper/thesis/code/errors_02.py in print_friday_message()
>      13
>      14 def print_friday_message():
> ---> 15     print_message("Friday")
>
> /Users/ghopper/thesis/code/errors_02.py in print_message(day)
>       9         "sunday": "Aw, the weekend is almost over."
>      10     }
> ---> 11     print(messages[day])
>      12
>      13
>
> KeyError: 'Friday'
> ~~~
> {: .error}
> > ## Solution
> > 1. 3 levels, since there are 3 arrows
> > 2. The file is `errors_02.py` 
> > 3. The function is `print_message()`
> > 4. Line 11
> > 5. It is a `KeyError`
> > 6. There isn’t really a message; you’re supposed to infer that `Friday` is not a key in `messages`.
> {: .solution}
{: .challenge}
