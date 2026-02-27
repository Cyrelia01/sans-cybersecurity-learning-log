# Strings and Numbers in Python

## Objective

Explore Python string methods and numeric operations, understand how built-in functions and dot notation work, identify type-related errors, and examine how Python handles mathematical operations and floating-point precision.

This lab reinforces string manipulation, data type behavior, operator precedence, and numeric edge cases in Python.

## Environment
- Lab-based Linux container environment
- Integrated code editor and terminal
- Python interpreter
- Source file: output.py

## Working with Strings

The variable len() was created with the value:

```Python
phrase = "Hello world"
print(len(phrase))
```

The output returned was ```11```.

This represents the total number of characters in the string, including the space between the words.

Next, the count() method was tested:

```Python
phrase = "Hello world"
print(phrase.count("l"))
```

The output returned was ```3```.

This does not count words or spaces. It specifically counts how many times the character "l" appears in the string. In "Hello world", the letter l appears three times.

Using split()

The variable was changed to:

```Python
phrase = "a-b-c-d-e-f-g-h-i-j-k-l-m-n-o-p"
print(phrase.split('-'))
```

The output was:

```['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p']```

The split() method separates a string based on a delimiter. In this case, the dash - was used as the separator, and Python returned a list containing each segment between the dashes.

This demonstrates how strings can be converted into lists for further processing.

Using replace()

The following code was tested:

```Python
phrase = "Hello Alex"
print(phrase.replace("Hello", "Goodbye"))
```

The output was:

```Goodbye Alex```

The replace() method substitutes one substring for another. While simple here, this functionality is commonly used for cleaning user input, sanitizing data, modifying logs, or dynamically generating content.

## Case Modification Methods

Using:

```Python
phrase = "Just a Test Sentence"
print(phrase.upper())
print(phrase.lower())
print(phrase.capitalize())
print(phrase.swapcase())
```

The output was:

```
JUST A TEST SENTENCE
just a test sentence
Just a test sentence
jUST A tEST sENTENCE
```

Notably, capitalize() only modifies the first character of the entire string, not the first letter of every word. To capitalize each word, Python provides a separate method: title().

String and Integer Concatenation Error

The following code was tested:

```Python
num_orders = 5
print("Number of orders:" + num_orders)
```

This produced the error:

```TypeError: can only concatenate str (not "int") to str```

Python does not automatically combine strings and integers. Explicit type conversion is required.

Two working solutions were tested:

```Python
print("Number of orders:", num_orders)
print("Number of orders: " + str(num_orders))
```

Both correctly produced:

```Number of orders: 5```

This works whether the integer is hardcoded or provided via user input, as long as it is converted to a string before concatenation.

## Working with Numbers

Basic multiplication was tested:

```print(888888 * 77)```

Output:

68444376

Division was tested:

```print(999 / 2)```

Output:

499.5

Order of Operations

The expression:

```print(1 + 2 * 3)```

Does not equal 9 because Python does follow standard mathematical order of operations (PEMDAS). Multiplication occurs before addition.

Therefore:

2 * 3 = 6
6 + 1 = 7

To force the addition first:

```print((1 + 2) * 3)```

Output:

9

Parentheses control evaluation order.

Floating Point Precision

Testing:

```print(0.2 + 0.4)```

Output:

0.6000000000000001

This is due to floating-point representation in binary. Many decimal numbers cannot be represented exactly in base-2, so small precision errors occur.

Using rounding:

```print(round(0.2 + 0.4, 1))```

Output:

0.6

The round() function requires a second argument to specify the number of decimal places. Without it, round() defaults to rounding to the nearest whole number.

Multiplying a String

The expression:

```print("1" * 77)```

Produced a long string of repeated 1 characters.

This is because multiplying a string by an integer in Python repeats the string that number of times.

To perform numeric multiplication instead:

```print(1 * 77)```

Output:

77

This highlights the importance of understanding data types and how operators behave differently depending on type context.

## Key Concepts Reinforced
- len() counts total characters, including spaces.
- count() counts specific character occurrences.
- split() converts a string into a list based on a delimiter.
- replace() substitutes substrings.
- capitalize() affects only the first character of a string.
- Python does not automatically concatenate strings and integers.
- Python follows standard mathematical order of operations.
- Floating-point arithmetic may produce small precision discrepancies.
- The * operator behaves differently for strings and integers.

## Conclusion

This lab explored practical string manipulation and numeric operations in Python, while highlighting several important behaviors:
- Methods accessed via dot notation
- Type-related errors
- Operator precedence
- Floating-point limitations
- Type-dependent operator behavior

Although foundational, these concepts are critical for writing reliable automation scripts, handling user input safely, and understanding how Python processes data internally.

This lab strengthened familiarity with Python’s built-in functions, string methods, numeric operations, and interpreter behavior.
