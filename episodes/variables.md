---
title: Variables and types
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Write programs that assign values to variables and perform calculations with those values.
- Use indexing to manipulate elements within a string.
- View and convert the data types of Python objects.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I store data in Python?
- What are some types of data that I can work with in Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use variables to store values.

Variables are names given to certain values. In Python the `=` symbol assigns a value to a variable. Here, Python assigns the number `42` to the variable `age` and the name `Ahmed` in single quote to a variable `first_name`.

```python
age = 42
first_name = 'Ahmed'
```

- Variable names:
  - cannot start with a digit
  - cannot contain spaces, quotation marks, or other punctuation
  - *may* contain an underscore (typically used to separate words in long variable names)
  - are case sensitive. `first_name` and `First_Name` would be different variables.

## Use `print()` to display values.

You can print Python objects to the Jupyter notebook output using the built-in function, `print()`. Inside of the parentheses we can add the objects that we want print, which are known as the `print()` function's arguments. You can pass variables and text strings (by placing text within quotes) directly to the print function, and you can separate multiple items with commas. 

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

## Variables must be created before they are used.

If a variable doesn't exist yet, or if the name has been misspelled, Python reports an error called a `NameError`.

```python
print(eye_color)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(eye_color)

NameError: name 'eye_color' is not defined
```

The last line of an error message is usually the most informative. In this case it tells us that the `eye_color` variable is not defined. NameErrors often refer to variables that haven't been created or assigned yet.

:::::::::::::::::::::::::::::::::::::::::  callout

## Variables Persist Between Cells

Variables defined in one Notebook cell are available in all other cells once they have been executed, so the location of cells in the notebook do not matter. In other words, if you execute a cell at the bottom of your notebook the variables in that cell will be available to cells at the top of the notebook. Notebook cells are a great way to organize your code, but Python only cares about the order in which the code has been executed.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Variables can be used in calculations.

We can use variables in calculations as if they were values. We assigned 42 to `age` a few lines ago, so we can reference that value within a new variable assignment.

