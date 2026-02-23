Reading and Writing Files in Python

## Objective

Create a Python program that accepts repeated user input and writes that data to a text file. This lab reinforces file handling, loops, conditional logic, and persistent storage using Python’s built-in file operations.

## Walkthrough

The lab began with starter code that prints introductory instructions:

```Python
print('Enter places you would like to visit, they will be stored in a file.')
print('Input "quit" to quit.\n')

# Add your code here

print('Okay, goodbye!')
```

The objective was to insert logic that repeatedly asks for user input until the user types "quit".

### Phase 1 – Opening the File

To write data to a file, the following was added under the # Add your code here section:

```Python 
with open('travel-list.txt', 'a') as file:
```

The with open() statement opens the file with 'a' (append mode) so new entries are added without overwriting existing content. This is safer and recommended over the default 'r' mode or 'w' mode so you don't accidentally lose data.

Using this handler also allows Python to automatically close the file when finished.

### Phase 2 – Repeated User Input

Since the number of places entered is unknown, a while True loop was used:

```Python
while True:
    country = input("Country: ")
    if country == "quit":
        break
```

This loop continuously prompts the user for input until the loop is broken by entering "quit".

Initial test run:

```Python
python output.py
Enter places you would like to visit, they will be stored in a file. Input "quit" to quit.

Country: Japan
Country: Ireland
Country: Scotland
Country: England
Country: Korea
Country: quit
Okay, goodbye!
Input example:
```

The loop functioned correctly and exited when "quit" was entered.

### Phase 3 – Writing to the File

To store each valid entry, an else clause was added:

```Python
else:
    file.write(country + "\n")
```

The else ensures only valid entries (not "quit") are written. Each entry is followed by \n to place it on a new line.

Full implemented code:

```Python
print('Enter places you would like to visit, they will be stored in a file.')
print('Input "quit" to quit.\n')

with open('travel-list.txt', 'a') as file:
    while True:
        country = input("Country: ")
        if country == "quit":
            break
        else:
            file.write(country + "\n")

print('Okay, goodbye!')
```

### Phase 4 – Verifying File Contents

After running the program, the file was checked using:

```cat travel-list.txt```

The previously entered destinations were successfully appended to the file.

This confirms that data persisted after program execution, and append mode prevented overwriting previous entries.

## Key Concepts 
- ```with open()``` safely handles file opening and closing
- 'a' mode appends data rather than overwriting
- ```while True``` is useful when the number of iterations is unknown
- break exits a loop immediately
- File writing requires explicit newline characters for formatting
- Persistent storage allows data to exist beyond program runtime

## Conclusion

This lab demonstrated how to:
- Accept repeated user input
- Use loops and conditionals for flow control
- Write data to a file safely and efficiently by using append
- Verify persistent storage from the command line

The program now collects travel destinations interactively and stores them in a text file for future reference, reinforcing both Python fundamentals and practical file handling techniques.
