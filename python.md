# Python

## Python shebang

``` 
#!/usr/bin/env python3
``` 

## `zip()`

Python has a number of built-in functions that allow coders to loop through data. One of these functions is Python zip. The `zip()` function creates an iterator that will merge elements from two or more data sources into one.

The Python `zip()` function has a wide variety of applications. For example, if you want to create a set of dictionaries from two arrays, each of which holds an employee name and their employee number, we could do that using `zip()`.

```python
employee_numbers = [2, 9, 18, 28]
employee_names = ["Candice", "Ava", "Andrew", "Lucas"]

zipped_values = zip(employee_names, employee_numbers)
zipped_list = list(zipped_values)

print(zipped_list)
```
```python
[('Candice', 2), ('Ava', 9), ('Andrew', 18), ('Lucas', 28)]
```
### Looping Over Iterables

Working with multiple iterables is one of the most popular use cases for the `zip()` function in Python. For example, if you want to go through multiple lists, you may want to make use of the `zip()` function. Indeed, we can use the `zip()` function as an iterator of tuples, or any other iterable elements, which is a common operation in software development.

Here is an example of `zip()` being used to iterate over multiple arrays:

```python
employee_numbers = [2, 9, 18, 28]
employee_names = ["Candice", "Ava", "Andrew", "Lucas"]

for name, number in zip(employee_names, employee_numbers):
	print(name, number)
```
```python
Candice 2
Ava 9
Andrew 18
Lucas 28
```
In this example, our program iterates through the list of tuples that `zip()` returns, and divides them into two values: name and number. This makes it easy for us to iterate through multiple iterable objects at once. If we wanted to, we could use this to iterate through three or more iterable objects.

### Python Unzip

In our code, we have zipped various types of data. But how do we restore data to its previous form? If you have a list of tuples—or zipped values—that you want to divide, you can use the `zip()` function’s unpacking operator. This is an asterisk * used in conjunction with the `zip()` function.

Here is an example of the `zip()` unpacking operator in action:

```python
employees_zipped = [('Candice', 2), ('Ava', 9), ('Andrew', 18), ('Lucas', 28)]
employee_names, employee_numbers = zip(*employees_zipped)

print(employee_names)
print(employee_numbers)
```
Returns the following:

```python
('Candice', 'Ava', 'Andrew', 'Lucas')
(2, 9, 18, 28)
```

## Date & Time / Python `strftime()`

