# Python Interactive Input and String Formatting

## Objective

Practice executing Python scripts from the terminal, modifying source code in an editor, troubleshooting syntax errors, and understanding how formatted strings (f-strings) behave in Python.

This lab reinforces interpreter behavior, syntax precision, and basic debugging methodology.

---

## Environment

- Lab-based Linux container environment
- Integrated code editor and terminal
- Python interpreter available (`python` and `python3`)
- Source file: `output.py`

---

## Initial Execution – Running a Simple Python Script

In the editor pane, the following code was written and saved as `output.py`:

```python
print("Hello, World!")
```

Switched to the terminal and executed:
python output.py

The program ran successfully and displayed:
Hello, World!

For comparison, the script was also executed using:
python3 output.py

This also ran successfully, confirming that both python and python3 were available in the lab environment.

To extend the exercise beyond static output, the script was modified to prompt the user for input.

In the editor:
```python
name = input("What is your name?")
print(f "Hello {name}, pleasure to meet you.")
```

After saving and executing the command, the following was returned:

File "/home/.../output.py", line 2
    print(f "Hello {name}, pleasure to meet you.")
            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
SyntaxError: invalid syntax

The error indicated an issue on line 2. The problem was a subtle syntax rule in Python: there must be no space between the f and the opening quotation mark in a formatted string.

Incorrect:
```python
print(f "Hello {name}, pleasure to meet you.")
```

Correct:
```python
print(f"Hello {name}, pleasure to meet you.")
```

The script was also tested with the "f" prefix. This executed successfully, but printed incorrectly with:
Hello {name}, pleasure to meet you.

Without the f, Python treats the string as a literal. The {name} placeholder is not evaluated unless the string is explicitly defined as a formatted string (f-string).

The script was then corrected to:
```python
name = input("What is your name?")
print(f"Hello {name}, pleasure to meet you.")
```

## Key Concepts Reinforced
- Python is an interpreted language that evaluates syntax immediately.
- Minor formatting mistakes can result in syntax errors.
- F-strings require exact syntax: f"string".
- Variables inside {} are evaluated only within formatted strings.
- Debugging involves carefully reading error messages and identifying precise syntax issues.
- Iterating between editing code and executing it is a core part of development workflow.

## Conclusion

This lab progressed from executing a simple Python script to building an interactive program that accepts user input and dynamically formats output.

A small syntax mistake in the formatted string provided an opportunity to reinforce how Python interprets code and how strict syntax rules impact execution.

By identifying and correcting the formatting issue, the final script successfully:
1. Prompted the user for input
2. Stored the input in a variable
3. Inserted the variable into a formatted string
4. Printed a personalized response

This exercise strengthened foundational Python skills and reinforced structured troubleshooting practices within an interpreted programming environment.
