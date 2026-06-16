# AWS EC2 Security Groups: Controlling Access to Your Instances (Beginner → Veteran Roadmap)

## Learning Objective

Master EC2 Security Groups from first principles so you can design secure cloud infrastructure, minimize attack surfaces, and confidently protect production workloads.

---

# Phase 0: First-Principles Foundation

## Core Question

Before learning Security Groups, answer:

* [ ] Why can computers communicate over networks?
* [ ] Why is every internet-connected server a potential target?
* [ ] What happens if every port is open?
* [ ] Why do attackers scan servers?
* [ ] Why is "deny by default" important?

### First-Principles Model

Internet

↓

Network Traffic

↓

Firewall Rules

↓

Operating System

↓

Application

Security Groups are AWS's first line of network defense.

### Mental Model

Think of a Security Group as a security guard standing at every EC2 instance.

Every incoming request asks:

* [ ] Who are you?
* [ ] Which port are you using?
* [ ] Are you allowed?

### Mastery Check

* [ ] Explain Security Groups without mentioning AWS.

---

# Phase 1: Understanding Network Security

## Learn

### What is Network Access Control?

* [ ] Network communication basics
* [ ] Client-server communication
* [ ] Network exposure risks

### Understand

Every service listens on a port.

Examples:

* [ ] SSH → Port 22
* [ ] HTTP → Port 80
* [ ] HTTPS → Port 443
* [ ] MySQL → Port 3306
* [ ] PostgreSQL → Port 5432

### Exercise

* [ ] Identify ports used by common applications

### Mastery Check

* [ ] Explain why ports exist.

---

# Phase 2: What Are Security Groups?

## Learn

### Definition

A Security Group is a virtual firewall attached to AWS resources.

### Characteristics

* [ ] Instance-level protection
* [ ] Stateful firewall
* [ ] Allow rules only
* [ ] Implicit deny

### Understand

Allowed Traffic:

Request → Security Group → EC2

Blocked Traffic:

Request → Security Group → Rejected

### Mastery Check

* [ ] Explain stateful vs stateless firewalls.

---

# Phase 3: Inbound Rules

## First Principle

Inbound rules determine who can enter.

### Components

Each rule contains:

* [ ] Protocol
* [ ] Port
* [ ] Source

### Example

SSH Access

Protocol: TCP

Port: 22

Source: Your IP

### Common Inbound Rules

#### SSH

* [ ] TCP 22
* [ ] Restrict to admin IP

#### Web Server

* [ ] TCP 80
* [ ] Open to internet

#### HTTPS

* [ ] TCP 443
* [ ] Open to internet

#### Database

* [ ] TCP 3306
* [ ] Allow application servers only

### Exercise

Create:

* [ ] SSH-only server
* [ ] Public website server
* [ ] Private database server

### Mastery Check

* [ ] Design secure inbound policies.

---

# Phase 4: Outbound Rules

## First Principle

Servers also initiate connections.

### Learn

Outbound rules control:

* [ ] Software updates
* [ ] API requests
* [ ] Database replication
* [ ] External service communication

### Components

* [ ] Protocol
* [ ] Port
* [ ] Destination

### Exercise

Create outbound policies for:

* [ ] Web server
* [ ] Database server
* [ ] Application server

### Mastery Check

* [ ] Explain why outbound restrictions matter.

---

# Phase 5: Understanding Ports

## Learn

### Port Categories

#### Well-Known Ports

* [ ] 22 SSH
* [ ] 80 HTTP
* [ ] 443 HTTPS

#### Database Ports

* [ ] 3306 MySQL
* [ ] 5432 PostgreSQL
* [ ] 27017 MongoDB

#### Application Ports

* [ ] 3000 Node.js
* [ ] 8080 Web Applications

### Exercise

Map services to ports.

### Mastery Check

* [ ] Identify unnecessary open ports.

---

# Phase 6: Restricting Access Properly

## First Principle

Every open port increases risk.

### Learn

### Bad Practice

* [ ] 0.0.0.0/0 on SSH

### Good Practice

* [ ] Restrict SSH to known IPs

### Better Practice

* [ ] Use VPN or bastion host

### Best Practice

* [ ] Eliminate direct SSH access where possible

### Exercise

Secure an insecure EC2 instance.

### Mastery Check

* [ ] Reduce attack surface effectively.

---

# Phase 7: Security Group Architecture

## Multi-Tier Architecture

### Web Tier

Allow:

* [ ] HTTP
* [ ] HTTPS

### Application Tier

Allow:

* [ ] Requests from web tier only

### Database Tier

