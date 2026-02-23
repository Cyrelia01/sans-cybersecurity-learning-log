Building a Simple TCP Port Scanner in Python

## Objective

Create a basic TCP port scanner using Python’s `socket` library to test whether common ports are open on a given host. This lab reinforced practical networking fundamentals (TCP connect scanning), Python loops, and interpreting connection results.

This lab was performed only against systems I control / am authorized to test. Any internal IPs used are masked below. (***** - sensitive)

---

## Environment

- Lab-based Linux container environment
- Python interpreter (`python` / `python3`)
- Library used: `socket` (standard library)
- Test targets:
  - Ubuntu Server VM IP: (***** - sensitive)
  - Localhost: `127.0.0.1`

---

## Attempt 1 – Misunderstanding the Goal (Listener vs Scanner)

I initially approached this as if I needed to create a listening server socket rather than a port *scanner*.

My first draft:

```python
import socket

sock = socket.socket(socket.SOCK_STREAM)
sock.bind(("0.0.0.0", 53489"))
sock.listen()
```

### What went wrong

Syntax error - I accidentally included an extra quote in the bind statement: 53489")) had a stray ".

Fix: remove the extra quote.

Incorrect socket initialization

```socket.socket()``` requires at minimum:
- an address family (IPv4 vs IPv6), and
- a socket type (TCP vs UDP)

The correct pattern for a TCP/IPv4 socket is:

```socket.socket(socket.AF_INET, socket.SOCK_STREAM)```

#### Wrong problem being solved

```bind()``` + ```listen()``` creates a server socket (a listener).

A port scanner is a client that attempts to connect to ports on a remote host. This was a good reminder that “socket programming” can mean either:
- building a service that listens for connections, or
- building a client that tests connections

In this lab, the goal was the second one.

## Attempt 2 – Building the Actual Port Scanner

I restarted with a cleaner plan:

1. Ask the user for a target IP address
2. Scan a standard port range (1–1024)
3. Attempt a TCP connection to each port
4. Print ports that accept the connection
5. Close the socket each iteration

### Implemented code:

```Python
import socket

print("Please enter an IP Address to scan.")
target = input("> ")

print("* Scanning: " + target + " *")

for port in range(1, 1025):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    result = s.connect_ex((target, port))
    if result == 0:
        print("Port: " + str(port) + " Open")
    s.close()
```

#### Why this works (what each part is doing)

- ```socket.socket(socket.AF_INET, socket.SOCK_STREAM)```
  - AF_INET means IPv4 addressing
  - SOCK_STREAM means TCP

```connect_ex((target, port))```
- Attempts a TCP connection to that port
- Returns 0 if the connection succeeds
- Returns a non-zero error code if it fails (connection refused, timeout, host unreachable, etc.)

This makes it easy to check success without raising exceptions

```for port in range(1, 1025)```
- Scans ports 1 through 1024 (inclusive)

This is a common “starter range” because it covers many well-known ports.

```s.close()```

Always closes the socket after testing a port to avoid resource exhaustion.

## Testing and Results

### Test 1 – Scanning an Offline Host

I used my Ubuntu Server VM IP as the target: (***** - sensitive)

Expectation:

Since the VM was powered off, I expected no ports to show open.

Observed behavior:

The scanner displayed the scanning banner but did not print any open ports.

I stopped the scan using Ctrl + C.

This matched expectations: if the host is offline/unreachable, no connection attempts succeed.

### Test 2 – Scanning Localhost (Successful Open Port)

To confirm the scanner worked end-to-end, I scanned localhost:

Input:

127.0.0.1

Output:

Port 80 reported as open.

This indicates a service was listening locally on TCP port 80.

Quick interpretation:

Port 80 is the standard port for HTTP (web traffic), which aligns with earlier labs involving a local web service.

## Key Concepts 
- A port scanner is a client connecting to a target, not a service listening for connections
- ```socket.AF_INET``` + ```socket.SOCK_STREAM``` creates an IPv4 TCP socket
- ```connect_ex()``` is convenient because it returns an error code instead of crashing the program
- “No open ports printed” can mean:
  - the host is offline/unreachable, or
  - the ports are closed/filtered, or
  - the scan is slow due to timeouts.
- Port 80 being open commonly indicates an HTTP service.

## Notes and Cautions

This scanning approach is a basic TCP connect scan and is meant for learning.

** Scanning systems you do not own or have explicit permission to test can violate policies and laws.**

Internal IPs and VM details are masked above. (***** - sensitive)

## Conclusion

This lab started with a false start (accidentally building a listener instead of a scanner), but that mistake helped clarify what TCP scanning actually requires: repeated client connection attempts across a port range.

The final script successfully:
- Accepts a target IP
- Iterates through a port range (1–1024)
- Identifies open TCP ports using ```connect_ex()```
- Confirms results through localhost testing

This gives me a working baseline scanner that I can extend later with improvements like timeouts, faster scanning, and better output formatting.
