---
publish_folder: Networks
---

## Introduction

CIDR stands for Classless Inter-Domain Routing. It replaced the **classful network** addressing architecture on the Internet.

It was introduced to improve the allocation of IP addresses and the efficiency of routing on the internet, addressing two main issues :

- **Address Space Exhaustion**: Prior to CIDR, IP addresses were allocated based on a classful network architecture (Classes A, B, and C), which was not efficient and led to rapid depletion of available addresses.
- **Routing Table Growth**: The increase in network connections led to larger routing tables, which strained the hardware and efficiency of routers.

Whereas classful network design for IPv4 sized the network prefix as one or more 8-bit groups, resulting in the blocks of Class A, B, or C addresses, under CIDR address space is allocated to Internet service providers and end users on any address-bit boundary.

CIDR is based on **variable-length subnet masking (VLSM)**, in which network prefixes have variable length (as opposed to the fixed-length prefixing of the previous classful network design).

**CIDR notation** is a compact representation of an IP address and its associated network mask.


## Resources

https://networkengineering.stackexchange.com/questions/19840/does-cidr-really-do-away-with-ip-address-classes

#publish 
#quartz 