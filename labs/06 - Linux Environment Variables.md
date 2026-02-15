# Linux Environment Variables Lab

## Overview
This lab introduces Linux environment variables and demonstrates how they can be used to store and reference system paths for efficient navigation. Environment variables are a foundational Linux concept and are widely used by the operating system, applications, and users to control behavior and store configuration data.

This exercise focuses on viewing existing environment variables, using predefined variables, and creating a custom environment variable.

---

## Environment
- **Platform:** SANS Academy hosted lab environment  
- **Operating System:** Linux (lab-provided system)  
- **Access Method:** Browser-based virtual lab environment  

---

## Commands Used
- `printenv` — display all environment variables  
- `cd` — change directory  
- `pwd` — display current working directory  
- `export` — create or modify environment variables  

---

## Steps Performed

1. Display all current environment variables: `printenv`
2. Confirm the HOME environment variable exists. This variable stores the path to the current user’s home directory.
3. Navigate to the SSH configuration directory: `cd /etc/ssh`
4. Use the HOME environment variable to return directly to the home directory: `cd $HOME`
5. Confirm the current directory is the home directory: `pwd`
6. Result: Successfully returned to the home directory.
7. Create a custom environment variable named QUICKJMP to store a frequently accessed directory: `export QUICKJMP="/var/log"`
8. Verify the variable works by navigating to it: `cd $QUICKJMP`
9. Result: Successful navigation to /var/log.

---

## Observations
- Using cd $HOME behaves the same as using: cd ~
- Environment variables store values that can be referenced anywhere in the shell session.
- Predefined variables like HOME are available by default and are commonly used in scripts and commands.
- Custom environment variables can be created using export.
- Environment variables allow for quick navigation and reduce the need to repeatedly type long paths.

---

## Security Insight

Environment variables are commonly used by applications and scripts to store configuration settings. 

From a security perspective, understanding how environment variables work is important because sensitive information (such as credentials or tokens) can sometimes be stored in them. 
Improper handling or exposure of environment variables can lead to security risks.

---

## Key Takeaways
- Environment variables simplify system navigation and configuration.
- $HOME and ~ reference the same directory.
- Custom environment variables can improve efficiency during system administration.
