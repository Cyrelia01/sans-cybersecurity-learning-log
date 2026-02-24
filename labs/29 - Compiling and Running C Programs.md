# Compiling and Running C Programs

## Objective

Compile and execute basic C programs using gcc, understand how C source files become executables, and compare output behavior between puts() and printf().

This lab reinforces fundamental C program structure, compilation workflow, and output formatting differences.

## Environment
- Lab-based Linux container environment
- GCC compiler
- Source file: output.c
- Executable file: output

## Phase 1 – Compiling and Running a Basic C Program

Starting code:

```C
#include <stdio.h>

int main() {
    puts("Welcome to your first C program.");
    return 0;
}
```

To compile the program:

```gcc -o output output.c```

#### Explanation:

```gcc``` → GNU C Compiler

```-o``` output → Name the executable file output

```output.c``` → Source file

After successful compilation, run the program:

```C
./output
```

Output:

```Welcome to your first C program.```

## Phase 2 – Printing Custom Output with puts()

Modified code:

```C
#include <stdio.h>

int main() {
    puts("My first C program");
    return(0);
}
```

Compile and run:

```C
gcc -o output output.c
./output
```

Output:

```My first C program```

This confirms successful compilation and execution.

## Phase 3 – Comparing puts() and printf()

Next, replaced the single puts() line with:

```C
puts("A short tale:");
printf("%s ", "The");
printf("%s ", "quick brown");
```

Compiled and executed:

```gcc output.c -o output; ./output```

Output:

```
A short tale:
The quick brown
```

However, the command prompt appeared immediately after the printed text because:
- puts() automatically appends a newline (\n)
- printf() does NOT automatically append a newline
- Without \n, output continues on the same line, including the shell prompt

This demonstrates an important behavioral difference:
- puts() → prints string + newline
- printf() → prints exactly what you specify and does not create a new line

## Phase 4 – Extending Output Behavior

Modified code to:

```C
puts("A short tale:");
printf("%s ", "The");
printf("%s ", "quick brown");
puts("fox");
puts("jumps over the lazy dog");
```

Compiled and ran:

```gcc output.c -o output; ./output```

Output:

```C
A short tale:
The quick brown fox
jumps over the lazy dog
Why This Works
```

```printf("%s ", "quick brown");``` leaves the cursor after "quick brown ".

```puts("fox");``` begins printing exactly where the cursor currently is.

After printing "fox", puts() adds a newline.

The next puts() prints on the following line.

Important clarification:
- puts() does NOT insert a newline before printing. It prints text starting at the current cursor position, then appends a newline.

This explains why "fox" appears on the same line as "The quick brown", but "jumps over the lazy dog" appears on the next line

## Key Concepts
- C programs must be compiled before execution.
- ```gcc -o <output> <source.c>``` creates an executable binary.
- ```./output``` runs the compiled program.
- ```puts()``` automatically appends a newline.
- ```printf()``` requires explicit formatting (including \n).
- Output formatting depends on cursor position and newline behavior.

## Conclusion

This lab demonstrated the full compilation and execution process for C programs and highlighted important differences between puts() and printf().

Understanding output behavior is foundational in C, especially because formatting must be handled explicitly. This lab also reinforces the distinction between interpreted languages (like Python) and compiled languages (like C), where source code must first be translated into machine code before execution.
