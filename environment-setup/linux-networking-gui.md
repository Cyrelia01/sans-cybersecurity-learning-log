## Basic Linux Network Configuration (GUI-Based)

## Overview

This entry documents a self-directed practice exercise configuring basic IPv4 network settings on an Ubuntu Linux system using the graphical user interface (GUI). While this was not an official SANS lab, the exercise was informed by SANS Academy coursework and completed to reinforce foundational networking concepts.

The goal of this exercise was to become familiar with:

- Navigating Linux network settings via GUI
- Understanding DHCP vs. static IP configuration
- Observing how virtualized networking behaves in a lab environment

## Environment

- Virtualization Platform: VMware Workstation 17 Player
- VM Network Mode: NAT
- Operating System: Ubuntu Desktop (likely 22.04 LTS)
- Desktop Environment: GNOME

## Objective

Configure a manual IPv4 address on a Linux system using the GUI and observe the system’s network behavior after applying static network settings.

## Steps Performed

1. Launched Ubuntu Desktop inside the VMware virtual machine.
2. Opened Settings (via Show Applications due to menu layout).
3. Navigated to the Network tab.
4. Observed that only a Wired connection was available and marked as unplugged.
5. Selected the option to add a new network configuration.
6. Chose IPv4 settings and changed the method from Automatic (DHCP) to Manual.
7. Entered a manually assigned IP address
8. Researched whether additional fields were required for a static configuration.
9. Configured the following values:
    \\\ IP address: 192.168.1.10
    \\\ Netmask: 255.255.255.0
    \\\ Gateway: 192.168.1.1
11. Left DNS and Routes set to automatic.
12. Applied the configuration.
13. Opened Firefox to test basic connectivity.

## Observations

- The network configuration applied successfully with no warnings or errors.
- Despite the wired interface being marked as unplugged, internet access was still available.
- Firefox was able to browse external websites normally.

This behavior was unexpected given the use of manually assigned (non-validated) network values.

## Analysis & Learning Notes

The continued internet connectivity is likely explained by the VM’s NAT networking mode, which abstracts networking through the host system. Possible contributing factors include:

- VMware NAT handling routing regardless of guest IP values
- The manually configured interface not being the actively used interface
- Host-level networking overriding guest-level static configuration

## This highlighted an important learning point:

Virtualized networking can behave differently from physical systems, and successful connectivity does not always mean the configuration is functionally correct.

## Next Steps to further validate and expand this exercise:

- Test network behavior after rebooting the VM
- Disconnect and reconnect the network interface
- Compare GUI-based configuration with terminal-based configuration
- Explore differences between NAT, Bridged, and Host-only networking modes

## Key Takeaways

- Gained familiarity with Linux GUI-based network configuration
- Reinforced understanding of IPv4 static vs. DHCP addressing
- Identified the impact virtualization has on network behavior
- Developed stronger troubleshooting instincts by questioning unexpected outcomes
