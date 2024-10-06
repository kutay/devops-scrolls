---
publish_folder: Networks
---
In the IP header, there is a TTL field. 
When a packet is sent, the TTL field is set to a value of 64 (at least in Linux and macOS). When the packet reaches a router, the router decrements the TTL field by 1. If the TTL field reaches 0, the router drops the packet and sends an Time Exceeded Message back to the source computer. But if the TTL field is greater than 0, the router forwards the packet to the next router in the path.

A traceroute tool sends packets to a destination IP and with a time-to-live (TTL) set to 1, so that the first router the packets reach will send back an error (“time exceeded”). 
When the error returns, the traceroute tool records the first router’s identity and round-trip time, increments the TTL, and sends new packets, repeating this process until either 1) the last packet reaches the destination IP or 2) two sets of packets are dropped.

Traceroute relies on the ICMP (Internet Control Message Protocol) protocol. ICMP is a network layer protocol used for error testing. It has no associated transport protocol, running directly on the Internet Protocol (IP). When the TTL of a packet sent by the traceroute tool is exceeded, the router sends back an ICMP Type 11 (Time Exceeded Error) packet.





- https://www.cloudflare.com/learning/network-layer/what-is-mtr/
- https://sebastianmarines.com/post/journey-of-a-packet-exploring-networks-with-traceroute/

#quartz 