## Variables and Data Types in Python

## Objective

Create and manipulate basic Python variables of different data types, print their values, inspect their types, and experiment with output formatting to better understand how Python handles data internally.

This lab reinforces foundational knowledge of variable assignment, data types, and syntax rules in Python.

## Environment
- Lab-based Linux container environment
- Integrated code editor and terminal
- Python interpreter
- Source file: output.py

---

## Creating Variables

In the code editor, four variables were created to represent different data types:

my_string = "I can write whatever I like here"
my_int = 1337
my_float = 42.1234
my_bool = False

Underneath the variable declarations, each variable was printed using:

print(my_string)
print(my_int)
print(my_float)
print(my_bool)

The program was executed in the terminal using python output.py.

The output was:

I can write whatever I like here
1337
42.1234
False

This confirmed that Python correctly stored and printed values for string, integer, float, and boolean types.

---

## Inspecting Data Types

To better understand how Python classifies each variable internally, the code was modified to print the type of each variable using the built-in type() function:

print(type(my_string))
print(type(my_int))
print(type(my_float))
print(type(my_bool))

Running python output.py produced:

<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>

This demonstrated how Python explicitly identifies each variable’s underlying data type.

---

## Experimenting with Multiple Statements on One Line

To experiment further, an attempt was made to print both the value and the type on a single line using the && operator:

print(my_string) && print(type(my_string))

This resulted in a syntax error:

SyntaxError: invalid syntax

The && operator is valid in shell environments (such as Bash) for conditional command execution, but it is not valid syntax in Python. Python does not use && to combine statements.

To correct this, the code was rewritten using separate print() statements:

print(my_string)
print(type(my_string))
print(my_int)
print(type(my_int))
print(my_float)
print(type(my_float))
print(my_bool)
print(type(my_bool))

The output confirmed both values and types were printed correctly.

---

## Key Concepts Reinforced
- Variables in Python do not require explicit type declarations.
- Strings require quotation marks, while integers and floats do not.
- Boolean values are written as True or False (case-sensitive).
- The type() function reveals how Python classifies stored data.
- Syntax from other environments (such as && from Bash) does not automatically apply to Python.
- Experimentation and error messages are essential parts of the learning process.

---

## Conclusion

This lab reinforced foundational Python concepts related to variable assignment and data types. While basic, the exercise provided practical reinforcement of:
- Data storage behavior
- Type inspection
- Syntax rules
- 
Interpreter feedback through error messages

The experimentation with && highlighted the importance of understanding language-specific syntax and not assuming behavior carries over from other environments.

Although simple, this lab strengthened familiarity with Python fundamentals that form the basis for more advanced programming and security automation tasks.
