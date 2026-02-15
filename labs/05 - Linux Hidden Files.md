# Linux Hidden Files

## Overview
This SANS Academy lab explores hidden files and directories in Linux and demonstrates how they can be discovered and accessed using command-line tools. Hidden files are commonly used for configuration and system purposes, but they can also be leveraged to conceal data.

This exercise reinforces file system awareness and basic investigative techniques in Linux.

---

## Environment
- **Platform:** SANS Academy hosted lab environment  
- **Operating System:** Linux (lab-provided system)  
- **Access Method:** Browser-based virtual lab environment  

---

## Commands Used
- `ls` — list directory contents  
- `ls -a` — list all files, including hidden files  
- `ls -la` — list all files with detailed permissions and ownership  
- `cat` — display the contents of a file  

---

## Steps Performed

1. Navigate to the lab directory: `cd /labs/Linux-Hidden-Files`
2. List visible files in the directory: `ls`
3. Only normal.txt was displayed.
4. List all files, including hidden files: `ls -a`
5. View the contents of the hidden file: `cat .secret-config-file`
6. Navigate into the hidden directory and list its contents using multiple commands on one line: `cd .hidden-dir; ls -a`
7. List all files in organized column format: `ls -la`  

---

## Observations

1. Hidden files and directories are identified by a leading . (dot).
2. The ls command does not display hidden files by default.
3. Command flags can be combined using a single - (e.g., ls -la), and the order of flags does not affect the result.
4. Multiple commands can be chained on a single line using a semicolon (;).
5. Hidden directories can contain both hidden and non-hidden files.

---

## Security Insight

Hidden files are often used to store configuration and temporary data. From a security perspective, they can also be used by attackers to conceal malicious scripts or sensitive information. Understanding how to identify hidden files is an important skill in system investigation and cybersecurity analysis.

---

## Key Takeaways

1. Always use ls -a or ls -la when investigating directories in Linux.
2. Hidden files are common in both legitimate system use and malicious activity.
3. Command chaining and flag combinations improve efficiency when working in the terminal.
