For, While, Nested Loops, and Conditional Patterns

## Objective

Practice building output using for loops, understand nested loops, apply conditional logic inside loops to generate patterns, and use while loops to iterate through lists and dictionaries.

## Environment
- Lab-based Linux container environment
- Integrated code editor and terminal
- Python interpreter available (python / python3)
- Source file: output.py

## Walkthrough

Part 1 – Basic For Loop Pattern

The initial goal was to build a string pattern using a for loop.

In the editor:

```
output = ""

for y in range(1, 10):
  output = output + "*"

print(output)
```

Output
*********

Observation:
- range(1, 10) generates numbers 1 through 9. The final called number in a sequence is not printed.
- On each iteration, "*" is concatenated to the output string.

The final result is 9 asterisks

Part 2 – Nested For Loops (Building a Box)

The next step introduced nested loops and newline characters.

```
output = ""

for y in range(1, 10):
  for x in range(1, 30):
    output = output + "*"
  output = output + "\n"

print(output)
```

Output
```
*****************************
*****************************
*****************************
*****************************
*****************************
*****************************
*****************************
*****************************
*****************************
```

Observations:
- Outer loop controls rows (y)
- Inner loop controls columns (x)
- After each row completes, "\n" moves to the next line

Result: 9 rows, 30 columns per row

Part 3 – Alternating Pattern Using Modulus

The pattern was modified using conditional logic:

```
output = ""

for y in range(1, 10):
  for x in range(1, 30):
    if (x % 2 == 0):
      char = "*"
    else:
      char = "-"
    output = output + char
  output = output + "\n"

print(output)
```

Output
```
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
```

Observations:
- x % 2 checks the remainder when dividing by 2.
  - Even numbers → remainder 0 → "*"
  - Odd numbers → remainder 1 → "-"

Since x resets each row, every row looks identical.

Part 4 – Creating a Checkerboard Pattern

To vary rows, y was included in the formula:

```
output = ""

for y in range(1, 10):
  for x in range(1, 30):
    if ((x + y) % 2 == 0):
      char = "*"
    else:
      char = "-"
    output = output + char
  output = output + "\n"

print(output)
```

Output
```
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
```

Observation:
- Including y offsets each row. Now the parity alternates by row, creating a checkerboard pattern.

Part 5 – While Loop with List

A list of cities was created:

```
cities = ['New York', 'London', 'Paris']

while cities:
    city = cities.pop(0)
    print("%s" % city)
```

Output
```
New York
London
Paris
```

Explanation:
- ```while cities:``` runs as long as the list is not empty.
- ```pop(0)``` removes and returns the first element.
- The list shrinks each iteration until empty.

This demonstrates:
- Truthy evaluation of non-empty lists
- List mutation during iteration
- Sequential processing

Part 6 – Converting List to Dictionary Objects

The list was changed to structured dictionaries:

```
cities = [
  {'name': 'New York', 'todo': 'Night-life'}, 
  {'name': 'London', 'todo': 'Culture'},
  {'name': 'Paris', 'todo': 'Food'}
]

while cities:
    city = cities.pop(0)
    print("%s" % city)
```

Output
```
{'name': 'New York', 'todo': 'Night-life'}
{'name': 'London', 'todo': 'Culture'}
{'name': 'Paris', 'todo': 'Food'}
```

This output is correct. While the output itself looks strange and appears to have errored, Python prints the dictionary representation exactly as stored.

There was no error — just raw data display.

Part 7 – Formatting Dictionary Output

To display the data more cleanly:

```
cities = [
  {'name': 'New York', 'todo': 'Night-life'}, 
  {'name': 'London', 'todo': 'Culture'},
  {'name': 'Paris', 'todo': 'Food'}
]

while cities:
    city = cities.pop(0)
    print("City: %s, To-do: %s" % (city['name'], city['todo']))
```

Output
```
City: New York, To-do: Night-life
City: London, To-do: Culture
City: Paris, To-do: Food
```

Explanation
- city['name'] accesses dictionary keys.
- %s placeholders inject values.

Data is now formatted rather than printed as raw structure.

## Conclusion

This lab progressed from simple iteration to structured data handling.

It reinforced:
- Loop mechanics
- Nested iteration
- Conditional pattern logic
- Data structure manipulation
- Formatted output of complex data types

Although the examples are simple, these mechanics underpin:
- Log parsing
- Automation scripts
- Data processing
- Pattern detection
- Security tooling