```python
age = age + 3
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Every Python object has a type.

Everything in Python is some type of object. Every object that you work with in Python will be of a specific type and understanding an object's type will help you know what you can and can't do with that object. 

### Use the built-in function `type()` to find an object's type.

You can use the built-in Python function `type()` to find out an object's type. 

```python
print(type(140.2))
print(type(age))
print(type(first_name))
print(type(print))
```

```output
<class 'float'>
<class 'int'>
<class 'str'>
<class 'builtin_function_or_method'>
```

1. 140.2 is an example of a floating point number or `float`. These are fractional numbers. 
2. The value of the `age` variable is 45, which is a whole number, or integer (`int`).
3. The first_name variable refers to the string (`str`) of 'Ahmed'.
4. The built-in Python function `print()` is also an object with a type, in this case it's a `builtin_function_or_method`. Built-in functions refer to those that are included in the core Python library.

## Types control what operations (or methods) can be performed on objects.

An object's type determines what the program can do with it.

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## Use an index to get a single character from a string.

We can reference the specific location of a character (individual letters, numbers, and so on) in a text string by using its index position. In Python, each character in a string (first, second, etc.) is given a number, which is called an index. Indices are numbered to begin from 0 rather than 1. We can use an index number in square brackets to refer to the character at that position.

```python
library = 'Alexandria'
print(library[0])
```

```output
A
```

## Use a slice to get multiple characters from a string.

A slice is a part of a string that we can reference using `[start:stop]`, where `start` is the index of the first character we want and `stop` is the last character. Referencing a string slice does not change the contents of the original string. Instead, the slice returns a copy of the part of the original string we want. 

```python
print(library[0:3])
```

```output
Ale
```

Note that in the example above, `library[0:3]` begins with zero, which refers to the first element in the string, and ends with a 3. When working with slices the end point is interpreted as going up to, *but not including* the index number provided. In other words, the character in the index position of 3 in the string `Alexandria` is `x`, so the slice `[0:3]` will go up to but not include that character, and therefore give us `Ale`.

## Use the built-in function `len` to find the length of a string.

The `len()`function will tell us the length of an item. In the case of a string, it will tell us how many characters are in the string. 

```python
print(len('Babel'))
```

```output
5
```

In the example above we have nested the `print()` and `len()` functions. When nesting functions, they are evaluated from the inside out, just like in mathematics, so `len()` is evaluated first, followed by the `print()` function.

### Variables only change value when something is assigned to them.

We can do arithmetic within a variable assignment, as we saw when we assigned the age variable. But once a Python variable is assigned it will not change value unless the assignment code is run again. The value of `older_age` does not get updated when we change the assignment of `age` to `50`, for example:

```python
age = 42
older_age = age + 3
age = 50
print('older age is', older_age, 'and age is', age)
```

```output
older age is 45 and age is 50
```

A variable in Python is analogous to a sticky note with a name written on it: assigning a value to a variable is like putting a sticky note on a particular value. When we assigned the variable `older_age`, it was like we put a sticky note with the name `older_age` on the value of `45`. Remember, `45` was the result of `age + 3` because `age` at that point in the code was equal to `42`. The `older_age` sticky note (variable) was never attached to (assigned to) another value, so it doesn't change when the `age` variable is updated to be `50`.

:::::::::::::::::::::::::::::::::::::::  challenge

## Swapping Values

Draw a table showing the values of the variables in this program
after each statement is executed.
In simple terms, what do the last three lines of this program do?

```python
x = 1.0
y = 3.0
swap = x
x = y
y = swap
```

:::::::::::::::  solution

## Solution

```
swap = x  #  x = 1.0 y = 3.0 swap = 1.0
x = y     #  x = 3.0 y = 3.0 swap = 1.0
y = swap  #  x = 3.0 y = 1.0 swap = 1.0
```

These three lines exchange the values in `x` and `y` using the `swap`
variable for temporary storage. This is a fairly common programming idiom.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Predicting Values

What is the final value of `position` in the program below?
(Try to predict the value without running the program,
then check your prediction.)

```python
initial = "left"
position = initial
initial = "right"
```

:::::::::::::::  solution

## Solution

```python
initial = "left"  # Initial is assigned the string "left"
position = initial  # Position is assigned the variable initial, currently "left"
initial = "right"  # Initial is assigned the string "right"
print(position)
```

```output
left
```

The last assignment to position was "left"



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Can you slice integers?

If you assign `a = 123`,
what happens if you try to get the second digit of `a`?

:::::::::::::::  solution

## Solution

Numbers are not stored in the written representation,
so they can't be treated like strings.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Slicing

We know how to slice using an explicit start and end point:

```python
library_name = 'Library of Babel'
print('library_name[1:3] is:', library_name[1:3])
```
```output
library_name[1:3] is: ib
```

But we can also use implicit and negative index values when we define a slice. Try the following (replacing `low` and `high` with index positions of your choosing) to figure out how these different forms of slicing work:

1. What does `library_name[low:]` (without a value after the colon) do?
2. What does `library_name[:high]` (without a value before the colon) do?
3. What does `library_name[:]` (just a colon) do?
4. What does `library_name[number:negative-number]` do?

:::::::::::::::  solution

## Solution

1. It will slice the string, starting at the `low` index and stopping at the end of the string.
2. It will slice the string, starting at the beginning on the string, and ending an element before the `high` index.
3. It will print the entire string.
4. It will slice the string, starting the `number` index, and ending a distance of the absolute value of `negative-number` elements from the end of the string.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Fractions

What type of value is 3.4?
How can you find out?

:::::::::::::::  solution

## Solution

It is a floating-point number (often abbreviated "float").

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Automatic Type Conversion

What type of value is 3.25 + 4?

:::::::::::::::  solution

## Solution

It is a float: integers are automatically converted to floats as necessary.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::: keypoints

- Use variables to store values.
- Use `print` to display values.
- Variables persist between cells.
- Variables must be created before they are used.
- Variables can be used in calculations.
- Use an index to get a single character from a string.
- Use a slice to get a portion of a string.
- Use the built-in function `len` to find the length of a string.
- Python is case-sensitive.
- Every object has a type.
- Use the built-in function `type` to find the type of an object.
- Types control what operations can be done on objects.
- Variables only change value when something is assigned to them.

::::::::::::::::::::::::::::::::::::::::::::::::::


