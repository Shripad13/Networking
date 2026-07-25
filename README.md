# Networking

# Visual Subnet Calculator link
https://www.davidc.net/sites/default/subnets/subnets.html

F5 is a networking device (often a load balancer) used to distribute traffic, improve application performance, and secure web applications.

“Security keys are cryptographic credentials used to authenticate and encrypt communication between systems. They can be symmetric or asymmetric and are essential in securing Wi-Fi, VPNs, APIs, SSH, and HTTPS traffic.”

############################## AWS VPC ##############################
## AWS VPC


VPC ---> Subnets (Servers) ---> routes --->RouteTables ---> IGW ---> User

In Subnet we have 2 types
1. Public Subnet - connected to IGW (internet gateway)
2. Private Subnet - not connected to IGW


In subnet we have, Servers & NAT-GW they connected to Route tables

What is the biggest network can be provided in AWS?
CIDR / 16 is the biggest network that can be provided by AWS with 65,536 IP's

Size of the any network depends on Classless Inter Domain Routing (CIDR) notation

10.20.0.0/16
Means first 2 bits 10.20 are already occupied, we can use only 0.0 = 256*256 = 65536 IP's

VPC is a regional service in AWS

DHCP server - Dynamically assigns a IP Network to the instances launched in VPC

# Router- Helps in a connecting two different networks 
Im AWS router is called as IGW - an entry point to access the internet 

# IGW/router forms a single private IP to connect to multiple devices in your VPC



One IGW can be attached to only one VPC also One VPC cannot have more than 1 IGW

# There will be a route table between IGW and Public subnet


Any one wants (from internet)to connect to server, it should not allow but if my server should connect to internet and downloads required packages
Then the concept of NAT gateway comes into picture 
NAT gateway enables the communication between private to Public 

If Private machines wants to talk to the internet , they need to talk over the NAT Gateway , NATG can only be public if its created in Public Subnet which has access to internet.

Usually between 2 networks communication will not happen for this we need vpc peering.
# VPC Peering helps in communication between 2 VPC's

# While enabling the peering, CIDR should be different of 2 networks

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
* Application Load Balancer (ALB)
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
2. In our case, we are going with bastion host to access private instances.

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

## 
# Subnets - 
Divides VPC into smaller segments
Assigned to spacific availability zones.

# NAT Gateway 
Enables private subnet access to the internet
Prevents direct inbound access.

# Internet Gateway 
Provides internet access to instances
Required for public VPC access

# Security Groups
Acts as firewall for instances
Controls inbound & outbound traffic

# Network ACLs
Filetrs traffic at the subnet level
Provides inbound & outbound rule-based filtering

# ELastic IP -
Static Public IP for cloud instances
Can be remapped between instances

# Flow logs
Captures detailed network traffic data.
Helps with monitoring & troubleshooting

# Endpoints
Provides private access to AWS services
Eliminates need for public internet access

# #############################################################################################
AWS VPC is a regional resources.
In VPC we have subnet range of /16 to /28 for IPv4 only 
There is a Soft limit of 5 VPC's per region, per account.

VPC's use private address space that means they are NOT publicly resolvable and can access over the internet.
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16

# Default VPS Points 
Within a Default VPC's you will be having the PUBLIC IPv4 CIDR so that is publicly accessible over the internet.
THis is the main reason to avoid using the default VPC.
Default VPC automatically allows the internet  access.
In Default VPC, Under NACL's All traffic is allowed in outbound & inbound rules.
DHCP options - will have 
Domain Name- ec2.internal
Domain name servers - AmazonProvidedDNS

Subnet - 
In Subnet you can see IPv4 CIDR range
Also you can see *Available IPv4 address*

Everywhere you will refer the VPC ID for example in scripting or IaC

# Is route tables are stateful or stateless in AWS?
AWS Route Tables are neither stateful nor stateless.
A Route Table's only job is to determine where to send traffic based on the destination IP address. It does not track connection state or allow/deny traffic.
Route Tables don't allow or deny traffic.


EC2 in private Network connects to RDS privately, what actions needs to perform for this?




# symmetric vs asymmetric encryption
Symmetric encryption uses a single shared key to both lock (encrypt) and unlock (decrypt) data. Asymmetric encryption uses a mathematically linked key pair: a public key to encrypt and a private key to decrypt.

# VPC Review
1. Logically isolated netowrk where you can define your own configs
2. Private IPV4 is require, IPV6 is optional
3. Valid CIDR's are 10.0.0.0  172.16.0.0, 192.168.0.0 
4. IPV4 CIDR must be between /16 & /28
5. VPC's are regional resource - 5vpc per region

Default Resources within Custom VPC's
1. DHCP Option sets to configure DHCP options like domain names, NTP servers, DNS servers
2. Main route table (default) witha primary local route 
3. Main NACL (default) with 2 simple rules - 2 separate for inbound & outbound rules
   

# VPC Internet Gateways
Horizontally scaled & highly available VPC component that allows communication between your VPC and the internet.
Supports both Ipv4 & Ipv6 traffic
Automaticaaly scales for traffic & offers  high availability
Enables public subnet resources to connect to the internet
Give you  target in your VPC for internet -routable traffic to flow through
Create seprately from the VPC & only attachable to single VPC

# VPC subnets
Range of IP addresses within your VPC for hosting resources
Subnets are bound to a single AZ
Subnets support IPv4 & Ipv6 also dual stack (4&6 at the same time)
4 types of subnets - Public  Private , VPN only, isolated 

AWS reserves 5 IP addresses per subnet.
Example - /28 CIDR subnet
Only 11 (16-5) have useable IP addresses

# Reserved Subnet IP's
VPC CIDR: 10.0.0.0/16
Subnet CIDR: 10.0.0.0/24

Network address: 10.0.0.0
VPC Router: 10.0.0.1
VPC DNS server: 10.0.0.2
Future Use: 10.0.0.3
Broadcast address: 10.0.0.255


Route tables contains rules(routes), that tell your network traffic where to go.
# Route table Types
1. Main Route Table - Automatically comes with your VPC & acts as the default table for any leftover, unassociated subnets.
2. Custom Route Table - Fully define & associate with subnets

# Custom Route Tables Concepts
1. Destination: Range of IP address (CIDR) where u want to direct your traffic towards (192.168.0.0/24)
2. Target: network interfaces or other connections where the destination traffic should go (Internet Gateway)
3. Local Route: Every route table has a local route applied for any VPC-bound traffic
4. Association: You associate subnets with a Route Table to apply the chosen rules for any network traffic in the subnet.

Public subnet route tables will have a local VPC route & a route to the IGW for all other traffic.
Public subnets will have publicly resolvable IP address assigned to the compute.
Public subnet will have one local route & IGW route

Private subnet route tables are only going to have local VPC route for the VPC CIDR traffic.
Private subnet will have one local route

# Network Access Control List: NACL
Allows or denies specific inbound or outbound traffic at the subnet level.
A Stateless firewall to control traffic at the subnet level.
Stateless: Must explicitly define both inbound & Outbound traffic rules.
Assign one NACL per subnet, with a Default NACL in place if needed.
Newly Created NACLs will deny all traffic by default.
List of ascending numbered, prioritized rules where the first match wins.
Traffic NACL's Dont work with:
Amzon DNS, Amazon DHCP,Amazon EC2 instance metdata, Reserved IP adddressed used by the default VPC router.