# Networking

# Visual Subnet Calculator link
https://www.davidc.net/sites/default/subnets/subnets.html

F5 is a networking device (often a load balancer) used to distribute traffic, improve application performance, and secure web applications.

“Security keys are cryptographic credentials used to authenticate and encrypt communication between systems. They can be symmetric or asymmetric and are essential in securing Wi-Fi, VPNs, APIs, SSH, and HTTPS traffic.”

############################## AWS VPC ##############################
## AWS VPC


VPC ---> Subnets (Servers) ---> RouteTables ---> IGW ---> User

In subnet we have, Servers & NAT-GW they connected to Route tables

What is the biggest network can be provided in AWS?
CIDR / 16 is the biggest network that can be provided by AWS with 65,536 IP's

Size of the any network depends on Classless inter domain Routing 

10.20.0.0/16
Means first 2 bits 10.20 are already occupied, we can use only 0.0 = 256*256 = 65536 IP's

VPC is a regional service in AWS

DHCP server - assigns a IP Network

# Router- Helps in a connecting two different networks 
Im AWS router is called as IGW - an entry point to access the internet 

# IGW/router forms a single private IP to connect to multiple devices in your VPC



One IGW can be attached to only one VPC also One VPC cannot have more than 1 IGW

# There will be a route table between IGW and Public subnet


Any one wants (from internet)to connect to server , it should not allow but if my server  should  connect to internet and downloads required packages
Then the concept of NAT gateway comes into picture 
NAT gateway enables the communication between private to Public 

Usually between 2 networks communication will not happen for this we need vpc peering.
# VPC Peering helps in communication between 2 VPC's

While enabling the peering, CIDR should be different of 2 networks

If we have 4 VPC's in same region or different region then you need to do a multiple (4) VPC peerings,
that where we have TRANSIT GATEWAY comes into Picture.
Transit gateway overcome the 4 VPC peerings & can have 1 Transit gateway in place.

# AWS Transit gateway -  
Define a Transit gateway & enroll 4 vpc's here
Connect Amazon VPC's, AWS accounts & on-premises networks to a single gateway.


#################### How Corporate Network works ##############################
## How Corporate Network works?

If Your Office has a On-Premise Network with VPN then people will connect go through VPN to connect servers.

Lets say if we want to connect AWS Account to On-premise then,

# AWS Direct connect
> AWS offfers AWS Direct connect to enable connectivity between On-Prem to AWS Account.
AWS Direct connect is very Costly & offers upto 400 gbps connection speed.
All depends on how much org can afford & what do you want to achieve.
Speed comes up with Cost. & It will offer Physical connection between Direct Connect location between On-Premises Data center.


AWS Point of Presence (PoP) offers dedicated connection between AWS Account & On-Premise.

# AWS Site-to-Site VPN service -  Its little cheaper then AWS Direct Connect
Transit gateway plays vital role in AWS S2S vpn service.

# AWS VPN software - For small companies & cheaper , based on no. of users & get license.


