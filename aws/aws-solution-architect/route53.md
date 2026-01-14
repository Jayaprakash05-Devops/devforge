# AWS Route 53

## AWS Route 53: Alias vs CNAME vs A Records

This document explains the differences between **Alias**, **CNAME**, and **A records** in **Amazon Route 53**, with practical examples for AWS and non-AWS use cases.

---

### 1️⃣ CNAME Records

**Definition:**  
A **CNAME (Canonical Name)** record maps one DNS name to another DNS name.  

**Key Points:**
- Can point to any hostname (AWS or non-AWS)
- Cannot be used at the **zone apex** (root domain)
- Adds an extra DNS lookup
- Incurs DNS query charges

**When to use CNAME:**
- Subdomain → external provider
- Subdomain → RDS endpoint
- Subdomain → other non-AWS hostnames

**Examples:**

| Your domain | Target | Record Type | Notes |
|------------|--------|------------|------|
| `myrds.example.com` | `mydb.abc123.us-east-1.rds.amazonaws.com` | CNAME | RDS endpoint, non-AWS Alias not supported |
| `www.your-domain.com` | `yourapp.provider.com` | CNAME | External SaaS provider |
| `app.example.com` | `service.example.io` | CNAME | Subdomain mapping to another DNS |

---

### 2️⃣ Alias Records (AWS-specific)

**Definition:**  
An **Alias** record is a Route 53–specific record type that behaves like an **A or AAAA record** but can point directly to **certain AWS resources**.  

**Key Points:**
- Can be used at **zone apex (root domain)**
- Free — no DNS query charges
- Automatically tracks IP changes of AWS-managed resources
- Only works for **specific AWS resources**

**Supported AWS Targets:**
- Elastic Load Balancers (ALB, NLB, CLB)
- CloudFront distributions
- S3 static website endpoints
- API Gateway custom domains
- VPC endpoints (interface endpoints)
- AWS Global Accelerator

**Examples:**

| Your domain | Target | Record Type | Notes |
|------------|--------|------------|------|
| `myapp.example.com` | ALB DNS name | Alias (A/AAAA) | AWS resource, auto-updating IPs |
| `example.com` | CloudFront distribution | Alias (A/AAAA) | Works at root domain |
| `static.example.com` | S3 website | Alias (A/AAAA) | AWS-hosted static website |

---

### 3️⃣ A / AAAA Records

**Definition:**  
- **A record:** Maps a domain name to a static IPv4 address  
- **AAAA record:** Maps a domain name to a static IPv6 address

**Key Points:**
- Works for static IPs only
- IPs must be managed manually
- Not suitable for AWS resources with dynamic IPs

**Example:**


![Uploading image.png…](https://assets-pt.media.datacumulus.com/aws-saa-pt/assets/pt2-q6-i1.jpg)
