# Characters and Numbers in C

## Objective

Understand how C handles strings at the memory level, explore null terminators (\0), observe unintended behavior when strings are improperly formed, and practice working with numeric data types including float and double.

This lab reinforces memory awareness in C and precision handling for numeric output.

## Phase 1 – Creating Strings Two Different Ways

Starting code:

```C
#include <stdio.h>

int main() {
    char myString[] = "Hello, World!";
    puts(myString);

    char singleLetters[] = {'H', 'e', 'l', 'l', 'o', '\0'};
    puts(singleLetters);

    return 0;
}
```

Compile and execute:

```gcc -o output output.c; ./output```

Output:

```C
Hello, World!
Hello
```

What Is Happening?

```myString[] = "Hello, World!"``` automatically includes the null terminator (\0) at the end.

```singleLetters[] = {'H','e','l','l','o','\0'}``` requires manually adding \0.

In C, strings are arrays of characters that must end with \0. The null terminator signals where the string ends in memory.

## Phase 2 – Removing the Null Terminator

Removed '\0' from the array:

```char singleLetters[] = {'H', 'e', 'l', 'l', 'o'};```

Compile and execute:

```gcc -o output output.c; ./output```

Output:

```C
Hello, World!
HelloHello, World!
```

Why Did This Happen?

Without \0, ```puts()``` continues reading memory beyond the intended string boundary until it eventually finds a null byte.

Since ```myString``` was stored nearby in memory, the program continued printing adjacent memory content.

This is undefined behavior in C and demonstrates how:
- C does not protect you from memory overrun
- Proper string termination is critical
- Memory layout matters

## Phase 3 – Incorrect Array Size

Restored the null terminator, then changed the declaration:

```char singleLetters[3] = {'H', 'e', 'l', 'l', 'o', '\0'};```

Compile and execute:

```gcc -o output output.c; ./output```

Compiler warnings appeared:

```warning: excess elements in array initializer```

Output:

```C
Hello, World!
HelHello, World!
```

What Happened?

We declared space for only 3 characters, but attempted to store 6 characters including \0. The compiler warned us but still compiled the code.

This reinforces:
- Arrays must be properly sized
- The null terminator counts toward total string length
- Warnings are not errors and will not prevent the code from executing, but they shouldn't be ignored.

## Phase 4 – Working with Float Values

Starting fresh:

```C
#include<stdio.h>

int main() {
    float apples = 2.35;
    float bananas = 1.78;

    printf("Apples: $%f\nBananas: $%f\n", apples, bananas);

    return 0;
}
```

Compile and run:

```gcc -o output output.c; ./output```

Output:

```C
Apples: $2.350000
Bananas: $1.780000
```
Formatting Precision

Changed %f to %.2f:

```printf("Apples: $%.2f\nBananas: $%.2f\n", apples, bananas);```

Output:

```C
Apples: $2.35
Bananas: $1.78
```

%.2f formats floats to two decimal places to make the content more human readable for numbers.

## Phase 5 – Using Floats in Calculations

```C
#include<stdio.h>

int main() {
    float apples = 2.35;
    float bananas = 1.78;

    printf("3 x Apples and 2 x Bananas: $%.2f\n", (3 * apples + 2 * bananas));

    return 0;
}
```

Output:

```3 x Apples and 2 x Bananas: $10.61```

This demonstrates arithmetic operations within ```printf()```.

## Phase 6 – Using double for Higher Precision

There are 25.4 millimeters in one inch.

To calculate inches per millimeter:

```C
#include<stdio.h>

int main() {
    double inches_mm = 1 / 25.4;

    printf("Number of inches in 1mm: %.12f\n", inches_mm);

    return 0;
}
```

Output:

```Number of inches in 1mm: 0.039370078740```

```double``` provides greater precision than ```float```, and is useful when many decimal places are required (ie. stock numbers).

## Phase 7 – Scaling the Calculation

Modified code:

```C
#include<stdio.h>

int main() {
    double inches_mm = 1 / 25.4;

    printf("Number of inches in 5000mm: %.12f\n", 5000 * inches_mm);

    return 0;
}
```

Output:

```Number of inches in 5000mm: 196.850393700787```

This demonstrates:
- Variable reuse
- Multiplying floating point values
- Maintaining precision across calculations

## Key Concepts 
- C strings must end with \0, otherwise forgetting the null terminator causes undefined behavior
- Arrays must be correctly sized, C allows memory overrun without automatic protection
- float vs double precision differences - float is accurate up to 6 decimal places, double is accurate up to 15 decimal places
- ```printf()``` formatting controls numeric display
- Compiler warnings should be taken seriously. We can read them and treat them similar to a Python error, but they do not prevent the compiled code from executing

## Conclusion

This lab highlighted how C handles memory directly, especially with strings. Unlike higher-level languages like Python, C requires explicit management of string boundaries and array sizes.

The numeric section reinforced formatting control and precision handling using float, double, and format specifiers.

The biggest takeaway: C gives you power but it does not protect you from mistakes.
