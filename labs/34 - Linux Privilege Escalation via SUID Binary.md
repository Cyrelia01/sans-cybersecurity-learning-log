# Linux Privilege Escalation via SUID Binary

## Risk Context (GRC Perspective)

This lab demonstrates how misconfigured SUID binaries can allow unauthorized privilege escalation on Linux systems.

In this scenario, a binary owned by another user (poweruser) allowed a standard user to execute a shell with elevated privileges. This type of configuration error can lead to:
- unauthorized data access
- lateral movement within systems
- bypassing access control policies

For organizations, this represents a failure of least privilege and configuration management controls. Relevant governance frameworks include:

NIST SP 800-53
- AC-6: Least Privilege
- CM-7: Least Functionality

CIS Linux Benchmarks
- SUID/SGID file auditing and restriction

Understanding how these technical weaknesses occur helps GRC professionals evaluate system configurations and enforce secure baseline standards.

---

## Objective

The goal of this lab was to escalate privileges from a standard user account to another user account (`poweruser`) by identifying and exploiting misconfigured SUID binaries on a Linux system.

This exercise demonstrates how improperly configured file permissions can allow privilege escalation.

---

## Initial Access Attempt

The lab instructions indicated that the target account was a user named `poweruser`.

The first step was to determine whether access to the user's home directory was already permitted.

Command executed:

```bash
cd /home/poweruser/
```

Result:

```bash: cd: /home/poweruser/: Permission denied```

This confirmed that the current user account did not have permission to access the poweruser directory.

Since direct access was denied, a privilege escalation method needed to be identified.

### Searching for SUID Binaries

One common privilege escalation technique in Linux environments involves identifying SUID binaries.

SUID (Set User ID) files execute with the permissions of the file owner rather than the user running the program. If misconfigured, they can allow users to inherit elevated privileges.

To locate all SUID binaries on the system, the following command was executed:

```find / -perm -4000 2>/dev/null```

Explanation:

/ searches the entire filesystem

-perm -4000 identifies SUID files

2>/dev/null suppresses permission denied errors

The command returned a list of binaries located primarily within /usr.

### Identifying an Unusual Binary

While reviewing the results, a binary named cash appeared:

```/usr/bin/cash```

This command is not a standard Linux utility, which made it suspicious.

To inspect its permissions:

```ls -alh /usr/bin/cash```

Output:

```-rwsr-sr-x 1 poweruser root```

Permission breakdown:

rws indicates the SUID bit is set and the binary runs with the permissions of the file owner

Owner: poweruser

Group: root

This means executing this binary could allow a user to run processes as poweruser.

### Investigating the Binary

Next step was determining what the cash binary actually does.

Command executed:

```strings /usr/bin/cash```

This revealed that the binary was effectively a copy of the sh shell. This means it can spawn a shell interpreter.

Because the binary is owned by poweruser, running it with the correct options could allow privilege escalation.

### Executing the SUID Binary

To inherit the permissions of the binary owner, the following command was executed:

```/usr/bin/cash -p```

Explanation:

-p tells the shell to preserve privileges. This prevents the shell from dropping the elevated identity.

After execution, the shell prompt changed. This indicated the shell was now running under the identity of poweruser.

### Verifying Privilege Escalation

To confirm the privilege escalation worked, the same actions that previously failed were attempted again.

First test:

```cd /home/poweruser```

This command now succeeded.

Second test:

```touch test.txt```

The file was successfully created inside the directory.

This confirmed that the shell was now running with poweruser privileges.

### Result

Privilege escalation was successful. Access to the poweruser account was obtained through exploitation of a misconfigured SUID binary.

---

## Key Lessons

This lab demonstrated how small configuration mistakes can lead to privilege escalation.

- SUID binaries run with the permissions of the file owner.
-   Any SUID binary owned by another user is a potential escalation path.
- Non-standard binaries in system directories should always be investigated.
- Tools such as `find`, `strings`, and `ls` are critical for privilege escalation analysis.
