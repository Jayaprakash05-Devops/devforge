# AWS Networking Cheat Sheet (VPC + Hybrid + Security + Connectivity)

> Complete AWS Networking notes for Cloud Architects, DevOps Engineers, SREs, and AWS Interview Preparation

---

# Table of Contents

- [AWS Networking Overview](#aws-networking-overview)
- [VPC](#vpc)
- [Subnets](#subnets)
- [Route Tables](#route-tables)
- [Internet Gateway](#internet-gateway)
- [NAT Gateway](#nat-gateway)
- [Security Groups](#security-groups)
- [NACL](#nacl)
- [VPC Peering](#vpc-peering)
- [Transit Gateway](#transit-gateway)
- [VPC Endpoints](#vpc-endpoints)
- [PrivateLink](#privatelink)
- [Direct Connect](#direct-connect)
- [VPN](#vpn)
- [Route 53](#route-53)
- [Elastic IP](#elastic-ip)
- [Load Balancers](#load-balancers)
- [Hybrid Networking](#hybrid-networking)
- [DNS](#dns)
- [Traffic Flow](#traffic-flow)
- [Monitoring & Troubleshooting](#monitoring--troubleshooting)
- [Common Interview Questions](#common-interview-questions)
- [Best Practices](#best-practices)
- [Official AWS Docs](#official-aws-docs)

---

# AWS Networking Overview

Core AWS networking services:

| Service | Purpose |
|---|---|
| VPC | Private network |
| Subnet | Network segmentation |
| Route Table | Traffic routing |
| IGW | Internet access |
| NAT Gateway | Outbound internet |
| Security Group | Stateful firewall |
| NACL | Stateless firewall |
| TGW | Multi-VPC connectivity |
| Route 53 | DNS |
| Direct Connect | Dedicated connection |
| VPN | Encrypted tunnel |

---

# VPC

VPC = Virtual Private Cloud

Logical isolated AWS network.

---

# VPC CIDR Example

```text
10.0.0.0/16
```

Provides:
```text
65,536 IP addresses
```

---

# VPC Important Facts

| Feature | Details |
|---|---|
| Region Scoped | Yes |
| Default VPC | One per region |
| Supports IPv4 | Yes |
| Supports IPv6 | Yes |

---

# Default VPC Components

- Public subnet
- Internet Gateway
- Route table
- Security group
- NACL

---

# Subnets

Subnet = Network segment inside VPC

---

# Public Subnet

Has route to:
```text
Internet Gateway
```

Used for:
- Load balancers
- Bastion hosts
- NAT Gateway

---

# Private Subnet

No direct internet access.

Used for:
- Databases
- Application servers
- Internal services

---

# Reserved IPs in Every Subnet

AWS reserves:
```text
First 4 IPs + Last IP
```

Example:
```text
10.0.1.0/24
```

Reserved:
```text
10.0.1.0
10.0.1.1
10.0.1.2
10.0.1.3
10.0.1.255
```

---

# Route Tables

Controls traffic routing.

---

# Example Routes

| Destination | Target |
|---|---|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | IGW |
| 0.0.0.0/0 | NAT GW |

---

# Route Priority

Longest prefix match wins.

Example:
```text
10.0.1.0/24 > 10.0.0.0/16
```

---

# Internet Gateway (IGW)

Provides:
```text
Internet access
```

Requirements:
- Public IP
- Route to IGW

---

# NAT Gateway

Provides:
```text
Outbound internet for private subnet
```

---

# NAT Gateway Important Facts

| Feature | Details |
|---|---|
| Managed Service | Yes |
| AZ Scoped | Yes |
| Requires Elastic IP | Yes |

---

# NAT Gateway vs NAT Instance

| Feature | NAT GW | NAT Instance |
|---|---|---|
| Managed | Yes | No |
| HA | Yes | Manual |
| Scaling | Auto | Manual |
| Performance | High | Depends |

---

# Security Groups

Instance-level firewall.

---

# Security Group Features

| Feature | Value |
|---|---|
| Stateful | Yes |
| Deny Rules | No |
| Allow Rules Only | Yes |

---

# Security Group Example

```text
Allow:
TCP 22 from 10.0.0.0/16
TCP 443 from 0.0.0.0/0
```

---

# NACL

Subnet-level firewall.

---

# NACL Features

| Feature | Value |
|---|---|
| Stateless | Yes |
| Allow Rules | Yes |
| Deny Rules | Yes |
| Rule Order Matters | Yes |

---

# Security Group vs NACL

| Feature | SG | NACL |
|---|---|---|
| Stateful | Yes | No |
| Applied At | Instance | Subnet |
| Deny Rules | No | Yes |

---

# VPC Peering

Connects:
```text
VPC ↔ VPC
```

---

# VPC Peering Limitations

- No transitive routing
- CIDR overlap not allowed

---

# Transit Gateway (TGW)

Hub-and-spoke networking.

---

# TGW Benefits

- Centralized routing
- Multi-VPC connectivity
- Hybrid networking
- Scalable architecture

---

# Transit Gateway Architecture

```text
VPCs
  ↓
Transit Gateway
  ↓
On-Prem / Other VPCs
```

---

# VPC Endpoints

Private AWS service access without internet.

---

# Types of VPC Endpoints

| Type | Service |
|---|---|
| Gateway Endpoint | S3, DynamoDB |
| Interface Endpoint | Most AWS services |

---

# Gateway Endpoint

Used for:
- S3
- DynamoDB

No ENI required.

---

# Interface Endpoint

Uses:
```text
Elastic Network Interface (ENI)
```

Powered by:
```text
AWS PrivateLink
```

---

# PrivateLink

Private service exposure.

---

# Benefits

- No internet exposure
- No VPC peering needed
- Secure SaaS integration

---

# Direct Connect

Dedicated private AWS connection.

---

# Direct Connect Benefits

- Low latency
- Consistent bandwidth
- Hybrid cloud
- Private connectivity

---

# Direct Connect Speeds

| Speed |
|---|
| 1 Gbps |
| 10 Gbps |
| 100 Gbps |

---

# VPN

Encrypted IPSec tunnel.

---

# VPN Types

| Type | Purpose |
|---|---|
| Site-to-Site VPN | On-prem to AWS |
| Client VPN | User remote access |

---

# Route 53

AWS DNS service.

---

# Route 53 Routing Policies

| Policy | Purpose |
|---|---|
| Simple | Single endpoint |
| Weighted | Traffic split |
| Latency | Lowest latency |
| Failover | DR |
| Geolocation | Region-based |
| Multivalue | Multiple healthy IPs |

---

# Route 53 Health Checks

Monitors:
- HTTP
- HTTPS
- TCP

---

# Elastic IP

Static public IPv4.

---

# Important Facts

- Region scoped
- One free when attached
- Charged if unused

---

# Load Balancers

| LB | Layer |
|---|---|
| ALB | L7 |
| NLB | L4 |
| GWLB | L3/L4 |

---

# ALB

Best for:
- HTTP routing
- APIs
- Microservices

---

# NLB

Best for:
- TCP/UDP
- Static IP
- High throughput

---

# Hybrid Networking

---

# Hybrid Connectivity Options

| Service | Use Case |
|---|---|
| VPN | Quick setup |
| Direct Connect | Enterprise dedicated connectivity |
| TGW | Centralized routing |

---

# DNS

---

# Public Hosted Zone

Internet-facing DNS.

---

# Private Hosted Zone

Internal VPC DNS.

---

# Resolver Endpoints

Used for:
- Hybrid DNS
- On-prem integration

---

# Traffic Flow Example

---

# Public Web App

```text
Internet
   ↓
Route 53
   ↓
CloudFront
   ↓
WAF
   ↓
ALB
   ↓
EC2/EKS/ECS
```

---

# Private Application

```text
Private Subnet
   ↓
NAT Gateway
   ↓
Internet
```

---

# Monitoring & Troubleshooting

---

# VPC Flow Logs

Captures:
- Accepted traffic
- Rejected traffic

---

# Common Tools

| Tool | Purpose |
|---|---|
| Reachability Analyzer | Path validation |
| Flow Logs | Traffic analysis |
| CloudWatch | Monitoring |
| Route Tables | Routing validation |

---

# Common Networking Problems

| Problem | Cause |
|---|---|
| No internet | Missing IGW/NAT |
| SSH timeout | SG/NACL issue |
| DNS failure | Route53/VPC DNS |
| Packet drops | NACL deny |
| Peering issue | Missing routes |

---

# Important Ports

| Port | Service |
|---|---|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 3306 | MySQL |
| 5432 | PostgreSQL |

---

# Common Interview Questions

---

# Difference between Security Group and NACL?

### Answer

```text
Security Group is stateful and instance-level.
NACL is stateless and subnet-level.
```

---

# Why use NAT Gateway?

### Answer

```text
Allows outbound internet access from private subnet.
```

---

# Difference between IGW and NAT Gateway?

| IGW | NAT GW |
|---|---|
| Public internet access | Outbound internet only |
| Public subnet | Private subnet |

---

# Why Transit Gateway over VPC Peering?

### Answer

```text
TGW provides scalable hub-and-spoke architecture.
```

---

# Difference between Direct Connect and VPN?

| Direct Connect | VPN |
|---|---|
| Dedicated line | Internet-based |
| Stable latency | Variable latency |
| Expensive | Cheaper |

---

# What is longest prefix match?

### Answer

```text
Most specific route wins.
```

---

# Best Practices

---

# Security

- Use least privilege SG rules
- Restrict 0.0.0.0/0
- Enable Flow Logs
- Use PrivateLink where possible

---

# High Availability

- Use Multi-AZ NAT Gateways
- Use TGW for scale
- Avoid single points of failure

---

# Performance

- Use Direct Connect for enterprise workloads
- Use NLB for high throughput
- Use placement groups for low latency

---

# Cost Optimization

- Avoid unnecessary NAT Gateways
- Use Gateway Endpoints for S3/DynamoDB
- Clean unused Elastic IPs

---

# MUST-REMEMBER Values

| Component | Important Fact |
|---|---|
| SG | Stateful |
| NACL | Stateless |
| NAT GW | AZ scoped |
| Peering | No transitive routing |
| Route Tables | Longest prefix wins |

---

# Golden Interview Statement

```text
AWS networking is built around secure, isolated, scalable, and highly available connectivity patterns.
```

---

# Official AWS Documentation

## VPC Docs

https://docs.aws.amazon.com/vpc/

---

## Transit Gateway Docs

https://docs.aws.amazon.com/vpc/latest/tgw/

---

## Route 53 Docs

https://docs.aws.amazon.com/route53/

---

## Direct Connect Docs

https://docs.aws.amazon.com/directconnect/

---

# Author

Created for:
- AWS Interview Preparation
- Cloud Architect Learning
- DevOps/SRE Knowledge Sharing
- Production Troubleshooting

---
