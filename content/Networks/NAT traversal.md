---
tags:
  - networks
publish_folder: Networks
---

## Introduction

[[Network Address Translation (NAT)]] typically uses private IP addresses on private networks with a single public IP address for the router facing the Internet.

While this is efficient for outbound connections (from the private network to the Internet), it complicates inbound connections (from the Internet to a specific device within the private network) because the NAT device does not inherently know how to forward unsolicited incoming packets to the correct internal device.


## NAT traversal techniques


- **NAT Port Mapping Protocol (NAT-PMP)** is a protocol introduced by Apple as an alternative to IGDP.
- **Port Control Protocol (PCP)** is a successor of NAT-PMP.
- [[UPnP Internet Gateway Device Protocol (UPnP IGD)]] is supported by many small NAT gateways in home or small office settings. It allows a device on a network to ask the router to open a port.
- [[Interactive Connectivity Establishment (ICE)]] is a complete protocol for using STUN and/or TURN to do NAT traversal while picking the best network route available. It fills in some of the missing pieces and deficiencies that were not mentioned by STUN specification.
- [[Session Traversal Utilities for NAT (STUN)]] is a standardized set of methods and a network protocol for NAT hole punching. It was designed for UDP but was also extended to TCP.
- [[Traversal Using Relays around NAT (TURN) ]]is a relay protocol designed specifically for NAT traversal.
- [[NAT hole punching]] is a general technique that exploits how NATs handle some protocols (for example, UDP, TCP, or ICMP) to allow previously blocked packets through the NAT.
	- UDP hole punching
	- TCP hole punching
	- ICMP hole punching
- [[Socket Secure (SOCKS)]] is a technology created in the early 1990s that uses proxy servers to relay traffic between networks or systems.
- [[Application-level gateway (ALG)]] techniques are a component of a firewall or NAT that provides configureable NAT traversal filters. It is claimed that this technique creates more problems than it solves.


## How it works

For some applications, we need to establish a peer-to-peer connection between clients. 
The problem is that with stateful firewalls and NAT devices, you can't easily do that.

Every firewall is configurable but usually, they allow all outbound connections and blocks all inbound connections. Then we add some specific exceptions for inbound connections like ssh.
Stateful firewalls remember what packets they have seen in the past and use that information to act on new incoming packets.
Basically, if your firewall sees a packet going from your device (`2.2.2.2:1234`) to a remote server (`7.7.7.7:5678`), it will then allow the remote server to send packets to your device, for a specific duration. 

The problem is that the the remote server is probably behind a firewall too, and it will block your packet. The good thing is that even if the packet is blocked by the remote firewall, your own firewall allowed it and it will accept future packets from the remote, even if the remote server never received the packet.
Both clients need to send each other packets to configure their respective firewall to accept future response packets. Even if the first packets will drop, the next ones will establish a two-way communication.

We also need to be cautious about keeping the connection alive, as firewall have limited memory and will usually forget about the session if no packets is received for some time (usually 30 seconds for UDP packets).

But we have a bigger problem : Source NAT (SNAT).
We are usually on private networks behind a NAT device that will map our private IP adress (192.168.x.y) to its public IP, and rewrite packets.

![[Pasted image 20240211000654.png]]

Why is that a problem? Because the peers don't know what the ip:port of their peer is. 
Worse, strictly speaking there is no ip:port yet as the NAT mapping only get created when outbound traffic towards the internet requires it.
We’re back to our stateful firewall problem, only worse: both sides have to speak first, but neither side knows to whom to speak, and can’t know until the other side speaks first.

![[Pasted image 20240211001024.png]]

We solve this deadlock with [[Session Traversal Utilities for NAT (STUN)]].
STUN relies on a simple observation: when you talk to a server on the internet from a NATed client, the server sees the public ip:port that your NAT device created for you, not your LAN ip:port.
So, the server can tell you what ip:port it saw. That way, you know what traffic from your LAN ip:port looks like on the internet, you can tell your peers about that mapping, and now they know where to send packets!

![[Pasted image 20240211001224.png]]

With most NAT devices, the combination of STUN and the simultaneous packet sending trick will work fine.
But there are some NAT devices that will create a completely different NAT mapping for every different destination that your device talk to. 
It means you can't use the same ip:port combination for all peers.

RFC 4787 calls the easy variant “Endpoint-Independent Mapping” (EIM for short), and the hard variant “Endpoint-Dependent Mapping” (EDM for short). There’s a subcategory of EDM that specifies whether the mapping varies only on the destination IP, or on both the destination IP and port.

![[Pasted image 20240211002004.png]]

One solution against that is to use relays. The classic way is a protocol called [[Traversal Using Relays around NAT (TURN)]].

The idea is that you authenticate yourself to a TURN server on the internet, and it tells you “okay, I’ve allocated ip:port, and will relay packets for you.” You tell your peer the TURN ip:port, and we’re back to a completely trivial client/server communication scenario.

Tailscale created another protocol : [[Detoured Encrypted Routing Protocol (DERP)]] which is a general purpose packet relaying protocol.

There are also several port mapping protocols : [[UPnP Internet Gateway Device Protocol (UPnP IGD)]], [[NAT-PMP]], and [[Port Control Protocol (PCP)]].





## Resources


https://tailscale.com/blog/how-nat-traversal-works



#networking 
#quartz 