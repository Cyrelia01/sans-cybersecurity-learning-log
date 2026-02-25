# Technical Learning Notes & Reflections
### (Linux, Networking, Python, and C Foundations)

This document captures both the technical lessons and the thinking evolution that developed across the labs in this repository.

The detailed commands, step-by-step implementations, and outputs are documented within the labs/ directory.

This file answers a broader question:

What patterns have emerged across all of this work — technically and mentally?

## 1. My Approach to Hands-On Labs

Across all infrastructure and programming labs, I’ve developed a consistent workflow:
- Understand what the system is supposed to do before touching it
- Execute commands incrementally
- Observe output carefully — especially warnings and errors
- Validate assumptions before making additional changes
- Document what failed, why it failed, and how it was resolved

The shift has been from:

“Try commands until it works.”

to

“Understand the system state and isolate the layer that is broken.”

That change alone has significantly improved confidence and troubleshooting accuracy.

## 2. Foundational Linux & System Concepts

#### Files, Directories, and Visibility

Early labs reinforced that:
- Hidden files are not secured, just hidden from default listing
- Permissions matter more than visibility
- Configuration files are hidden for cleanliness, not secrecy

This reframed how I think about both:
- Forensic artifacts
- Attacker tradecraft
- Defender visibility

### Pipes, Redirects, and Data Flow

Using |, >, and 2> reinforced that:
- Output is data. All of it.
- Linux tools are composable
- Power comes from chaining small utilities together
- The ability to redirect, filter, suppress, and paginate output strengthened understanding of data flow at the shell level

### Processes and Job Control

Understanding foreground vs background processes clarified why a terminal “locks.”

Key realizations:
- Foreground processes control the session
- Ctrl+Z, bg, and fg allow control over execution state
- Jobs and processes are related but distinct

This improved confidence when interacting with live systems.

## 3. Virtualization & Networking: System State Over Commands

The VMware NAT and DHCP troubleshooting lab reinforced a major lesson:
- Most problems are caused by system state, not commands.

Symptoms included:
- “Temporary failure resolving”
- No outbound connectivity
- Failed package installations

Initial assumption: DNS issue.
Actual root cause: Network configuration misalignment in VM settings.

#### Troubleshooting process:
- Tested raw IP connectivity
- Verified DHCP behavior
- Checked interface configuration
- Compared against known working setup
- Corrected VM networking mode

#### Key lesson:

Always validate connectivity at the lowest layer first.

## 4. DNS Server Deployment & SERVFAIL Analysis

When deploying BIND as an authoritative DNS server, initial resolution returned:

```SERVFAIL```

### Root causes discovered:

1. .local Namespace Conflict

Ubuntu reserves .local for mDNS. Renaming zone from:

lab.local

to:

lab.test

resolved the conflict.

2. Firewall Configuration

Port 53 required both UDP and TCP allowance.

3. Client Misconfiguration

Verified DNS assignment using:
- resolvectl status
- Packet-Level Validation

Using Wireshark with:

udp.port == 53

Confirmed:
- Query packets sent
- Authoritative Answer flag (AA) set
- Response status NOERROR

This reinforced that:
- CLI validation confirms behavior
- Packet capture confirms protocol truth

## 5. Programming Foundations – Python

### Variables and Types

Python enforces type compatibility.

Attempting:

print("Orders: " + num_orders)

produced:

TypeError

Fix:

str(num_orders)

or

f"{num_orders}"

Lesson:

Be aware of implicit vs explicit type handling.

### Floating Point Precision

0.2 + 0.4

returned:

0.6000000000000001

Cause: Binary floating-point representation.

This reinforced that computers approximate decimal math at binary level.

### CLI Argument Failures

Running:

python output.py A B

produced:

ValueError

Fix options:
- Validate input using .isdigit()
- Use try/except where possible to allow the remainder of the code to continue running

Lesson:
- Never assume user input is valid.

### Threading Behavior

Sequential execution:

Two 5-second tasks = 10 seconds.

Threaded execution:

Two 5-second tasks = ~5 seconds.

Understanding join() clarified execution synchronization.

#### Key insight:
- Parallelism reduces wait time for I/O-bound tasks.

### Socket-Based Port Scanner

Building a TCP scanner reinforced:
- Socket creation
- TCP vs UDP distinction
- Port ranges (1–1024)
- Testing against known targets

Early syntax errors and incorrect tuple formatting highlighted precision matters in low-level networking code.

#### Critical reminder:

Scanning systems you do not own or have explicit permission to test can violate policies and laws.

## 6. C Programming – Memory & Precision

C labs revealed a major shift in thinking.

Null Terminator Behavior

Removing \0 caused Memory overrun and adjacent string printing. C does not protect string boundaries. This can cause undefined behavior and can be dangerous.

### Incorrect Array Size

Declaring:

char word[3] but storing 6 characters produced compiler warnings. The compiled code will still execute though.

#### Lesson:

Warnings are early signals of unsafe behavior.

### float vs double

Using double improved precision in decimal calculations.

Float is accurate up to 6 decimal places and is good for things like currency usage.

Double is accurate up to 15 decimal places and is good for stock pricing or similar. However, in most coding scenario's the use of double will probably not be required.

#### Lesson:

Choose data types intentionally based on required precision.

## 7. Cross-Lab Failure Patterns

Across Linux, networking, Python, and C labs, recurring root causes included:
- Incorrect assumptions
- Namespace conflicts
- Type mismatches
- Input validation failures
- Memory boundary errors
- Misunderstanding execution flow
- System state misconfiguration

Most failures were not complex.

They were subtle.

## 8. Troubleshooting Methodology Strengthened

Across labs, a consistent debugging framework emerged:
- Reproduce the issue
- Simplify environment
- Validate lowest layer first
- Read error messages closely
- Compare expected vs actual behavior
- Isolate variables
- Retest after each change

This replaced guessing with structured diagnosis.

## 9. Security Mindset Development

Repeated themes:
- Hidden files are organizational, not secure.
- Command history is productivity — and forensic artifact.
- Powerful tools are dual-use.
- Misconfiguration is often more dangerous than exploitation.

Seeing Linux and programming through a dual-use lens has been foundational.

## 10. Growth in Technical Confidence

Early reaction to errors:
- “Something is wrong.”

Current reaction:
- “Good — what layer is broken?”

Progress observed:
- Reading stack traces with confidence
- Recognizing memory vs syntax issues
- Understanding class vs instance behavior
- Thinking in terms of state, not commands
- Distinguishing interpreted vs compiled execution models

## 11. Documentation as Engineering Discipline

Maintaining this repository has reinforced that:

Documentation is not fluff. It is evidence of reasoning.

Good documentation:
- Exposes understanding gaps
- Demonstrates communication ability
- Makes work reproducible
- Shows troubleshooting maturity

### Closing Reflection

This training has reinforced:
- Curiosity over memorization
- Verification over assumption
- Understanding over syntax copying
- Patience over speed

Most importantly, confidence now comes from understanding why something works, and makes it easier to understand why it broke.
