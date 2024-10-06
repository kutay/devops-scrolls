---
tags:
  - networks
publish_folder: Networks
---

## Introduction

**Network Address Translation (NAT)** is a process in which IP addresses in a packet's header are replaced with different IP addresses, typically used to map private IP addresses to a single public IP address or vice versa, allowing multiple devices on a local network to share a single public IP address for accessing external networks like the Internet.

**NAT** was primarily created as a short-term solution (in addition to [[CIDR]]) to the [[IPv4 address exhaustion]].
The long-term solution is [[IPv6]]

### NAT types

Based on whether source or destination IP addresses of packets are translated, NAT is classified into source NAT, destination NAT, and bidirectional NAT.

**Source NAT** translates only source IP addresses of packets and applies to the scenario where intranet users access the Internet.
When a packet sent from an intranet user for accessing the Internet reaches a NAT device, the NAT device translates the private IPv4 address of the packet into a public IPv4 address.

Based on whether port number translation is performed during source IP address translation, source NAT is categorized into the types : 

- NAT no-PAT : translates only IP addresses but not port numbers
- NAPT (PAT) : translates IP addresses and port numbers
- Easy IP : special type of NAPT and uses the public IP address of the outbound interface as the post-NAT IP address

**Destination NAT** translates only the destination IP addresses and destination port numbers of packets, and applies to scenarios where Internet users require to access intranet services.
When a packet sent from an Internet user for accessing intranet services reaches a NAT device, the NAT device translates the public IPv4 address of the packet into a private IPv4 address.

Destination NAT can be classified into the types below based on whether there are fixed mappings between pre-NAT and post-NAT IP addresses.

- static destination NAT
- dynamic destination NAT
- NAT server

**Bidirectional NAT** translates both source and destination IP addresses of packets. Bidirectional NAT is not an independent function. Instead, it is a combination of source NAT and destination NAT.


## NAT Types Defined in STUN

In the Session Traversal Utilities for NAT (STUN) protocol, NAT is classified into four types based on the mapping mode from private IP addresses and port numbers to the public IP addresses and numbers, as shown in the following figure.

![[Pasted image 20240210154039.png]]


- Full-cone NAT
- Restricted-cone NAT
- Port-restricted cone NAT
- Symmetric NAT



## NAT and IPv6


- **NAT64**
	- Provides a mechanism to allow IPv6-only hosts to communicate with IPv4 servers
	- It translates IPv6 addresses to IPv4 addresses and vice versa
- **NPTv6 (Network Prefix Translation)**
	- Used in IPv6 networks
	- Unlike traditional NAT which changes both the address and port, NPTv6 only changes the prefix of the IPv6 address, leaving the rest of the packet intact. This provides a simpler and more predictable mechanism for translation in IPv6 networks


## Resources

- RFC 1631 : The IP Network Address Translator (NAT)
	- https://datatracker.ietf.org/doc/html/rfc1631
- RFC 2663 : IP Network Address Translator (NAT) Terminology and Considerations
	- https://datatracker.ietf.org/doc/html/rfc2663

- https://info.support.huawei.com/info-finder/encyclopedia/en/NAT.html

#networking 
#quartz 