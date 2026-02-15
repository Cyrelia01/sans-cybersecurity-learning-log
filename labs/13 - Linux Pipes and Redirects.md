# Lab: Pipes and Redirects

## Platform
SANS Academy system

---

## Objective
Learn how to redirect command output, chain commands using pipes, and manage standard output and error streams in Linux.

---

## Commands Used
- `grep`
- `cat`
- `ps`
- `less`
- `find`
- Pipes (`|`)
- Output redirection (`>`)
- Error redirection (`2>`)

---

## Steps

1. Search the `/etc/passwd` file for a line containing `root` and redirect the output to a file named `test.txt` in the current directory: grep root /etc/passwd > test.txt
2. Print the contents of the file to confirm the redirect worked: cat test.txt - Result: Success
3. Run a process listing and pipe the output to grep to filter for the www-data user: ps aux | grep www-data
4. Search /etc recursively for files containing the term apache and redirect the results to results.txt: grep -r apache /etc > results.txt
5. Search /etc for files containing the term pass and pipe the output to less for review: grep pass /etc | less
6. Exit Less. Search the entire system for files containing the name pass, suppressing error messages by redirecting stderr to /dev/null: find / -iname "*pass*" 2>/dev/null

---

## Observations
- > redirects standard output to a file, overwriting it if the file exists.
- Pipes (|) allow output from one command to become input for another.
- less is useful for safely reviewing large outputs.
- Ctrl + Z suspends a running foreground process.
- Redirecting stderr to /dev/null helps reduce noise when scanning restricted directories.
- These techniques are foundational for log analysis, system administration, and forensic investigations.
