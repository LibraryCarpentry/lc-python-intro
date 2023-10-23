---
title: Data Types and Operators
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Write Python to view and convert the data types of Python objects.
- Perform arithmetic on floating point numbers and integers, and perform string operations such as concatenation on strings.

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

In the example above, we didn't bother to pass the `ms` variable to a `print()` function. That's because, in Jupyter Notebooks, if a variable is in the last line of a cell, it will output the value of the object to the Notebook. 

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


