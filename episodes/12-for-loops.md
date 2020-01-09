---
title: "For Loops"
teaching: 10
exercises: 15
questions:
- "How can I make a program do many things?"
objectives:
- "Explain what for loops are normally used for."
- "Trace the execution of a simple (unnested) loop and correctly state the values of variables in each iteration."
- "Write for loops that use the Accumulator pattern to aggregate values."
keypoints:
- "A *for loop* executes commands once for each value in a collection."
- "The first line of the `for` loop must end with a colon, and the body must be indented."
- "Indentation is always meaningful in Python."
- "A `for` loop is made up of a collection, a loop variable, and a body."
- "Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable)."
- "The body of a loop can contain many statements."
- "Use `range` to iterate over a sequence of numbers."
- "The Accumulator pattern turns many values into one."
---
## A *for loop* executes commands once for each value in a collection.

*   Doing calculations on the values in a list one by one
    is as painful as working with `temperature_001`, `temperature_002`, etc.
*   A *for loop* tells Python to execute some statements once for each value in a list,
    a character string,
    or some other collection.
*   "for each thing in this group, do these operations"

~~~
for number in [2, 3, 5]:
    print(number)
~~~
{: .python}

*   This `for` loop is equivalent to:

~~~
print(2)
print(3)
print(5)
~~~
{: .python}

*   And the `for` loop's output is:

~~~
2
3
5
~~~
{: .output}

## The first line of the `for` loop must end with a colon, and the body must be indented.

*   The colon at the end of the first line signals the start of a *block* of statements.
*   Python uses indentation rather than `{}` or `begin`/`end` to show *nesting*.
    *   Any consistent indentation is legal, but almost everyone uses four spaces.

~~~
for number in [2, 3, 5]:
print(number)
~~~
{: .python}
~~~
IndentationError: expected an indented block
~~~
{: .error}

*   Indentation is always meaningful in Python.

~~~
firstName="Jon"
  lastName="Smith"
~~~
{: .python}
~~~
  File "<ipython-input-7-f65f2962bf9c>", line 2
    lastName="Smith"
    ^
IndentationError: unexpected indent
~~~
{: .error}

*   This error can be fixed by removing the extra spaces
    at the beginning of the second line.

## A `for` loop is made up of a collection, a loop variable, and a body.

~~~
for number in [2, 3, 5]:
    print(number)
~~~
{: .python}

*   The collection, `[2, 3, 5]`, is what the loop is being run on.
*   The body, `print(number)`, specifies what to do for each value in the collection.
*   The loop variable, `number`, is what changes for each *iteration* of the loop.
    *   The "current thing".

## Loop variable names follow the normal variable name conventions.

*   Loop variables will:
    *   Be created on demand during the course of each loop.
    *   Persist after the loop finishes.
        * Use a new variable name to avoid overwriting a data collection you need to keep for later
    *   Often be used in the course of the loop
        * So give them a meaningful name you'll understand as the body code in your loop grows.
        * Example: `for single_letter in ['A', 'B', 'C', 'D']:` instead of `for asdf in ['A', 'B', 'C', 'D']:`
~~~
for kitten in [2, 3, 5]:
    print(kitten)
~~~
{: .python}

## The body of a loop can contain many statements.

*   But no loop should be more than a few lines long.
*   Hard for human beings to keep larger chunks of code in mind.

~~~
primes = [2, 3, 5]
for p in primes:
    squared = p ** 2
    cubed = p ** 3
    print(p, squared, cubed)
~~~
{: .python}
~~~
2 4 8
3 9 27
5 25 125
~~~
{: .output}

## Use `range` to iterate over a sequence of numbers.

*   The built-in function `range` produces a sequence of numbers.
    *   *Not* a list: the numbers are produced on demand
        to make looping over large ranges more efficient.
*   `range(N)` is the numbers 0..N-1
    *   Exactly the legal indices of a list or character string of length N

~~~
print('a range is not a list: range(0, 3)')
for number in range(0,3):
    print(number)
~~~
{: .python}
~~~
a range is not a list: range(0, 3)
0
1
2
~~~
{: .output}

## Or use `range` to repeat an action an arbitrary number of times.

*   You don't actually have to use the iterable variable's value.
*   Use this structure to simply repeat an action some number of times.
    *   That number of times goes into the `range` function.

~~~
for number in range(5):
    print("Again!")
~~~
{: .python}
~~~
Again!
Again!
Again!
Again!
Again!
~~~
{: .output}

## The Accumulator pattern turns many values into one.

*   A common pattern in programs is to:
    1.  Initialize an *accumulator* variable to zero, the empty string, or the empty list.
    2.  Update the variable with values from a collection.

~~~
# Sum the first 10 integers.
total = 0
for number in range(10):
   total = total + (number + 1)
print(total)
~~~
{: .python}
~~~
55
~~~
{: .output}

