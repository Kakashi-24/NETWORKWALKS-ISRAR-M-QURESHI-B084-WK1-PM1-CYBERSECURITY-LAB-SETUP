# VMware Cybersecurity Lab Setup

**Networkwalks Cybersecurity Program — Batch B084**  
**Week 1 — Project Module 1**  
**Prepared by Israr M Qureshi**

## Project overview

This project documents the network configuration of a Kali Linux virtual machine using VMware Workstation. The work includes configuring NAT networking, assigning a static IP address, setting DNS servers and verifying internet connectivity.

The original lab brief references VirtualBox. VMware Workstation was used because Kali Linux was already installed on this platform.

## Objectives completed

- Configured VMnet8 as a NAT network.
- Set the lab subnet to 10.0.0.0/24.
- Assigned Kali Linux the static address 10.0.0.2/24.
- Configured the NAT gateway and DHCP address pool.
- Configured DNS servers.
- Verified gateway reachability, external connectivity and web access.

## Lab configuration

| Component | Configuration |
|---|---|
| Hypervisor | VMware Workstation |
| Guest operating system | Kali Linux |
| Virtual network | VMnet8 — NAT |
| Subnet | 10.0.0.0/24 |
| Subnet mask | 255.255.255.0 |
| Kali IP address | 10.0.0.2/24 |
| Default gateway | 10.0.0.254 |
| DHCP range | 10.0.0.128–10.0.0.200 |
| DNS servers | 1.1.1.1 and 8.8.8.8 |
| Network interface | eth0 |
| NetworkManager profile | Wired connection 1 |

## Implementation

### 1. VMware NAT network

VMnet8 was configured to use NAT with subnet 10.0.0.0 and subnet mask 255.255.255.0.

The Kali VM network adapter was set to NAT, with Connected and Connect at power on enabled.

### 2. Gateway and DHCP configuration

The NAT gateway was configured as 10.0.0.254.

The DHCP pool was set to 10.0.0.128–10.0.0.200, keeping Kali's static address outside the dynamically assigned range.

### 3. Kali static addressing

Kali was configured with static address 10.0.0.2/24, gateway 10.0.0.254 and DNS servers 1.1.1.1 and 8.8.8.8.

The configuration was checked using:

```bash
ip -br addr
ip route
nmcli -g IP4.DNS device show eth0
```

The output confirmed the static address on eth0, the default route and the configured DNS servers.

### 4. Connectivity verification

The following tests were performed:

```bash
ping -c 4 10.0.0.254
ping -c 4 1.1.1.1
ping -c 4 google.com
```

| Test | Observed result |
|---|---|
| NAT gateway | Four replies with 0% packet loss |
| External IP 1.1.1.1 | Four replies with 0% packet loss |
| google.com | Domain resolved and four replies visible |
| Web browsing | Kali website loaded successfully in Firefox |

## Evidence and report

The project report includes seven screenshots covering:

1. VMnet8 NAT subnet configuration.
2. Kali VM network adapter settings.
3. NAT gateway configuration.
4. DHCP address pool.
5. Kali IP address, route and DNS.
6. Connectivity tests.
7. Website access from Kali Firefox.

[Download the project report](NETWORKWALKS-ISRAR-M-QURESHI-B084-WK1-PM1-FINAL.docx)

## Key learning

This task demonstrated how NAT provides internet connectivity to a virtual machine and how static addressing, DHCP allocation, default gateways and DNS work together.

Keeping the static address outside the DHCP pool avoids overlapping address assignments.

## Conclusion

The networking configuration was successfully verified. Kali Linux operates on the required subnet with a static IP address and working internet connectivity.

This repository documents the networking portion of the lab demonstrated in the report.

---
**Author:** Israr M Qureshi  
**Batch:** B084  
**Task:** WK1-PM1
