# Self-Directed Practice: Installing Software Using Package Managers (RHEL)

## Overview
This self-directed exercise focuses on installing, updating, validating, and managing software packages on a Red Hat Enterprise Linux (RHEL)-based system using `dnf` and `rpm`.

The goal of this practice was to reinforce understanding of:
- Package installation and removal
- System and package updates
- Package verification and rollback
- RPM queries and validation

This was not an official SANS lab, but a hands-on exercise completed to deepen familiarity with Linux package management workflows with various distributions, specifically RedHat Enterprise Linux (RHEL).

---

## Environment
- **Distribution:** RHEL-based Linux system
- **Package Manager:** `dnf`
- **Package Utility:** `rpm`

---

## Lab Steps

1. Installed Wireshark using the `dnf` package manager. The `-y` flag was used to automatically accept prompts: dnf -y install wireshark
2. Confirmed the installation was successful by listing the package: dnf list wireshark
3. Checked for available updates specifically for Wireshark: dnf list updates
4. To ensure the entire system was up to date, ran a full update: dnf update
5. Observed that the git package required an update. Chose not to use the -y flag in order to review prompts and output: dnf update git
6. After updating Git, ran a full system update again to ensure all updates were completed: dnf -y update
7. Removed the Apache HTTP Server (httpd) package: dnf -y remove httpd
8. Verified removal by listing the package: dnf list httpd
The package now appeared as available instead of installed, confirming successful removal.
9. Review DNF History: dnf history
10. Rolled back the system to a prior state before the removal of httpd: dnf -y history rollback 8
11. Locate Installed Files for Wireshark: rpm -ql wireshark
12. Attempted to view installation scripts for the httpd package: rpm -q --scripts httpd
At this point, it became clear that the rollback target was incorrect and the deletion history had not been fully restored.
13. Performed a second rollback using a different transaction ID: dnf -y history rollback 7
After this rollback, the installation scripts for httpd were accessible as expected.
14. Reviewed the Wireshark changelog: rpm -q --changelog wireshark
15. Validated the Wireshark installation: rpm -V wireshark
The output indicated that /usr/bin/wireshark was missing.
16. Reinstalled the package to correct the missing binary: dnf -y reinstall wireshark
17. Verified that the Wireshark binary was present and properly labeled: ls -alZ /usr/bin/wireshark

---

## Observations & Lessons Learned
1. dnf history and rollback are powerful tools, but selecting the correct transaction ID is critical.
2. Package verification with rpm -V is an effective way to detect missing or altered files.
3. Rollbacks can impact package scripts and validation results if not carefully applied.
4. Reinstallation is often the fastest and cleanest way to resolve integrity issues.

This exercise reinforced how Linux package managers maintain system state and how administrators can audit, repair, and roll back changes when needed.
