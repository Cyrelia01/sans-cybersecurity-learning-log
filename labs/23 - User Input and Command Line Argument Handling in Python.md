User Input and Command Line Argument Handling in Python

## Objective

Implement interactive user input, process command line arguments using sys.argv, validate argument types, and handle runtime errors using structured input validation and exception handling.

## Environment
- Linux lab container
- Python interpreter (python / python3)
- Source file: output.py

## Part 1 – Capturing Interactive User Input

The initial task was to read user input into a variable named age and print it back to the screen.

Provided structure:

```Python
print("How old are you?")
print(">")

print("You are:")
print(age)
```

The first attempt added:

```Python
print("How old are you?")
print(">")
input()

print("You are:")
print(age)
```

This resulted in:

```NameError: name 'age' is not defined```

The issue was that input() returns a string, but the returned value was not assigned to a variable. Since age was never defined, Python could not reference it.

The next attempt introduced:

```Python
print("How old are you?")
print(">")
input()

age = input()
print("You are:")
print(age)
```

This created unexpected behavior. The program appeared to pause after the first input. The reason was that there were now two calls to input():

The first consumed user input but discarded it.

The second waited for new input to assign to age.

The correct implementation was:

```Python
print("How old are you?")
print(">")
age = input()
print("You are:")
print(age)
```

This successfully captured and displayed the user’s input.

## Part 2 – Parsing Command Line Arguments with sys.argv

The second portion of the lab introduced command line arguments.

The program structure included:
- import sys
- A predefined list of project names was stored in projects. The script required two positional arguments to define a slice range.

The program was executed as:

```Python
python output.py 5 10
```

Result:

```['Frost', 'Ginger', 'Hawk', 'Igloo', 'Jazz']```

Input Validation and Error Handling

Running:

```Python
python output.py A B
```

Produced:

```ValueError: invalid literal for int() with base 10: 'A'```

This occurred because the script attempted to convert non-numeric input into integers.

To prevent this, argument validation was added before conversion:

```Python
if not sys.argv[1].isdigit() or not sys.argv[2].isdigit():
sys.exit('You can only use integers for the arguments')
```

Now executing:

```python output.py A B```

Produces:

```You can only use integers for the arguments```

This prevents the script from reaching the conversion step and exits cleanly.

Alternative Error Handling – Try/Except

An alternative solution wrapped integer conversion in a try/except block:

```Python
try:
  start = int(sys.argv[1])
  end = int(sys.argv[2])
except:
  sys.exit('Oh dear')
```

However, because an .isdigit() validation occurs earlier in execution, invalid arguments such as A B trigger sys.exit() before reaching the try/except block.

This demonstrates execution flow:
- Python processes code sequentially.
- The first condition that triggers sys.exit() terminates the program immediately.

## Key Concepts
- input() captures interactive user input as a string
- Variables must be explicitly assigned before use
- sys.argv stores command line arguments as strings
- Explicit type conversion is required for numeric operations
- .isdigit() performs simple numeric validation
- try/except handles runtime conversion errors
- Python slicing uses half-open ranges [start:end]

Conclusion

This lab transitioned from interactive user input to structured command line argument processing.

It reinforced:
- the distinction between runtime input and CLI arguments
- the importance of explicit type conversion
- Defensive input validation strategies
- Controlled program termination

Understanding execution order

These patterns are foundational for writing reliable command line tools and form the basis for more advanced scripting and automation tasks.
