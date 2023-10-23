---
title: Data Types and Operators
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain key differences between integers and floating point numbers.
- Explain key differences between numbers and character strings.
- Use built-in functions to convert between integers, floating point numbers, and strings.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What kinds of data do programs store?
- How can I convert one type to another?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Every Python object has a type.

Everything in Python is some type of object. Objects contain attributes, usually data and related functions, called methods. Every object that you work with in Python will be of a specific type and understanding an object's type will help you know what you can and can't do with that object. 

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
2. The value of the `age` variable from the previous episode is 45, which is a whole number, or integer (`int`). Note that you can pass a variable to the `type()` function, but it is the *value* of the variable that has a type in Python - the variable is just a label.
3. The first_name variable refers to the string (`str`) of 'Ahmed' from the last episode. 
4. The built-in Python function `print()` is also an object with a type, in this case it's a `builtin_function_or_method`. Note that there are functions and methods that you and others can define in Python. The builtin functions refer to those that are included in the core Python library. 


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

### You can use the `+` and `*` operators on strings.

In the example above, we see that we can't subtract a single character from a string. But some arithmetic operators can be "overloaded" in Python so that they will work on strings. For example, adding" character strings together will concatenate them.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

Along similar lines, multiplying a character string by an integer *n* creates a new string that consists of that character string repeated  *n* times.

```python
ms = 'Mi' + ('ssi' * 2) + 'ppi'
ms
```

```output
Mississippi
```

In the example above, we didn't bother to pass the `ms` variable to a `print()` function. That's because, in Jupyter Notebooks, if a variable is in the last line of a cell, it will print the value of the variable to the output. 

### Strings have a length (but numbers don't).

We've already seen that the function `len` counts the number of characters in a string, but numbers (floats and integers) don't have a length.

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

### Can't add numbers and strings.

We have to convert numbers to strings or vice versa when operating on them.

```python
print(1 + 'A')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

Some types can be converted to other types by using the type name as a function. For example, we can change non-strings to a string using the `str()` function, which allows us to concatenate the objects as strings:

```python
print(str(1) + 'A')
```

```output
1A
```

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

### You can mix integers and floats in operations.

Integers and floating-point numbers can be mixed when you do  arithmetic. Python will automatically convert integers to floats as needed.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

### Variables only change value when something is assigned to them.

In a spreadsheet, if we make cell A1 depend on the value in cell C3, and then update the C3, A1 updates automatically. This does **not** happen with Python variables.

```python
first = 1 
second = 5 * first
first = 2
print('first is', first, 'and second is', second)
```

```output
first is 2 and second is 5
```

When you assigned `second` the value of `5 * first`, the `first` variable was equal to `1`. Because we didn't run any code to reassign `second` after we updated the value of `first`, `second` is still equal to `5`. Remember that variables are assigned when they're run, and they won't update on their own.

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

It is a float:
integers are automatically converted to floats as necessary.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Division Types

There are three different types of division:

1. 'Normal' division (aka floating-point division) is what most people may be familiar with: `5 / 2 = 2.5`
2. Floor division cuts out everything after a decimal point: `5 / 2 = 2`
3. Modulo division returns the remainder after division: `5 / 2 = 1`

In Python 3,  the `/` operator performs floating-point division, the `//`
operator performs floor division, and the '%' (or *modulo*) operator
calculates the modulo division:

```python
print('5 / 3:', 5/3)
print('5 // 3:', 5//3)
print('5 % 3:', 5%3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

If `num_students` is the number of students who registered for a workshop (let's say 150), and `num_per_workshop` is the number that can attend a single section of the workshop (let say 20), write an expression that calculates the number of workshop sections needed to teach everyone. It will be helpful to detect when the number of students per class doesn't divide the number of students evenly. Detect that number with the `%` operator and test if the remainder that it returns is greater than
0.

:::::::::::::::  solution

## Solution

```python
num_students = 150
num_per_workshop = 20
num_classes = num_students // num_per_workshop
remainder = num_students % num_per_workshop

print(num_students, 'students,', num_per_workshop, 'per workshop')
print(num_classes, 'full workshops, plus an extra section with only ', remainder, 'students')
```

```output
150 students, 20 per workshop
7 full workshops, plus an extra section with only  10 students
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Strings to Numbers

Where reasonable, `float()` will convert a string to a floating point number,
and `int()` will convert a floating point number to an integer:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```
If the conversion doesn't make sense, however, an error message will occur

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>()
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Given this information, what do you expect the following program to do?

What does it actually do?

Why do you think it does that?

```python
print("fractional string to int:", int("3.4"))
```

:::::::::::::::  solution

## Solution

What do you expect this program to do? It would not be unreasonable to expect the Python `int` command to convert the string "3.4" to 3.4 and an additional type conversion to 3. After all, Python performs a lot of other magic - isn't that part of its charm?

However, Python throws an error. Why? To be consistent, possibly. If you ask Python to perform two consecutive conversions, you must convert it explicitly in code.

```python
num_as_string = "3.4"
num_as_float = float(num_as_string)
num_as_int = int(num_as_float)
print(num_as_int)
```

```output
3
```

We could also write it in a single line like this: `int(float("3.4"))`


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Arithmetic with Different Types

Which of the following will print 2.0?
Note: there may be more than one right answer.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

:::::::::::::::  solution

## Solution

Answer: 1 and 4.

1. is correct
2. gives 2.1
3. gives an error because we cannot convert text to int directly
4. is correct
5. gives 2 (as an integer not as a float)
6. gives an error because `second` is a string.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Every object has a type.
- Use the built-in function `type` to find the type of an object.
- Types control what operations can be done on objects.
- Strings can be added and multiplied.
- Strings have a length but numbers don't.
- You have to convert numbers to strings or vice versa when operating on them.
- You can mix integers and floats freely in operations.
- Variables only change value when something is assigned to them.

::::::::::::::::::::::::::::::::::::::::::::::::::


