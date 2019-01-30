---
title: "Libraries"
teaching: 10
exercises: 10
questions:
- "How can I extend the capabilities of Python?"
- "How can I use software that other people have written?"
- "How can I find out what that software does?"
objectives:
- "Explain what software libraries are and why programmers create and use them."
- "Write programs that import and use libraries from Python's standard library."
- "Find and read documentation for standard libraries interactively (in the interpreter) and online."
keypoints:
- "Most of the power of a programming language is in its libraries."
- "A program must import a library module in order to use it."
- "Use `help` to learn about the contents of a library module."
- "Import specific items from a library to shorten programs."
- "Create an alias for a library when importing it to shorten programs."
---
## Most of the power of a programming language is in its (software) libraries.

*   A *(software) library* is a collection of files (called *modules*) that contains
    functions for use by other programs.
    *   May also contain data values (e.g., numerical constants) and other things.
    *   Library's contents are supposed to be related, but there's no way to enforce that.
*   The Python [standard library][stdlib] is an extensive suite of modules that comes
    with Python itself.
*   Many additional libraries are available from [PyPI][pypi] (the Python Package Index).
*   We will see later how to write new libraries.

> ## Libraries and modules
>
> A library is a collection of modules, but the terms are often used
> interchangeably, especially since many libraries only consist of a single
> module, so don't worry if you mix them.
{: .callout}


## A program must import a library module before using it.

*   Use `import` to load a library module into a program's memory.
*   Then refer to things from the module as `module_name.thing_name`.
    *   Python uses `.` to mean "part of".
*   Using `string`, one of the modules in the standard library:

~~~
import string

print('The lower ascii letters are', string.ascii_lowercase)
print(string.capwords('capitalise this sentence please.'))
~~~
{: .python}
~~~
The lower ascii letters are abcdefghijklmnopqrstuvwxyz
Capitalise This Sentence Please.
~~~
{: .output}

*   You have to refer to each item with the module's name.
    *   `string.capwords(ascii_lowercase)` won't work: the reference to `ascii_lowercase`
        doesn't somehow "inherit" the function's reference to `string`.

## Use `help` to learn about the contents of a library module.

*   Works just like help for a function.

~~~
help(string)
~~~
{: .python}
~~~
Help on module string:

NAME
    string - A collection of string constants.

MODULE REFERENCE
    https://docs.python.org/3.6/library/string
    
    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    Public module variables:
    
    whitespace -- a string containing all ASCII whitespace
    ascii_lowercase -- a string containing all ASCII lowercase letters
    ascii_uppercase -- a string containing all ASCII uppercase letters
    ascii_letters -- a string containing all ASCII letters
    digits -- a string containing all ASCII decimal digits
    hexdigits -- a string containing all ASCII hexadecimal digits
    octdigits -- a string containing all ASCII octal digits
    punctuation -- a string containing all ASCII punctuation characters
    printable -- a string containing all ASCII characters considered printable

CLASSES
    builtins.object
        Formatter
        Template
⋮ ⋮ ⋮
~~~
{: .output}

## Import specific items from a library module to shorten programs.

*   Use `from ... import ...` to load only specific items from a library module.
*   Then refer to them directly without library name as prefix.

~~~
from string import ascii_letters

print('The ASCII letters are', ascii_letters)
~~~
{: .python}
~~~
The ASCII letters are abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
~~~
{: .output}

## Create an alias for a library module when importing it to shorten programs.

*   Use `import ... as ...` to give a library a short *alias* while importing it.
*   Then refer to items in the library using that shortened name.

~~~
import string as s

print(s.capwords('capitalise this sentence again please.'))
~~~
{: .python}
~~~
Capitalise This Sentence Again Please.
~~~
{: .output}

*   Commonly used for libraries that are frequently used or have long names.
    *   E.g., The `pandas` library is often aliased as `pd`.
*   But can make programs harder to understand,
    since readers must learn your program's aliases.

> ## Exploring the os Library
> The os library provides a way of accessing operating system functionality.
>
> 1. What function from the `os` library can you use to determine the current 
>    working directory?
>
> > ## Solution
> > 1. Using `help(os)` we see that we've got `os.getcwd()` which returns
> >    a string representing the current working directory.
> {: .solution}
{: .challenge}

