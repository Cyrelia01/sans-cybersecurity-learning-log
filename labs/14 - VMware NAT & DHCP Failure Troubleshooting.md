VMware NAT & DHCP Failure Troubleshooting

## Overview

During a Linux lab, I encountered a networking failure that prevented the VM from accessing the internet. This issue initially appeared to be DNS-related, but ultimately traced back to a problem with VMware’s NAT/DHCP services on the host system.

This document outlines the full troubleshooting process, errors observed, steps taken, and final resolution.

---

## Environment

Host: Windows (VMware Workstation)
Guest OS: Linux (APT-based distribution)
Network Type: NAT

## Initial Symptoms

While attempting to install packages, I began receiving the following error:

Temporary failure resolving 'archive.ubuntu.com'

This suggested a DNS issue.

---

## Troubleshooting process and steps

Phase 1 – Test Network Connectivity

1. Test DNS resolution by pinging google.com

Result: Message "Temporary failure resolving"

2. Test raw IP connectivity by pinging 8.8.8.8

Result: No response

Conclusion: If an external IP cannot be reached, the issue is not DNS. The VM had no outbound network connectivity.

Phase 2 – Review Recent Changes

Earlier, I had completed a lab that involved manually changing VM network settings. At this point, I realized:
- I had not restored the network settings back to their default configuration.

1. I reverted the VM network adapter back to: default NAT settings
2. After restoring default settings: ping 8.8.8.8

Result: Still no connectivity

Additional observations: 
1. No internet access
2. apt update failed
3. Network interface was up
4. DHCP requests appeared to be sent but no DHCP response received

Phase 3 – Verify DHCP Assignment

1. Checked IP configuration: ip addr

Result: No valid NAT-assigned IP address

2. Attempted DHCP renewal: sudo dhclient

Result: No address received

Conclusion:
The VM was requesting DHCP, but nothing was responding. This suggested the issue might be outside the VM.

Phase 4 – Investigate VMware Networking

At this stage, the problem appeared to be with:

- VMware NAT service
- VMware DHCP service
- Host-level virtual network configuration

Troubleshooting attempts included:

1. Power cycling the VM
2. Rebooting the host
3. Verifying NAT adapter configuration
4. Confirming correct network type (NAT)
5. Checking VMware network settings

None of these resolved the issue.

Phase 5 – Repair VMware Installation

Since VMware networking services appeared to be broken at the host level, I performed the following:

1. Downloaded the latest version of VMware Workstation (an upgrade from Player to Pro was required due to Player no longer being available)
2. Ran the installer
3. Restarted VMware
4. Immediately after boot checked IP configuration: ip addr

Result: Valid NAT IP address assigned

5. Connectivity tests: ping 8.8.8.8 and ping google.com

Result: Successful responses

6. Attempt to run apt Package manager again: sudo apt update

Result: Repositories resolved correctly. Updates completed successfully

---

## Root Cause

Earlier network configuration changes caused VMware’s NAT/DHCP services on the host to become misconfigured or non-functional. 

The VM itself was functioning correctly but was unable to receive:
- DHCP lease
- NAT routing
- DNS access

Repairing VMware restored the required networking services.

---

## Lessons Learned
1. Remember to change network settings back after purposefully changing them to something that shouldn’t work.
2. If you’re getting frustrated, step away and come back later. A fresh look helps.
3. If you can’t reach an external IP, the issue isn’t DNS — it’s network connectivity.
4. If DHCP requests go out but no address is received, the problem may exist outside the VM.
5. Sometimes troubleshooting sends you down a rabbit hole. At a certain point, repairing or upgrading the underlying software may resolve the issue faster.

---

## Key Commands Used
ping google.com
ping 8.8.8.8
ip addr
sudo dhclient
sudo apt update

---

## Final Outcome
- VMware networking repaired
- NAT and DHCP restored
- Internet connectivity functional
- Package installation working normally
