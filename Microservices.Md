                ┌───────────────────────┐
                │        Users           │
                │  (Browser / Client)    │
                └───────────┬───────────┘
                            │
                            ▼
              ┌─────────────────────────────┐
              │   Application Load Balancer  │
              │   (Internet-facing or        │
              │    Internal ALB)              │
              └───────────┬───────────┬─────┘
                          │           │
          ─────────────────┘           └─────────────────
          ▼                                              ▼
┌───────────────────────┐                ┌───────────────────────┐
│ Availability Zone A   │                │ Availability Zone B   │
│ (e.g., us-east-1a)    │                │ (e.g., us-east-1b)    │
│                       │                │                       │
│  ┌─────────────────┐ │                │  ┌─────────────────┐ │
│  │ EC2 Instance 1  │◄┼── Health Check ─┼─►│ EC2 Instance 2  │ │
│  │ (Target Group)  │ │                │  │ (Target Group)  │ │
│  └─────────────────┘ │                │  └─────────────────┘ │
│                       │                │                       │
└───────────────────────┘                └───────────────────────┘


Enable Cross-Zone Load Balancing (Usually Default) - This ensures traffic is evenly distributed across instances in all AZs

# Interview-Ready Answer (Concise)

“To set up a load balancer across two Availability Zones in AWS, we use an Elastic Load Balancer—typically an Application Load Balancer. We create the load balancer inside a VPC and attach it to at least two subnets, each in a different Availability Zone. We then create a target group and register EC2 instances (or an Auto Scaling Group) running in both AZs. The load balancer uses health checks to route traffic only to healthy instances, and cross-zone load balancing ensures even traffic distribution. This setup provides high availability and fault tolerance.”

# Networking / Microservices
How This Works?
The Application Load Balancer (ALB) is deployed across two subnets, each in a different AZ
Traffic is distributed to healthy EC2 instances in both AZs
If one AZ fails, traffic automatically flows to the other
Health checks ensure only healthy targets receive traffic


# Real-World Failure Scenario (This Is the Key Differentiator)
Scenario: Availability Zone Failure

“For example, if Availability Zone us-east-1a experiences a network or power issue, the Application Load Balancer automatically stops routing traffic to unhealthy targets in that AZ based on failed health checks. Since the Auto Scaling Group spans multiple AZs, instances in us-east-1b continue serving traffic without manual intervention. In many cases, Auto Scaling also launches replacement instances in the healthy AZ, maintaining capacity while the impacted AZ recovers.”

# Why This Works in Production?
Health checks fail → ALB removes unhealthy targets
Traffic shifts automatically → No downtime
Auto Scaling compensates → Capacity maintained
No DNS change required → Seamless to users