The `strftime()` method returns a string representing date and time using [date](https://www.programiz.com/python-programming/datetime#date), [time](https://www.programiz.com/python-programming/datetime#time) or [datetime](https://www.programiz.com/python-programming/datetime#datetime) object.

### Example 1: datetime to string using `strftime()`

The program below converts a `datetime` object containing current date and time to different string formats.

```python
from datetime import datetime

now = datetime.now() # current date and time

year = now.strftime("%Y")
print("year:", year)

month = now.strftime("%m")
print("month:", month)

day = now.strftime("%d")
print("day:", day)

time = now.strftime("%H:%M:%S")
print("time:", time)

date_time = now.strftime("%m/%d/%Y, %H:%M:%S")
print("date and time:",date_time)
```

When you run the program, the output will something like be:

 year: 2018
month: 12
day: 24
time: 04:59:31
date and time: 12/24/2018, 04:59:31

Here, year, day, time and date\_time are strings, whereas now is a `datetime` object.

### How `strftime()` works?

In the above program, `%Y`, `%m`, `%d` etc. are format codes. The `strftime()` method takes one or more format codes as an argument and returns a formatted string based on it.

1.  We imported `datetime` class from the `datetime` module. It's because the object of `datetime` class can access `strftime()` method.

    ![Import datetime module in Python](https://cdn.programiz.com/sites/tutorial2program/files/import-datetime.jpg)

2.  The `datetime` object containing current date and time is stored in now variable.

    ![datetime object containing current date and time](https://cdn.programiz.com/sites/tutorial2program/files/current-date-time.jpg)

3.  The `strftime()` method can be used to create formatted strings.

    ![Python strftime() example](https://cdn.programiz.com/sites/tutorial2program/files/python-strftime-format-1.jpg)

4.  The string you pass to the `strftime()` method may contain more than one format codes.

    ![Python strftime() example](https://cdn.programiz.com/sites/tutorial2program/files/python-strftime-format-2.jpg)

### Format Code List

The table below shows all the codes that you can pass to the `strftime()` method.

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| %a        | Abbreviated weekday name.                                                                                                                        | Sun, Mon, ...            |
| %A        | Full weekday name.                                                                                                                               | Sunday, Monday, ...      |
| %w        | Weekday as a decimal number.                                                                                                                     | 0, 1, ..., 6             |
| %d        | Day of the month as a zero-padded decimal.                                                                                                       | 01, 02, ..., 31          |
| %-d       | Day of the month as a decimal number.                                                                                                            | 1, 2, ..., 30            |
| %b        | Abbreviated month name.                                                                                                                          | Jan, Feb, ..., Dec       |
| %B        | Full month name.                                                                                                                                 | January, February, ...   |
| %m        | Month as a zero-padded decimal number.                                                                                                           | 01, 02, ..., 12          |
| %-m       | Month as a decimal number.                                                                                                                       | 1, 2, ..., 12            |
| %y        | Year without century as a zero-padded decimal number.                                                                                            | 00, 01, ..., 99          |
| %-y       | Year without century as a decimal number.                                                                                                        | 0, 1, ..., 99            |
| %Y        | Year with century as a decimal number.                                                                                                           | 2013, 2019 etc.          |
| %H        | Hour (24-hour clock) as a zero-padded decimal number.                                                                                            | 00, 01, ..., 23          |
| %-H       | Hour (24-hour clock) as a decimal number.                                                                                                        | 0, 1, ..., 23            |
| %I        | Hour (12-hour clock) as a zero-padded decimal number.                                                                                            | 01, 02, ..., 12          |
| %-I       | Hour (12-hour clock) as a decimal number.                                                                                                        | 1, 2, ... 12             |
| %p        | Locale’s AM or PM.                                                                                                                               | AM, PM                   |
| %M        | Minute as a zero-padded decimal number.                                                                                                          | 00, 01, ..., 59          |
| %-M       | Minute as a decimal number.                                                                                                                      | 0, 1, ..., 59            |
| %S        | Second as a zero-padded decimal number.                                                                                                          | 00, 01, ..., 59          |
| %-S       | Second as a decimal number.                                                                                                                      | 0, 1, ..., 59            |
| %f        | Microsecond as a decimal number, zero-padded on the left.                                                                                        | 000000 - 999999          |
| %z        | UTC offset in the form +HHMM or -HHMM.                                                                                                           |                          |
| %Z        | Time zone name.                                                                                                                                  |                          |
| %j        | Day of the year as a zero-padded decimal number.                                                                                                 | 001, 002, ..., 366       |
| %-j       | Day of the year as a decimal number.                                                                                                             | 1, 2, ..., 366           |
| %U        | Week number of the year (Sunday as the first day of the week). All days in a new year preceding the first Sunday are considered to be in week 0. | 00, 01, ..., 53          |
| %W        | Week number of the year (Monday as the first day of the week). All days in a new year preceding the first Monday are considered to be in week 0. | 00, 01, ..., 53          |
| %c        | Locale’s appropriate date and time representation.                                                                                               | Mon Sep 30 07:06:05 2013 |
| %x        | Locale’s appropriate date representation.                                                                                                        | 09/30/13                 |
| %X        | Locale’s appropriate time representation.                                                                                                        | 07:06:05                 |
| %%        | A literal '%' character.                                                                                                                         | %                        |

- - -