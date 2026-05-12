# AWS EC2 Cheat Sheet (Interview + Production Ready)

> Complete EC2 notes for Cloud Architects, DevOps Engineers, SREs, and AWS Interview Preparation

---

# Table of Contents

- [What is EC2](#what-is-ec2)
- [EC2 Instance Types](#ec2-instance-types)
- [EC2 Purchasing Options](#ec2-purchasing-options)
- [EC2 Storage](#ec2-storage)
- [Networking](#networking)
- [Security](#security)
- [Monitoring](#monitoring)
- [Scaling](#scaling)
- [Boot Process](#boot-process)
- [Metadata & User Data](#metadata--user-data)
- [Placement Groups](#placement-groups)
- [AMI](#ami)
- [Important Timeouts & Limits](#important-timeouts--limits)
- [Troubleshooting](#troubleshooting)
- [CLI Commands](#cli-commands)
- [Interview Questions](#interview-questions)
- [Best Practices](#best-practices)
- [Official AWS Docs](#official-aws-docs)

---

# What is EC2

Amazon EC2 (Elastic Compute Cloud) provides scalable virtual servers in AWS Cloud.

---

# EC2 Core Components

| Component | Purpose |
|---|---|
| AMI | Operating system template |
| Instance Type | CPU/RAM/Network configuration |
| EBS | Persistent storage |
| Security Group | Instance firewall |
| Key Pair | SSH authentication |
| ENI | Elastic Network Interface |

---

# EC2 Instance Types

---

# General Purpose

| Family | Use Case |
|---|---|
| T3/T4g | Burstable workloads |
| M5/M6i | Balanced compute/memory |

---

# Compute Optimized

| Family | Use Case |
|---|---|
| C5/C6i | CPU-intensive apps |

Examples:
- Gaming servers
- Batch processing
- API servers

---

# Memory Optimized

| Family | Use Case |
|---|---|
| R5/R6i | High-memory applications |
| X1/X2 | SAP HANA |

Examples:
- Redis
- SAP
- Analytics

---

# Storage Optimized

| Family | Use Case |
|---|---|
| I3/I4i | High IOPS workloads |
| D3 | Dense storage |

Examples:
- NoSQL databases
- Elasticsearch

---

# GPU Instances

| Family | Use Case |
|---|---|
| P Series | ML training |
| G Series | Graphics rendering |

---

# EC2 Purchasing Options

| Type | Description |
|---|---|
| On-Demand | Pay per use |
| Reserved | Long-term discount |
| Savings Plan | Flexible discount model |
| Spot | Unused AWS capacity |
| Dedicated Host | Physical server isolation |

---

# Spot Instance Important Facts

| Feature | Details |
|---|---|
| Cheapest Option | Yes |
| Can AWS terminate? | Yes |
| Interruption Notice | 2 minutes |
| Best For | Batch jobs |

---

# EC2 Storage

---

# EBS Volume Types

| Type | Use Case |
|---|---|
| gp3 | General SSD |
| io1/io2 | High IOPS |
| st1 | Throughput optimized |
| sc1 | Cold HDD |

---

# gp3 Defaults

| Attribute | Value |
|---|---|
| Baseline IOPS | 3000 |
| Baseline Throughput | 125 MB/s |

---

# io2 Features

- Highest durability
- High IOPS
- Mission-critical databases

---

# Instance Store

| Feature | Value |
|---|---|
| Persistent | No |
| Very Fast | Yes |
| Ephemeral | Yes |

Use Cases:
- Cache
- Temporary storage
- Buffering

---

# Networking

---

# ENI (Elastic Network Interface)

Provides:
- Private IP
- Public IP
- MAC address
- Security groups

---

# Security Groups

## Characteristics

- Stateful firewall
- Allow rules only
- Instance-level firewall

---

# NACL

## Characteristics

- Stateless firewall
- Allow + Deny rules
- Subnet-level firewall

---

# Security Group vs NACL

| Feature | Security Group | NACL |
|---|---|---|
| Stateful | Yes | No |
| Deny Rules | No | Yes |
| Applied At | Instance | Subnet |

---

# Elastic IP

- Static public IPv4
- Region-specific
- Charged if unused

---

# Monitoring

---

# CloudWatch Basic Monitoring

Default:
```text
5 minutes
```

---

# Detailed Monitoring

Frequency:
```text
1 minute
```

---

# Important EC2 Metrics

| Metric | Purpose |
|---|---|
| CPUUtilization | CPU usage |
| DiskReadOps | Disk reads |
| NetworkIn | Incoming traffic |
| StatusCheckFailed | Health issue |

---

# Scaling

---

# Auto Scaling Components

| Component | Purpose |
|---|---|
| Launch Template | Instance configuration |
| ASG | Auto Scaling Group |
| Scaling Policy | Scale logic |

---

# Scaling Types

| Type | Description |
|---|---|
| Dynamic Scaling | CPU/metric based |
| Scheduled Scaling | Time-based |
| Predictive Scaling | Forecast-based |

---

# Auto Scaling Defaults

| Setting | Default |
|---|---|
| Health Check Grace Period | 300 sec |
| Cooldown | 300 sec |

---

# Boot Process

```text
Hardware
   ↓
BIOS/UEFI
   ↓
Bootloader
   ↓
Kernel
   ↓
Init/Systemd
   ↓
Services
```

---

# Metadata & User Data

---

# Instance Metadata

URL:
```bash
http://169.254.169.254/latest/meta-data/
```

Used for:
- IAM role credentials
- Instance info
- Networking details

---

# User Data

Runs:
```text
At first boot
```

Used for:
- Bootstrap scripts
- Package installation
- App deployment

---

# IMDSv2

More secure metadata service.

Interview Question:
```text
Why use IMDSv2?
```

Answer:
```text
Protection against SSRF attacks
```

---

# Placement Groups

---

# Cluster Placement Group

Best for:
- Low latency
- HPC workloads

---

# Spread Placement Group

Best for:
- High availability

---

# Partition Placement Group

Best for:
- Large distributed systems

Examples:
- Hadoop
- Cassandra

---

# AMI

Amazon Machine Image

Contains:
- OS
- Packages
- Configurations

---

# AMI Types

| Type | Description |
|---|---|
| Public | AWS/community |
| Private | Custom AMI |
| Marketplace | Paid AMIs |

---

# Important Timeouts & Limits

| Setting | Default |
|---|---|
| SSH Timeout | Depends on SG/NACL |
| ASG Cooldown | 300 sec |
| Health Grace Period | 300 sec |
| Spot Notice | 2 min |
| Basic Monitoring | 5 min |
| Detailed Monitoring | 1 min |

---

# EC2 Status Checks

---

# System Status Check

Checks:
- AWS infrastructure

---

# Instance Status Check

Checks:
- OS/network configuration

---

# Attached EBS Status Check

Checks:
- Volume health

---

# Troubleshooting

| Problem | Cause |
|---|---|
| SSH timeout | SG/NACL issue |
| High CPU | Application load |
| Instance unreachable | Route/NACL/SG |
| Disk full | EBS exhaustion |
| Status check failed | Infrastructure/OS issue |

---

# Common Linux Commands

## Disk Usage

```bash
df -h
```

---

## Memory Usage

```bash
free -m
```

---

## CPU Usage

```bash
top
```

---

## Network Connections

```bash
netstat -tulpn
```

---

# AWS CLI Commands

---

# Describe EC2 Instances

```bash
aws ec2 describe-instances
```

---

# Start Instance

```bash
aws ec2 start-instances --instance-ids i-123456
```

---

# Stop Instance

```bash
aws ec2 stop-instances --instance-ids i-123456
```

---

# Create AMI

```bash
aws ec2 create-image \
--instance-id i-123456 \
--name my-ami
```

---

# Interview Questions

---

# Why T-series instances are cheap?

Answer:
```text
Burstable CPU model using CPU credits
```

---

# Difference between gp3 and io2?

| gp3 | io2 |
|---|---|
| General purpose | Mission critical |
| Cheaper | Expensive |
| Baseline performance | High guaranteed IOPS |

---

# Security Group vs NACL?

Answer:
```text
SG is stateful at instance level.
NACL is stateless at subnet level.
```

---

# Difference between reboot and stop/start?

| Action | Host Changes? |
|---|---|
| Reboot | No |
| Stop/Start | Yes |

---

# Why use Auto Scaling?

Answer:
- High availability
- Cost optimization
- Elastic scaling

---

# Best Practices

---

# Security

- Use IAM Roles instead of access keys
- Disable root login
- Use IMDSv2
- Enable SSM Session Manager
- Use least privilege SG rules

---

# Performance

- Use gp3 for most workloads
- Use placement groups for low latency
- Enable detailed monitoring

---

# Reliability

- Use Multi-AZ architecture
- Use Auto Scaling
- Use Load Balancers
- Backup using AMIs and snapshots

---

# Cost Optimization

- Use Spot for batch jobs
- Use Savings Plans
- Stop unused instances
- Right-size instances

---

# Golden Interview Statement

```text
EC2 provides flexible, scalable compute capacity with full infrastructure-level control.
```

---

# Official AWS Documentation

## EC2 Docs

https://docs.aws.amazon.com/ec2/

---

## EC2 Instance Types

https://aws.amazon.com/ec2/instance-types/

---

## EBS Docs

https://docs.aws.amazon.com/ebs/

---

## Auto Scaling Docs

https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html

---

# Author

Created for:
- AWS Interview Preparation
- Cloud Architect Notes
- DevOps/SRE Learning
- Production Troubleshooting

---
