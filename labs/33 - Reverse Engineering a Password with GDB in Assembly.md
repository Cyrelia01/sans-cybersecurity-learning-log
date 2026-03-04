# Reverse Engineering a Password with GDB in Assembly

## Objective

The goal of this lab was to reverse engineer a compiled binary using GDB in order to determine the correct password required for successful program execution.

The binary had no debugging symbols, requiring analysis at the assembly level.

---

## Initial Reconnaissance

Navigated to the lab directory:

```bash
cd /labs/Linux-gdb-Lab2
ls
```
Two executables were present:
- lab
- lab2

This exercise focused on lab.

## Launching GDB

Started the debugger: `gdb ./lab`

Checked available functions: `info func`

Important functions discovered:
`string_reverse`
`string_compare`
`main`
`fgets@plt`
`printf@plt`

This immediately suggested:
- User input is collected using `fgets`
- The input is reversed and compared against a stored value

### Analyzing main()

Disassembled main: `disas main`

Key instructions identified:

call   fgets@plt
call   string_reverse
call   string_compare

This confirmed the program flow:
- Prompt user
- Read input
- Reverse input
- Compare reversed input to expected value and print WIN or LOSE

### Setting Breakpoints

Set breakpoints at:

`break *main`
`break *string_compare`
`run`

The program stopped at main, then continued until it prompted for input.

Entered a test password:

something

Execution stopped at `string_compare`.

### Inspecting Registers and Stack

This binary was 32-bit, confirmed by use of eip, esp, etc.

On 32-bit systems, function arguments are passed via the stack.

The first argument is at: `*(char**)($esp+4)`

The second argument is at: `*(char**)($esp+8)`

Examined both: `x/s *(char**)($esp+4)`

Output:

`"\ngnihtemos"`

This revealed:
- The user input had been reversed.
- "something\n" became "\ngnihtemos".

Examined the second argument: `x/s *(char**)($esp+8)`

Output:

`"\nc&Cnz5B^@0"`

This was the stored comparison string.

### Reverse Engineering the Password

Since the program compares: `reverse(user_input) == stored_value`

To determine the correct password we need to reverse the stored value.

Stored value: `c&Cnz5B^@0`

Reversed: `0@^B5znC&c`

This must be the required password.

### Confirming the Solution

Exited and ran the binary normally:

`gdb ./lab`

Entered:

`0@^B5znC&c`

Program output:

`You WIN!`

Success!

## Observations and Lessons Learned
1. Assembly Reveals Program Logic

Even without debugging symbols, the control flow clearly showed:
- Input
- Transformation
- Comparison
- Conditional branch

Understanding this structure made reversing straightforward.

2. Newline Behavior of fgets

fgets() retains the newline character.

When reversed, the newline becomes the first character. This is why both inspected strings began with \n. This detail is critical when debugging string logic.

3. Understanding Stack-Based Argument Passing

Because this was a 32-bit binary:
- Arguments are passed on the stack.
- `$esp+4` and `$esp+8` hold the first and second arguments.

Knowing this allowed direct inspection of the compared values.

4. Breakpoint Persistence Issue

At one point, a breakpoint was accidentally set inside libc:

Breakpoint 3 at 0xf7d78519

On restart, GDB produced:

Cannot insert breakpoint 3.
Cannot access memory at address 0xf7d78519

This occurred because the address was inside a shared library and address space layout randomization caused it to shift between runs.

The fix was restarting GDB cleanly and setting breakpoints only inside the program’s code.

## Final Takeaways
- Always analyze control flow first.
- Identify transformation functions.
- Break at comparison points.
- Inspect arguments directly rather than guessing.
- Understand calling conventions for your architecture.
- Newline handling matters in string comparisons.

Most importantly:

The simplest strategy is often the most effective.
Break at the comparison and inspect both arguments directly.
