# Environment Variables in C (Parsing `environ` and Using `getenv`, `setenv`, `unsetenv`)

## Objective

Use C to explore environment variables in two ways:

1. Iterate through the process environment using the `environ` pointer and parse each `KEY=VALUE` pair.
2. Pull specific variables directly using `getenv()`, then set and unset a custom environment variable with `setenv()` and `unsetenv()`.

This lab reinforced string parsing, loop control, environment access patterns, and debugging compiler warnings that led to a runtime crash.

---

## Environment

- Lab-hosted Linux environment (container-style shell)
- C compiler: `gcc`
- Source file: `output.c`
- Executable: `output`

---

## Part 1 – Parsing Environment Variables Using `environ` + `strtok`

Starter code provided:

```c
#include <stdio.h>
#include <string.h>

extern char **environ;

int main() {
    int i = 0;
    int j = 0;
    while(environ[i]) {
        char *ptr = strtok(environ[i++], "=");
        while (ptr != NULL) {
            // Add your code here to output ptr...

            ptr = strtok(NULL, "");
            j++;
        }
    }

    return 0;
}
```

To validate what ptr contained, I inserted the following line where the comment indicated:

`printf("%s\n", ptr);`

Compiled and ran:

`gcc -o output output.c; ./output`

This printed environment variables in a long stream, where each KEY and VALUE appeared on separate lines, for example:

`SHELL
/bin/bash
PWD
/home/490026d6f045`
...

This worked, but it was difficult to read because there was no visual separation between each variable pair.

## Part 2 – Grouping Output Into Key/Value Pairs Using a Counter

The lab suggested using the j counter, since it increments each time the inner loop runs. I added a blank line every two outputs (every KEY + VALUE) by inserting:

```C
printf("%s\n", ptr);
if (j % 2 == 1) printf("\n");
```

After compilation and execution:

`gcc -o output output.c; ./output`

The output became much easier to scan, clearly grouping each environment variable into key/value pairs:

```
KEY: SHELL
VAL: /bin/bash

KEY: PWD
VAL: /home/490026d6f045

KEY: LOGNAME
VAL: 490026d6f045
...
```

This reinforced that `strtok()` was splitting each environment entry at the first = into a KEY, then returning the remainder of the line as VALUE.

## Part 3 – Reading Specific Variables with getenv() (Crash + Fix)

Next, the lab asked to output specific variables: USER, PATH, and HOME.

I replaced everything inside main() with:

```C
printf("USER: %s\n", getenv("USER"));
printf("PATH: %s\n", getenv("PATH"));
printf("HOME: %s\n", getenv("HOME"));

return 0;
```

When compiling and running:

`gcc -o output output.c; ./output`

I received multiple warnings and then a runtime crash:

`warning: implicit declaration of function 'getenv'
warning: format '%s' expects argument of type 'char *', but argument 2 has type 'int'
Segmentation fault (core dumped)`

At this point, the function `getenv()` was clearly being treated as unknown by the compiler. Without the proper header, C assumes an implicit return type, which caused the format mismatch warnings and then led to the segmentation fault at runtime.

Fix: include the correct header for environment functions.

I added:

`#include <stdlib.h>`

Then recompiled and ran again:

`gcc -o output output.c; ./output`

Successful output:

```C
USER: 490026d6f045
PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
HOME: /home/490026d6f045
```

This reinforced an important C concept: warnings are not always harmless. In this case, ignoring warnings would have meant ignoring the exact reason the program crashed.

## Part 4 – Setting and Unsetting an Environment Variable (setenv, unsetenv)

Finally, the lab asked to create an environment variable, print it, unset it, and print again to confirm the change.

I added:

```C
setenv("MYVAL", "my env var", 0);
printf("MYVAL: %s\n", getenv("MYVAL"));
unsetenv("MYVAL");
printf("MYVAL: %s\n", getenv("MYVAL"))
```
Then compiled and ran:

`gcc -o output output.c; ./output`

Result:

```C
USER: 490026d6f045
PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
HOME: /home/490026d6f045
MYVAL: my env var
MYVAL: (null)
```

This confirmed:

`setenv()` successfully created the variable for the current process environment. `unsetenv()` removed it. `getenv()` returned `(null)` after it was removed, meaning it no longer existed.

## Key Takeaways
- environ provides a raw list of environment strings in KEY=VALUE format.
- `strtok()` can be used to split KEY and VALUE, but output formatting matters for readability.
- `getenv()` is the clean, direct way to retrieve a specific variable.
- If a function is not declared (missing header), C may compile with warnings but behave incorrectly or crash at runtime.
- `setenv()` and `unsetenv()` allow modification of environment variables for the current process.
- `(null)` from `getenv()` is expected when a variable does not exist.
