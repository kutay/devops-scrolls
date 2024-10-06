---
tags:
  - gcp
publish_folder: GCP
---

## Google Cloud's network

Google Cloud's networking is based on the highly scalable Jupiter network fabric and the high-performance, flexible Andromeda virtual network stack.
Jupiter fabrics can deliver more that 1 petabit per second of total bisection bandwidth, which is enough capacity for 100 000 servers to exchange data at a rate of 10 Gbps each.

Google Cloud is divided into regions, which are further subdivided into zones.
A region is a geographic area where the round-trip time (RTT) from one VM to another is typically under 1ms.

**Google Network Infrastructure**

Google network infrastructure consists of three main types of networks : 

- A data center network which connects all the machines in the network together
- A software-based private network WAN which connects all data centers together
- A software-defined public WAN for user-facing traffic entering the Google network

**Network service tiers**

Google Cloud is the first major public cloud to offer a tiered cloud network.
Two tiers are available : premium and standard tier

*Premium Tier* delivers traffic from external systems to Google Cloud resources by using Google's global network. This network consists of an extensive private fiber network with over 100 points of presence (PoPs) around the globe.
This means that incoming traffic from the internet enters Google's network at the PoP closest to the sending system. Within the Google network, traffic is routed from that PoP to the VM.
*Standard tier* delivers traffic from external systems to Google Cloud resources by routing it over the internet. The traffic leaves the Google network at its neareast PoP.

Standard tier offers a lower-cost alternative but can be limiting if you have a latency or performance sensitive app.

#### Connecting your network and Google's network

In most projects, you need to connect your on-premise network to Google Cloud's network.
There are several options. 

**Cloud VPN** is an easy and low-cost solution if you don't need high-throughput.
It lets you securely connect your on-premises network to your VPC network through an IPsec VPN connection in a single region.

**Cloud Interconnect** is a better solution if you need a more performant connection. 
You have two solutions : *Dedicated Interconnect* or *Partner Interconnect*.

**Network Connectivity Center** supports connecting different enterprise sites outside of Google Cloud by using Google's network as a wide area network (WAN).
It's a hub-and-spoke model for network connectivity management in Google Cloud.
Your on-premises networks connect to the hub via a HA VPN tunnel, VLAN attachments or router appliance instances.

See https://cloud.google.com/network-connectivity/docs/concepts for more information.



## Virtual Private Cloud (VPC)

Virtual Private Cloud (VPC) provides networking functionality for your cloud-based systems.
A VPC network is a global resource that consists of regional virtual subnetworks (subnets) in data centers, all connected by a global WAN (Google's SDN).

#fixme default vpc?
#fixme vpc firewall rules


#### Shared VPC

Shared VPC enables an organization to connect resources from multiple projects to a common VPC network so they can communicate with each other securely and efficiently using internal IPs from that network.
You specify a *host* project and attach *service* projects to it.
Eligible resources from service projects can use subnets in the Shared VPC

#### VPC Networking Peering

Google Cloud VPC Network Peering enables internal IP address connectivity across two VPC networks regardless of whether they belong to the same project or the same organization.
Traffic stays within Google's network and doesn't traverse the public internet.


#### VPC Packet Mirroring

Packet Mirroring is useful when you need to monitor and analyze your security status. 
It clones the traffic of specific instances and forwards it for examination. It captures all traffic (ingress and egress) and packet data.
Packet Mirroring copies traffic from *mirrored sources*  (VM instances) and sends it to a *collector destination* (instance group behind an internal LB). 
To configure Packet Mirroring, you create a *packet mirroring policy* that specifies the source and the destination.


## Cloud DNS

Cloud DNS is a managed, low-latency DNS service running on the same infrastructure as Google, which allows you to easily publish and manage millions of DNS zones and records.

#### Public DNS zones

Used for providing a namespace that is only visible inside the VPC or hybrid network environment. 

#### Private DNS zones

Used for providing a namespace that is only visible inside the VPC or hybrid network environment.

#### Split Horizon DNS

Used to serve different answers for the same name depending on who is asking : internal or external network resource

#### DNS Peering

All or a portion of the DNS namespace can be configured to be sent from one network to another. 


#### DNS Forwarding

#fixme 




## Load Balancing


Cloud Load Balancing is a fully distributed load-balancing solution that balances user traffic (HTTP(S), HTTS/2, gRPC, TCP/SSL, UDP, QUIC) to multiple backends to avoid congestion, reduce latency, increase security and reduce costs.
It can be externally accessible or internal to your VPC.


#### External Load Balancing

External HTTP(S) Load Balancing is a proxy-based Layer 7 load balancer that enables you to run and scale your services behind a single external IP address.

It can be configured in three modes : 

- Global external HTTP(S) load balancer
- Global external HTTP(S) load balancer (classic)
- Regional external HTTP(S) load balancer

https://cloud.google.com/load-balancing/docs/https



## Cloud CDN

#fixme


## Cloud NAT

#fixme



#publish/cloud/gcp
#quartz 