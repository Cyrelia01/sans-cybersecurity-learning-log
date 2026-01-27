# Linux File Permissions Lab

## Overview
This SANS Academy lab focuses on understanding and modifying Linux file permissions. The exercise covers changing ownership and permissions for users and groups using `chown`, `chgrp`, and `chmod`.

The goal is to reinforce foundational Linux security concepts by practicing permission management on example files.

---

## Environment
- **Platform:** SANS Academy lab environment  
- **Operating System:** Linux (hosted within the lab)  
- **Access:** Browser-based virtual lab environment  

---

## Objective
- Understand Linux file ownership (user and group)  
- Learn how to modify permissions using `chmod`, `chown`, and `chgrp`  
- Practice verifying permission changes with `ls -l`  

---

## Steps Performed

1. Navigate to the lab directory: `cd /labs/Linux-File-Permissions/`
2. List the files in the directory with detailed permissions: `ls -l`
3. Observed three example files with various rwx permissions.
4. Remove all permissions for example-1.txt: `chmod a-x example-1.txt`
5. Verify changes with: `ls -l`
6. Permissions now show ----------
7. Attempt to give read permissions to user, group, and others using: `chmod a=r example-1.txt -r--r--r--`
8. Initial attempt with symbolic notation (-r--r--r--) did not apply; likely required numeric notation or root privileges.
9. Tried to change the owner to root: `sudo chown root example-1.txt`
10. Received error: -bash: sudo: command not found
11. Reflection: In the hosted lab environment, sudo is not available, so ownership changes may be restricted.
12. Successfully applied read-only permissions using numeric notation: `chmod 444 example-1.txt`
13. Verified using `ls -l`. Successful.
14. Grant write permission to the owner: `chmod 644 example-1.txt`
15. Verified using `ls -l`. Successful.
16. Modify permissions on example-2.txt to:
17.   Owner: read, write, execute
18.   Group: read, execute
19.   Others: no permissions
20. Used `chmod 750 example-2.txt`
21. Verified using `ls -l`. Successful.
22. Modify permissions on example-3.txt to:
23.   Owner: read-only
24.   Group: read, write, execute
25.   Others: execute only
26. Used `chmod 471 example-3.txt`
27. Verified using `ls -l`. Successful.

## Observations

1. Symbolic permission changes may fail if numeric notation or correct privileges are not used.
2. `ls -l` is critical to verify file permission changes.
3. Root privileges may be required in some environments to modify certain files (sudo not available in this lab VM).

## Key Takeaways

1. chmod can modify permissions using symbolic (rwx) or numeric notation.
2. chown and chgrp manage file ownership (user and group).
3. Verifying changes with `ls -l` ensures permissions are correctly applied.
