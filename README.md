# Networking

# Visual Subnet Calculator link
https://www.davidc.net/sites/default/subnets/subnets.html

F5 is a networking device (often a load balancer) used to distribute traffic, improve application performance, and secure web applications.

“Security keys are cryptographic credentials used to authenticate and encrypt communication between systems. They can be symmetric or asymmetric and are essential in securing Wi-Fi, VPNs, APIs, SSH, and HTTPS traffic.”

############################## AWS VPC ##############################
## AWS VPC


VPC ---> Subnets (Servers) ---> routes --->RouteTables ---> IGW ---> User

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

If Private machines wants to talk to the internet , they need to talk over the NAT Gateway , NATG can  only be public if its created in Public Subnet which has access to internet.

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


## Here’s VPC in a way anyone can understand 👇

What is a VPC?

Think of VPC as your own private network inside AWS.
Just like your home has rooms, locks, WiFi, and rules —
A VPC has subnets, route tables, gateways, and security rules.
---

Components (Explained Like a Home Setup)

1. Subnets = Rooms in your house

* Public Subnet → Living Room (anyone can visit)
* Private Subnet → Bedroom (restricted access)
---

2. Internet Gateway (IGW) = Main Door

If you want public internet access → you need a door.
IGW is that door.
---

3. NAT Gateway = Security Guard

Instances in private subnet cannot go out directly.
NAT Gateway lets them access the internet *securely*
→ but still keeps them private.
---

4. Route Table = Google Maps

Decides where traffic should go.
Public subnet routes to IGW.
Private subnet routes to NAT.
---

5. Security Groups = Rules inside the house.

They control:

* Who can enter
* Who can leave
* Which service can talk to which

SG = Door Security
NACL = Compound Wall Security
---

🧠 Simple Example Setup
Public Subnet:
* ALB
* Bastion Host
* NAT Gateway

Private Subnet:
* EC2 instances
* EKS nodes
* RDS
* Microservices

Why separate?
Because **public = exposed, private = protected.
---

🚀 Golden Rule for DevOps Engineers**

90% of AWS issues come from wrong VPC design, misconfigured routes, or incorrect security group rules.**

If your app is not reachable, 3 things to check first:

1. SG rules
2. Subnet type (public/private)
3. Route table entries


Final Takeaway-
AWS VPC is not complicated.
It’s just networking — made cloud friendly.


## Bastion/Jump Host -
Bastion host is a special purpose server used to access servers in private network from external network
Bastillion is a tool to manage bastion hosts.

## expense-vpc - 
1. VPN can be hosted on AWS or AWS VPN
2. In our case, we are goin with bastion host to access private instances.

In expense-vpc, we have Load Balancer which is internet facing hosted on Public subnet having 2 regions (us-east-1 & us-west-2) .
Each subnet will have route table associated with IGW to access internet.



# Route Table (The Container)
A collection of rules (routes) for a Virtual Private Cloud (VPC).
Each subnet within your VPC is associated with one route table.
Controls traffic flow for all instances in its associated subnets. 

# Route (The Rule)
An individual entry within a route table.
Specifies a Destination (like an IP range, e.g., 0.0.0.0/0 for all internet traffic) and a Target (where to send it, e.g., an Internet Gateway, NAT Gateway, or another VPC).
When traffic leaves a subnet, the route table is consulted to find the best matching route. 
# Analogy
Route Table: Your GPS device's list of all possible roads.
Route: A specific instruction on that list, like "Turn left onto Main Street"