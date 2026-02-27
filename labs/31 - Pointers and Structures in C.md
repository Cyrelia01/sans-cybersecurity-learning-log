# Pointers and Structures in C

## Objective
- Understand how pointers store and reference memory addresses
- Practice pointer arithmetic
- Define and use a struct with typedef
- Interpret compiler errors and correct structural mistakes

## Part 1 – Pointers and Memory Addresses

### Creating a Variable in Memory and a Pointer to It

Starting code:

```C
#include<stdio.h>

int main() {
   char message[] = "Hi there";
   char *msg_ptr = &message[0];

   printf("Address of message:\n%p\n\n", &message);
   printf("Address stored in msg_ptr:\n%p\n\n", msg_ptr);

   return 0;
}
```

Compile and run:

```gcc -o output output.c; ./output```

Example output:

```C
Address of message:
0x7ffceec4eb5f

Address stored in msg_ptr:
0x7ffceec4eb5f
```

#### Observation
- message is an array stored in memory
- &message[0] retrieves the address of the first character
- msg_ptr stores that address
- Both printed addresses match
- Running the program multiple times produced different memory addresses, confirming that memory allocation changes between executions

### Pointer Arithmetic – Walking Through Memory

Next, pointer arithmetic was introduced:

```
msg_ptr += 3;
printf("Fourth character of *msg_ptr: %c\n", *msg_ptr);

msg_ptr -= 2;
printf("Second character of *msg_ptr: %c\n", *msg_ptr);
```

Output:

```
Fourth character of *msg_ptr: t
Second character of *msg_ptr: i
```

#### Explanation
- ```msg_ptr += 3``` moves the pointer forward 3 bytes
- Since char is 1 byte, this moves forward 3 characters
- *msg_ptr dereferences the pointer and retrieves the value at that memory location

From "Hi there":
- Moving forward 3 positions lands on t
- Moving back 2 positions lands on i

This demonstrates precise, byte-level memory navigation.

## Part 2 – Creating a Struct with Typedef

### Step 1 - Defining the Structure

Initial struct definition:

```C
#include <stdio.h>

typedef struct {
  char *username; 
  char *email;
  char *password;
  int admin;
  
} User;
```

This defines the structure layout but does not assign values.

### Step 2 – Creating an Instance and Assigning Values

Initial attempt in main():

```C
User account_1;
account_1.Cyrelia
account_1.cyrelia@fakeemail.com
account_1.fakepassword123
account_1.0
```

#### Error Encountered

Compilation produced:

```
error: 'User' has no member named 'Cyrelia'
error: stray '@' in program
error: expected ';' before numeric constant
```

#### Why This Failed
- Cyrelia was interpreted as a struct member
- Email without quotes was treated as invalid syntax
- account_1.0 attempts to access a field named 0, which does not exist
- No semicolons were present

In C, struct fields must be accessed using declared member names and assigned string literals with quotes.

### Step 3 – Correct Member Assignment

Revised code:

```C
User account_1;
account_1.username = "Cyrelia";
account_1.email = "cyrelia@fakeemail.com";
account_1.password = "fakepassword123";
account_1.0
```

#### Error Encountered

Compiler error:

```error: expected ';' before numeric constant```

#### Root Cause

The line:

```account_1.0```

is invalid syntax. There is no field named 0.

### Step 4 – Final Correction

Corrected line:

```account_1.admin = 0;```

Full working program:

```C
#include <stdio.h>

typedef struct {
  char *username;
  char *email;
  char *password;
  int admin;
  
} User;

int main()
{
    User account_1;

    account_1.username = "Cyrelia";
    account_1.email = "cyrelia@fakeemail.com";
    account_1.password = "fakepassword123";
    account_1.admin = 0;

    printf("User Account: %s\n", account_1.username);
    printf("\tEmail: %s\n", account_1.email);
    printf("\tPassword: %s\n", account_1.password);
    printf("\tAdmin: %d\n", account_1.admin);

    return 0;
}
```

Output:

```C
User Account: Cyrelia
        Email: cyrelia@fakeemail.com
        Password: fakepassword123
        Admin: 0
```

## Key Concepts 

### Pointers
- & retrieves a memory address
- * dereferences a pointer
- Pointer arithmetic moves in units of the data type
- C allows direct memory traversal
### Structs
- A struct defines grouped data layout - similar to Class in Python programming
- typedef simplifies usage of the struct name
- Struct definitions declare fields only — no values
- Values must be assigned after creating an instance
- Member access uses the . operator

### Debugging Lessons
- Compiler errors clearly indicate incorrect member names
- String literals must be enclosed in quotes
- Struct members must match declared field names
- Error messages often point directly to incorrect syntax

## Conclusion

This lab reinforced low-level memory awareness in C. Unlike higher-level languages, C requires explicit handling of:
- Memory addresses
- Pointer arithmetic
- Data structure layout
- Proper syntax for member access

Incremental debugging clarified the distinction between defining a structure and initializing an instance, and demonstrated how pointer behavior directly reflects memory organization.
