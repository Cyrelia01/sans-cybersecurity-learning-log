Handling Exceptions with try-catch in Python

## Objective

Understand how Python handles runtime errors using exceptions, deliberately trigger errors, and implement structured exception handling using try, except, and else blocks.

This lab reinforces defensive programming, input validation, and graceful error handling.

## Environment
- Lab-based Linux container environment
- Python interpreter (python / python3)
- File: output.py

## Walkthrough

Initial Provided Code

The lab began with the following working program:

```Python
print('Enter 2 numbers and I\'ll divide them.')
print('Enter "q" to quit.\n')

while True:
    first_input = input('First Number: ')
    if first_input == 'q':
        break

    second_input = input('Second Number: ')
    if second_input == 'q':
        break

    answer = int(first_input) / int(second_input)
    print('The answer is: ' + str(answer))
    print('Let\'s try another...!\n')

print('Ok, bye!')
```

This program continuously prompts for two numbers as input from the user and then divides them. 

### Phase 1 – Confirm Working Behavior

Executed:

```python output.py```

Input:

First Number: 7
Second Number: 6

Output:

```The answer is: 1.1666666666666667```

The program functioned correctly under valid numeric input.

### Phase 2 – Triggering an Exception (ZeroDivisionError)

Tested invalid math operation:

First Number: 3
Second Number: 0

Output:

```ZeroDivisionError: division by zero```

This occurred because Python cannot divide by zero. The program terminated with a traceback error.

Modified the division logic to include a try-catch block:

```Python
try:
    answer = int(first_input) / int(second_input)
except ZeroDivisionError:
    print('Can\'t divide by zero! Let\'s try again.\n')
else:
    print('The answer is: ' + str(answer))
    print('Let\'s try another...!\n')
```

Re-ran the program and entered:

First Number: 3
Second Number: 0

Output:

```Can't divide by zero! Let's try again.```

The exception was successfully caught and handled gracefully without crashing the program.

### Phase 3 – Triggering a ValueError

Next test:

First Number: apple
Second Number: banana

Output:

```ValueError: invalid literal for int() with base 10: 'apple'```

This error occurred because Python attempted to convert non-numeric input to integers using int().

Expanded the exception handling to include ValueError:

```Python
try:
    answer = int(first_input) / int(second_input)
except ZeroDivisionError:
    print('Can\'t divide by zero! Let\'s try again.\n')
except ValueError:
    print('You must enter a number. Let\'s try again.\n')
else:
    print('The answer is: ' + str(answer))
    print('Let\'s try another...!\n')
```

Re-tested using:

First Number: apple
Second Number: banana

Output:

```You must enter a number. Let's try again.```

The program now successfully handles division by zero and non-numeric input without terminating execution.

## Key Concepts
- Exceptions occur during runtime when Python encounters invalid operations
- try allows execution of code that may fail
- except handles specific error types
- else runs only if no exception occurs
- Multiple except blocks can be used for different error types
- Structured error handling improves program stability and user experience

## Conclusion

This lab demonstrated how to:
- Identify runtime exceptions
- Interpret Python traceback messages
- Use try/except to prevent program crashes
- Handle multiple exception types within a single control structure
- Build more resilient and user-friendly programs
