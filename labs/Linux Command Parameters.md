# Linux Command Parameters Lab

## Overview
This lab introduces Linux command parameters (also called options or flags) and demonstrates how they modify command behavior. Understanding parameters is essential for effectively using Linux commands and interpreting their output.

This exercise focuses on identifying short-form and long-form parameters and chaining multiple parameters together.

---

## Lab Source
- **Type:** SANS Academy Lab  
- **Platform:** SANS Academy hosted system  

---

## Objective
Learn how to:
- Identify short and long command parameters
- Chain multiple parameters together
- Use parameters to control command output

---

## Steps Performed

1. Navigate to the `/etc` directory: cd /etc
2. View help information for the ls command: ls --help
3. Observe the large amount of output describing available parameters
4. List directory contents using multiple chained parameters: ls -alh
5. Observe the output: Files are displayed in a detailed list format and are shown in human-readable units

---

## Observations
- Single-letter parameters are preceded by a single dash (-).
- Multiple single-letter parameters can be chained together: ls -alh instead of: ls -a -l -h
- Full-word parameters are preceded by a double dash (--).
- Some commands support both short and long parameters, while others only support one form.

---

## Key Takeaways
- Linux commands can be modified using parameters
- Short parameters use a single dash (-)
- Long parameters use a double dash (--)
- Parameters can be chained for efficiency and clarity
