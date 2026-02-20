Python Functions and Conditionals

## Objective

Practice defining and calling Python functions, using default parameters, passing arguments dynamically, and implementing conditional logic with if, elif, and else statements.

## Environment
- Lab-based Linux container environment
- Integrated code editor and terminal
- Python interpreter available (python / python3)
- Source file: output.py

## Walkthrough

Part 1 – Defining and Calling Functions

The first portion of the lab focused on creating simple functions that return strings representing ingredients in hot drinks.

In the editor, the following functions were created:

```Python
def coffee():
  return "1 spoon of coffee"

def tea():
  return "1 tea bag"

def milk():
  return "1 splash of milk"

def water():
  return "Hot water"

def sugar(lumps=1):
  return str(lumps) + " lumps of sugar"
```

Making Drinks Using Function Calls

The functions were then combined inside print statements to simulate drink compositions:

```Python
print("White tea contains:\n", tea(), milk(), water())
print("Black coffee contains:\n", coffee(), water())
print("My coffee contains:\n", coffee(), sugar(4), water())
```

Output
White tea contains:  1 tea bag 1 splash of milk Hot water
Black coffee contains:  1 spoon of coffee Hot water
My coffee contains:  1 spoon of coffee 4 lumps of sugar Hot water

What This Demonstrated
- Each function uses return to send a value back when called.
- The str() function is required because integers cannot be concatenated directly with strings.
- Functions can be called inside other expressions.
- Multiple return values can be printed in sequence.
- Default parameters can be overridden (sugar(4)).
- Each function call executes independently and returns its defined value.

Part 2 – Conditionals and Dynamic Input

The next portion introduced conditional logic using if, elif, and else.

A function was created that greets customers differently depending on their name:

```Python
def breakfast_for_person(name):
  if (name == "Angus"):
    return "Hey Angus, Apple juice and a bagel?"
  elif (name == "Tamira"):
    return "Welcome Tamira, want an Espresso and a cake?"
  else:
    return "Hi " + name + ", what can I get you?"
```

The function was then called with three names:

```Pytho
print(breakfast_for_person('Angus'))
print(breakfast_for_person('Tamira'))
print(breakfast_for_person('Derek'))
```

Output
Hey Angus, Apple juice and a bagel?
Welcome Tamira, want an Espresso and a cake?
Hi Derek, what can I get you?

This demonstrated:
1. Functions Return Values
- Functions do not print automatically. They return values that must be printed or otherwise used.

2. Passing Arguments Dynamically
- The parameter name becomes a variable inside the function.
- Each time the function is called, name is assigned a new value. This allows the function to behave differently depending on input.

3. Conditional Logic Flow
- Python evaluates conditionals in order:
  - First if
  - Then elif
  - Finally else

## Key Takeaway
- While the example itself is simple, the underlying mechanics are foundational to:
  - Input validation systems
  - Authentication workflows
  - Role-based access logic
  - Automation scripts
  - Security tooling logic
- Conditionals form the decision-making backbone of programs.
- Functions allow reusable, modular design.

Although straightforward, this exercise builds the structural thinking required for more advanced scripting, automation, and security analysis workflows.