Allow:

* [ ] Requests from application tier only

### Architecture

Internet

↓

Web Security Group

↓

Application Security Group

↓

Database Security Group

### Project

* [ ] Build secure three-tier architecture

### Mastery Check

* [ ] Design layered security.

---

# Phase 8: Security Group References

## Learn

Instead of IP addresses:

* [ ] Reference another Security Group

### Benefits

* [ ] Dynamic scaling support
* [ ] Easier management
* [ ] Reduced configuration errors

### Example

Database Security Group:

Allow MySQL from:

Application Security Group

Not:

Specific IPs

### Project

* [ ] Implement SG-to-SG communication

### Mastery Check

* [ ] Build scalable security policies.

---

# Phase 9: Security Monitoring

## Learn

### AWS Tools

* [ ] CloudTrail
* [ ] VPC Flow Logs
* [ ] CloudWatch

### Detect

* [ ] Unauthorized changes
* [ ] Excessive access attempts
* [ ] Misconfigurations

### Exercise

Audit security group changes.

### Mastery Check

* [ ] Investigate suspicious network activity.

---

# Phase 10: Common Misconfigurations

## Dangerous Patterns

### Never Do

* [ ] Open SSH to the world
* [ ] Open database ports publicly
* [ ] Allow all protocols unnecessarily
* [ ] Use overly permissive rules

### Learn

Why these create risks:

* [ ] Brute-force attacks
* [ ] Data exposure
* [ ] Lateral movement

### Exercise

Review intentionally vulnerable security groups.

### Mastery Check

* [ ] Identify security issues immediately.

---

# Phase 11: Security Group Automation

## Learn

### Infrastructure as Code

* [ ] Terraform
* [ ] CloudFormation

### Benefits

* [ ] Repeatability
* [ ] Version control
* [ ] Auditability

### Project

* [ ] Deploy security groups through code

### Mastery Check

* [ ] Manage infrastructure without manual changes.

---

# Phase 12: Advanced Security Design

## Defense-in-Depth

Security Groups are one layer.

Additional layers:

* [ ] IAM
* [ ] OS Firewall
* [ ] Application Authentication
* [ ] Encryption
* [ ] Monitoring

### Learn

* [ ] Zero Trust concepts
* [ ] Network segmentation
* [ ] Least privilege networking

### Project

* [ ] Design enterprise-grade security architecture

---

# Veteran Mental Models

## Think Like an Attacker

Always ask:

* [ ] What is exposed?
* [ ] What can be reached?
* [ ] What happens if compromised?

## Security Principles

* [ ] Deny by default
* [ ] Least privilege
* [ ] Defense in depth
* [ ] Minimize attack surface
* [ ] Trust nothing by default

---

# Veteran Projects

## Project 1

* [ ] Secure single EC2 server

## Project 2

* [ ] Build secure three-tier application

## Project 3

* [ ] Implement bastion host architecture

## Project 4

* [ ] Deploy security groups using Terraform

## Project 5

* [ ] Conduct security review of production environment

---

# Veteran Mastery Checklist

## Fundamentals

* [ ] Understand networking basics
* [ ] Understand firewall principles
* [ ] Understand ports and protocols

## AWS Security

* [ ] Configure inbound rules correctly
* [ ] Configure outbound rules correctly
* [ ] Use security group references

## Operations

* [ ] Audit configurations
* [ ] Monitor changes
* [ ] Detect misconfigurations

## Architecture

* [ ] Design layered security
* [ ] Protect databases properly
* [ ] Implement least privilege

---

# Final Veteran Benchmark

You have reached veteran level when you can:

* [ ] Secure EC2 environments from scratch
* [ ] Design secure multi-tier architectures
* [ ] Prevent common network attacks
* [ ] Audit security groups quickly
* [ ] Automate network security controls
* [ ] Explain firewall behavior from first principles
* [ ] Minimize attack surfaces without affecting functionality
* [ ] Lead cloud security reviews confidently

---

# Real-World Security Group Rules Cheat Sheet

## Public Web Server

* [ ] TCP 80 → 0.0.0.0/0
* [ ] TCP 443 → 0.0.0.0/0
* [ ] TCP 22 → Admin IP only

## Private Application Server

* [ ] Allow traffic from Web SG
* [ ] No public internet access

## Private Database

* [ ] Allow DB port from App SG only
* [ ] No public internet access

## Golden Rule

* [ ] Open only what is required.
* [ ] Restrict access as much as possible.
* [ ] Review rules regularly.
* [ ] Assume every exposed service will eventually be targeted.

```
```
