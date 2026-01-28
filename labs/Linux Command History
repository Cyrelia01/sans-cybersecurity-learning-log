# Linux Command History Lab

## Overview
This lab explores how Linux command history is stored and persisted across terminal sessions. Understanding how command history works is important for both usability and security, as sensitive commands may be written to disk and later recovered.

This exercise demonstrates how commands entered during a session are saved to the `.bash_history` file in the user’s home directory.

---

## Lab Source
- **Type:** SANS Academy Lab  
- **Platform:** SANS Academy hosted system  

---

## Objective
Learn how:
- Command history is recorded
- History persists between shell sessions
- `.bash_history` can contain sensitive information

---

## Steps Performed

1. Enter a command containing sensitive-looking text: echo "This command is a secret."
2. Display the current session’s command history: history
3. Refresh the lab page to reload the bash session. (Note: This step is important so the in-memory command history is written to disk.)
4. Display the contents of the bash history file: cat .bash_history
5. Observe that the previously executed command is present in the history file.

---

## Observations
- At the end of a terminal session, the command history stored in memory is written to: .bash_history
- Commands entered during the session persist across terminal restarts.
- Both the terminal history and .bash_history file must be cleared to remove sensitive data that was entered (i.e. passwords)

---

## Security Insight

While command history is extremely useful for productivity, it can also pose a security risk. Sensitive data such as passwords, tokens, or internal commands may be unintentionally stored in .bash_history.

From a defensive and forensic perspective, history files can be a valuable source of information when investigating system activity or potential misuse.

---

## Key Takeaways
- Linux stores command history in .bash_history
- History persists across shell sessions
- Sensitive information should never be entered directly into commands
- Command history can be both a usability feature and a forensic data source
