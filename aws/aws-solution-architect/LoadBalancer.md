# AWS Load Balancer Cheat Sheet (ALB & NLB)

> Interview-focused AWS ELB notes for Senior Cloud Architects / DevOps Engineers / SREs

---

# Table of Contents

- [AWS Load Balancer Types](#aws-load-balancer-types)
- [Application Load Balancer (ALB)](#application-load-balancer-alb)
- [Network Load Balancer (NLB)](#network-load-balancer-nlb)
- [ALB vs NLB](#alb-vs-nlb)
- [Health Checks](#health-checks)
- [Common Interview Questions](#common-interview-questions)
- [Architecture Patterns](#architecture-patterns)
- [Troubleshooting](#troubleshooting)
- [Useful AWS CLI Commands](#useful-aws-cli-commands)
- [Best Practices](#best-practices)
- [Official AWS Documentation](#official-aws-documentation)

---

# AWS Load Balancer Types

| LB Type | Layer | Protocols | Main Use Case |
|---|---|---|---|
| ALB | Layer 7 | HTTP/HTTPS/gRPC | Web apps, APIs, Microservices |
| NLB | Layer 4 | TCP/UDP/TLS | High-performance applications |
| GWLB | Layer 3/4 | IP | Security appliances |
| CLB | Legacy | HTTP/TCP | Older applications |

---

# Application Load Balancer (ALB)

## Key Features

- Layer 7 Load Balancer
- Path-based routing
- Host-based routing
- Header-based routing
- Query parameter routing
- Supports WebSockets
- Supports HTTP/2
- Supports gRPC
- AWS WAF integration
- Lambda targets supported

---

# ALB Important Defaults

| Attribute | Default Value |
|---|---|
| Idle Timeout | 60 seconds |
| Deregistration Delay | 300 seconds |
| Stickiness | Disabled |
| Cross-Zone LB | Enabled |
| Access Logs | Disabled |
| Deletion Protection | Disabled |

---

# ALB Routing Examples

## Path-Based Routing

```text
/api/* → API Service
/images/* → Image Service
```

## Host-Based Routing

```text
app.example.com → App Service
admin.example.com → Admin Service
```

---

# ALB Sticky Sessions

## Types

- lb_cookie
- app_cookie

## Interview Tip

Avoid sticky sessions for:
- Microservices
- Stateless applications
- Auto Scaling workloads

---

# ALB Common Error Codes

| Error Code | Meaning |
|---|---|
| 502 | Bad Gateway |
| 503 | No Healthy Targets |
| 504 | Gateway Timeout |

---

# ALB CloudWatch Metrics

| Metric | Purpose |
|---|---|
| RequestCount | Traffic volume |
| TargetResponseTime | Backend latency |
| HTTPCode_ELB_5XX | ELB-side errors |
| HealthyHostCount | Healthy targets |
| RejectedConnectionCount | Capacity issues |

---

# Network Load Balancer (NLB)

## Key Features

- Layer 4 Load Balancer
- Ultra-high performance
- Supports TCP/UDP/TLS
- Static IP support
- Elastic IP support
- Preserves source IP
- Very low latency

---

# NLB Important Defaults

| Attribute | Default Value |
|---|---|
| Idle Timeout | 350 seconds |
| Deregistration Delay | 300 seconds |
| Cross-Zone LB | Disabled |
| Access Logs | Disabled |

---

# NLB Major Advantages

- Supports millions of requests/sec
- Native client IP preservation
- Static IP support
- Better for long-lived TCP connections
- UDP support

---

# NLB Common Use Cases

| Use Case | Reason |
|---|---|
| Kafka | Long-lived TCP |
| Gaming | UDP support |
| Trading systems | Low latency |
| SIP/VoIP | UDP |
| Databases | Static IP requirement |

---

# ALB vs NLB

| Feature | ALB | NLB |
|---|---|---|
| Layer | L7 | L4 |
| Protocols | HTTP/HTTPS/gRPC | TCP/UDP/TLS |
| Static IP | No | Yes |
| WAF Support | Yes | No |
| Source IP Preservation | Via Header | Native |
| Path Routing | Yes | No |
| Host Routing | Yes | No |
| Lambda Target | Yes | No |
| UDP Support | No | Yes |
| HTTP/2 | Yes | No |
| WebSockets | Yes | TCP only |
| Cross-Zone Default | Enabled | Disabled |

---

# Health Checks

## ALB Health Check Defaults

| Setting | Default |
|---|---|
| Interval | 30 sec |
| Timeout | 5 sec |
| Healthy Threshold | 5 |
| Unhealthy Threshold | 2 |

---

## NLB Health Check Defaults

| Setting | Default |
|---|---|
| Interval | 30 sec |
| Timeout | 10 sec |
| Healthy Threshold | 5 |
| Unhealthy Threshold | 2 |

---

# Architecture Patterns

## Internet-Facing Architecture

```text
CloudFront
   ↓
AWS WAF
   ↓
ALB
   ↓
EKS / ECS / EC2
```

---

## High-Performance TCP Architecture

```text
Client
   ↓
NLB
   ↓
Kafka / Trading App / Database
```

---

## Security Inspection Architecture

```text
Internet
   ↓
GWLB
   ↓
Firewall Appliances
   ↓
ALB / NLB
```

---

# Common Interview Questions

---

## Why use ALB?

### Answer

- Advanced HTTP routing
- Microservices architecture
- WAF integration
- gRPC support
- Authentication integration

---

## Why use NLB?

### Answer

- Ultra-low latency
- Static IP support
- Source IP preservation
- UDP support
- Long-lived TCP connections

---

## Why do requests fail after exactly 60 seconds?

### Answer

ALB Idle Timeout default is 60 seconds.

---

## Why avoid sticky sessions?

### Answer

- Uneven traffic distribution
- Poor scalability
- Reduced fault tolerance

---

## Why is Cross-Zone disabled by default in NLB?

### Answer

To maintain zonal isolation and reduce cross-AZ traffic costs.

---

# Troubleshooting

| Problem | Possible Cause |
|---|---|
| 502 Errors | Application failure |
| 503 Errors | No healthy targets |
| 504 Errors | Backend timeout |
| Uneven traffic | Sticky sessions |
| TLS handshake failure | Cipher mismatch |
| WebSocket disconnect | Idle timeout |

---

# Useful AWS CLI Commands

## Describe Load Balancer Attributes

```bash
aws elbv2 describe-load-balancer-attributes \
--load-balancer-arn <arn>
```

---

## Modify ALB Idle Timeout

```bash
aws elbv2 modify-load-balancer-attributes \
--load-balancer-arn <arn> \
--attributes Key=idle_timeout.timeout_seconds,Value=300
```

---

## Describe Target Health

```bash
aws elbv2 describe-target-health \
--target-group-arn <arn>
```

---

# Best Practices

## ALB Best Practices

- Enable access logs
- Use WAF
- Use HTTPS everywhere
- Avoid sticky sessions
- Tune idle timeout properly
- Use path-based routing

---

## NLB Best Practices

- Use for high-throughput workloads
- Enable cross-zone carefully
- Preserve source IP when needed
- Use TLS listeners for secure TCP workloads

---

# MUST-REMEMBER Values

| Setting | Value |
|---|---|
| ALB Idle Timeout | 60 sec |
| NLB Idle Timeout | 350 sec |
| Deregistration Delay | 300 sec |
| Health Check Interval | 30 sec |
| Healthy Threshold | 5 |
| Unhealthy Threshold | 2 |

---

# Golden Interview Statement

```text
Use ALB when application awareness is needed.
Use NLB when network performance is critical.
```

---

# Official AWS Documentation

## ALB Documentation

https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html

---

## NLB Documentation

https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html

---

## ELB Best Practices

https://aws.amazon.com/blogs/networking-and-content-delivery/elb-best-practices/

---

# Author

Created for:
- AWS Interview Preparation
- Cloud Architect Learning
- DevOps/SRE Knowledge Sharing

---