*   Read `total = total + (number + 1)` as:
    *   Add 1 to the current value of the loop variable `number`.
    *   Add that to the current value of the accumulator variable `total`.
    *   Assign that to `total`, replacing the current value.
*   We have to add `number + 1` because `range` produces 0..9, not 1..10.

> ## Classifying Errors
>
> Is an indentation error a syntax error or a runtime error?
>
> > ## Solution
> >
> > It is a syntax error. The problem has to do with the placement of the code, not its logic.
> >
> {: .solution}
{: .challenge}


> ## Tracing Execution
>
> Create a table showing the numbers of the lines that are executed when this program runs,
> and the values of the variables after each line is executed.
>
> ~~~
> total = 0
> for char in "tin":
>     total = total + 1
> ~~~
> {: .python}
{: .challenge}

> ## Reversing a String
>
> Fill in the blanks in the program below so that it prints "nit"
> (the reverse of the original character string "tin").
>
> ~~~
> original = "tin"
> result = ____
> for char in original:
>     result = ____
> print(result)
> ~~~
> {: .python}
> >
> > ## Solution
> >
> > `result` is an empty string because we use it to build or accumulate on our reverse string. `char` is the loop variable for `original`. Each time through the loop `char` takes on one value from `original`. Use `char` with `result` to control the order of the string. Our loop code should look like this:
> > ~~~
> > original = "tin"
> > result = ""
> > for char in original:
> >    result = char + result
> > print(result)
> > nit
> > ~~~
> > If you were to expand out the loop the iterations would look something like this:
> > ~~~
> > #First loop
> > char = "t"
> > result = ""
> > char + result = "t"
> > #Second loop
> > char = 'i"
> > result = "t"
> > char + result = "it"
> > #Third loop
> > char = "n"
> > result = "it"
> > char + result = "nit"
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Practice Accumulating
>
> Fill in the blanks in each of the programs below
> to produce the indicated result.
>
> ~~~
> # Total length of the strings in the list: ["red", "green", "blue"] => 12
> total = 0
> for word in ["red", "green", "blue"]:
>     ____ = ____ + len(word)
> print(total)
> ~~~
> {: .python}
>
> ~~~
> # List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
> lengths = ____
> for word in ["red", "green", "blue"]:
>     lengths.____(____)
> print(lengths)
> ~~~
> {: .python}
>
> ~~~
> # Concatenate all words: ["red", "green", "blue"] => "redgreenblue"
> words = ["red", "green", "blue"]
> result = ____
> for ____ in ____:
>     ____
> print(result)
> ~~~~
> {: .python}
>
> ~~~
> # Create acronym: ["red", "green", "blue"] => "RGB"
> # write the whole thing
> ~~~
> {: .python}
{: .challenge}

> ## Cumulative Sum
>
> Reorder and properly indent the lines of code below
> so that they print an array with the cumulative sum of data.
> The result should be `[1, 3, 5, 10]`.
>
> ~~~
> cumulative += [sum]
> for number in data:
> cumulative = []
> sum += number
> print(cumulative)
> sum = 0
> data = [1,2,2,5]
> ~~~
> {: .python}
> >
> > ## Solution
> > ~~~
> > data = [1,2,2,5]
> > cumulative = []
> > sum = 0
> > for number in data:
> >   sum += number
> >   cumulative += [sum]
> > print(cumulative)
> > ~~~
> > {: .python}
> > ~~~
> > [1, 3, 5, 10]
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Identifying Variable Name Errors
>
> 1. Read the code below and try to identify what the errors are
>    *without* running it.
> 2. Run the code and read the error message.
>    What type of `NameError` do you think this is?
>    Is it a string with no quotes, a misspelled variable, or a
>    variable that should have been defined but was not?
> 3. Fix the error.
> 4. Repeat steps 2 and 3, until you have fixed all the errors.
>
> ~~~
> for number in range(10):
>     # use a if the number is a multiple of 3, otherwise use b
>     if (Number % 3) == 0:
>         message = message + a
>     else:
>         message = message + "b"
> print(message)
> ~~~
> {: .python}
{: .challenge}

> ## Identifying Item Errors
>
> 1. Read the code below and try to identify what the errors are
>    *without* running it.
> 2. Run the code, and read the error message. What type of error is it?
> 3. Fix the error.
>
> ~~~
> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
> print('My favorite season is ', seasons[4])
> ~~~
> {: .python}
>
> > ## Solution
> >
> > It is an index error:
> > ~~~
> > IndexError: list index out of range
> > ~~~
> > {: .error}
> >
> > The problem is that `4` points to an item that doesn't exist in the list. Remember the first item of a list in Python is `0`.  
> > Replace `seasons[4]` with `seasons[0]`, `seasons[1]`, `seasons[2]` or `seasons[3]` to have the different items of the list printed.  
> {: .solution}
{: .challenge}
