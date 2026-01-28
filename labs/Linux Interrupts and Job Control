# Linux Interrupts and Job Control Lab

## Overview
This lab introduces Linux interrupts and basic job control within the shell. It demonstrates how to suspend, resume, and manage running processes using keyboard shortcuts and built-in shell commands.

Understanding interrupts and job control is essential when working with long-running processes, monitoring tools, or when multitasking within a single terminal session.

---

## Lab Source
- **Type:** SANS Academy Lab  
- **Platform:** SANS Academy hosted system  

---

## Objective
Learn how to:
- Interrupt or suspend running processes
- Resume suspended processes in the foreground or background
- Switch between multiple suspended jobs

---

## Commands Used

- `top` — display running processes in real time  
- `Ctrl + C` — terminate a running process  
- `Ctrl + Z` — suspend a running process  
- `fg` — resume a job in the foreground  
- `bg` — resume a job in the background  
- `jobs` — list suspended/background jobs  
- `less` — view file contents one page at a time  

---

## Steps Performed

1. Start a running process: top
2. The terminal becomes “locked” into the running process. Suspend it using: Ctrl + Z
3. The terminal reports the process as stopped and returns control to the command line.
4. Resume the suspended process in the foreground: fg
5. top resumes and again occupies the terminal.
6. Suspend top again: Ctrl + Z
7. Launch another command: less /etc/passwd
8. Suspend the less command as well: Ctrl + Z
9. At this point, two processes are suspended. List them: jobs
10. Resume the less process using its job number: fg 2
11. Observe that you can now switch between suspended jobs and processes.

---

## Observations
- Ctrl + Z suspends a running process without terminating it.
- Multiple processes can be suspended at the same time.
- The jobs command displays all suspended and background jobs.
- Job numbers can be used with fg or bg to resume specific processes.
- The terminal can effectively multitask using job control.

---

## Key Takeaways
- Linux supports interrupting and suspending processes without killing them
- Ctrl + Z suspends, fg resumes in the foreground
- Multiple jobs can be managed within a single terminal
- Job control improves efficiency and situational awareness