> ## Locating the Right Module
>
> Given the variables `year`, `month` and `day`, how would you generate a date in the standard iso format:
>
> ~~~
> year = 2016
> month = 10
> day = 22
> ~~~
> {: .python}
>
> 1. Which [standard library][stdlib] module could help you?
> 2. Which function would you select from that module?
> 3. Try to write a program that uses the function.
>
> > ## Solution
> >
> > The [datetime module](https://docs.python.org/3/library/datetime.html) seems like it could help you.
> >
> >
> > You could use `date(year, month, date).isoformat()` to convert your date:
> >
> > ~~~
> > import datetime
> >
> > iso_date = datetime.date(year, month, day).isoformat()
> > print(iso_date)
> > ~~~
> > {: .python}
> >
> > or more compactly:
> >
> > ~~~
> > import datetime
> >
> > print(datetime.date(year, month, day).isoformat())
> > ~~~
> > {: .python}
> >
> {: .solution}
{: .challenge}

> ## When Is Help Available?
>
> When a colleague of yours types `help(os)`,
> Python reports an error:
>
> ~~~
> NameError: name 'os' is not defined
> ~~~
> {: .error}
>
> What has your colleague forgotten to do?
>
> > ## Solution
> >
> > Importing the os module (`import os`)
> {: .solution}
{: .challenge}

> ## Importing With Aliases
>
> 1. Fill in the blanks so that the program below prints `0123456789`.
> 2. Rewrite the program so that it uses `import` *without* `as`.
> 3. Which form do you find easier to read?
>
> ~~~
> import string as s
> numbers = ____.digits
> print(____)
> ~~~
> {: .python}
>
> > ## Solution
> >
> > ~~~
> > import string as s
> > numbers = s.digits
> > print(numbers)
> > ~~~
> > {: .python}
> >
> > can be written as
> >
> > ~~~
> > import string
> > numbers = string.digits
> > print(numbers)
> > ~~~
> > {: .python}
> >
> > Since you just wrote the code and are familiar with it, you might actually
> > find the first version easier to read. But when trying to read a huge piece
> > of code written by someone else, or when getting back to your own huge piece
> > of code after several months, non-abbreviated names are often easier, expect
> > where there are clear abbreviation conventions.
> {: .solution}
{: .challenge}

> ## There Are Many Ways To Import Libraries!
>
> Match the following print statements with the appropriate library calls
>
> Library calls:
> ~~~
> A) from string import digits
> B) import string
> C) import string as s
> ~~~
> {: .python}
>
> Print commands:
> ~~~
> 1. print(list(s.digits))
> 2. print(list(digits))
> 3. print(string.ascii_uppercase)
> ~~~
> {: .python}
> >
> > ## Solution
> > A2) Importing `digits` from `string` provides the `digits` methods
> > B3) Importing `string` provides methods such as `ascii_uppercase`, but
> >     requires the `string.` syntax.
> > C1) Importing `string` with the alias `s` allows `s.digits`
> {: .solution}
{: .challenge}

> ## Importing Specific Items
>
> 1. Fill in the blanks so that the program below prints `90.0`.
> 2. Do you find this version easier to read than preceding ones?
> 3. Why *wouldn't* programmers always use this form of `import`?
>
> ~~~
> ____ math import ____, ____
> angle = degrees(pi / 2)
> print(angle)
> ~~~
> {: .python}
>
> > ## Solution
> >
> > ~~~
> > from math import degrees, pi
> > angle = degrees(pi / 2)
> > print(angle)
> > ~~~
> > {: .python}
> >
> > Most likely you find this version easier to read since it's less dense.
> > The main reason not to use this form of import is to avoid name clashes.
> > For instance, you wouldn't import `degrees` this way if you also wanted to
> > use the name `degrees` for a variable or function of your own. Or if you
> > were to also import a function named `degrees` from another library.
> {: .solution}
{: .challenge}

> ## Reading Error Messages
>
> 1. Read the code below and try to identify what the errors are without running it.
> 2. Run the code, and read the error message. What type of error is it?
>
> ~~~
> import datetime
> datetime.date(2017,13,1)
> ~~~
> {: .python}
>
> > ## Solution
> >
> > 1. The date object takes arguments in the order year, month, day, so 13 is 
> >    an invalid value for month.
> > 2. You get an error of type "ValueError", indicating that the object
> >    received an inappropriate argument value. The additional message
> >    "month must be in 1..12" makes it clearer what the problem is.
> {: .solution}
{: .challenge}

[pypi]: https://pypi.org/
[stdlib]: https://docs.python.org/3/library/
[randommod]: https://docs.python.org/3/library/random.html
