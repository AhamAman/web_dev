# AWS Security: IAM Roles, Policies, Security Groups & Network ACLs (Beginner → Veteran Roadmap)

## Learning Objective

Master AWS security from first principles by understanding identity, authorization, network security, least privilege access, and how enterprise cloud systems protect infrastructure, applications, and data.

---

# Phase 0: First-Principles Foundation

## Core Question

Before learning IAM and security rules, answer:

* [ ] Why do security breaches happen?
* [ ] Why shouldn't every user have admin access?
* [ ] How does AWS know who can perform an action?
* [ ] Why must network traffic be controlled?
* [ ] How do organizations secure thousands of cloud resources?

### First-Principles Model

Every security system answers two questions:

### Identity

Who are you?

### Authorization

What are you allowed to do?

### Fundamental Insight

Security is not about allowing access.

Security is about controlling access.

### Mastery Check

* [ ] Explain authentication vs authorization.

---

# Phase 1: Understanding Cloud Security

## Learn

### Common Threats

* [ ] Unauthorized access
* [ ] Credential theft
* [ ] Data leakage
* [ ] Privilege escalation
* [ ] Network attacks

### Security Layers

Identity Layer

↓

Network Layer

↓

Application Layer

↓

Data Layer

### Mental Model

Cloud security resembles a building:

* [ ] IAM = Employee badges
* [ ] Security Groups = Building doors
* [ ] NACLs = Security checkpoints
* [ ] Encryption = Locked safes

### Mastery Check

* [ ] Explain defense-in-depth.

---

# Phase 2: What is IAM?

## Definition

AWS Identity and Access Management (IAM) controls who can access AWS resources and what actions they can perform.

### IAM Components

* [ ] Users
* [ ] Groups
* [ ] Roles
* [ ] Policies

### Architecture

User

↓

IAM Authentication

↓

Policy Evaluation

↓

AWS Resource

### Mastery Check

* [ ] Explain IAM architecture.

---

# Phase 3: IAM Users and Groups

## Learn

### IAM Users

Represent:

* [ ] Humans
* [ ] Administrators
* [ ] Developers

### IAM Groups

Collection of users sharing permissions.

Examples:

* [ ] Developers
* [ ] Administrators
* [ ] Security Team

### Best Practices

* [ ] Avoid root account usage
* [ ] Use groups for permission management

### Project

* [ ] Create users and groups

### Mastery Check

* [ ] Design user access structure.

---

# Phase 4: IAM Policies

## First Principle

Permissions are rules.

### Definition

Policies define:

* [ ] Allowed actions
* [ ] Allowed resources
* [ ] Conditions

### Components

#### Effect

* [ ] Allow
* [ ] Deny

#### Action

* [ ] s3:GetObject
* [ ] ec2:StartInstances

#### Resource

Specific AWS resource

### Example Thinking

Allow:

Read S3 Bucket

Deny:

Delete S3 Bucket

### Project

* [ ] Create custom IAM policy

### Mastery Check

* [ ] Read and write IAM policies confidently.

---

# Phase 5: IAM Roles

## First Principle

Applications need permissions too.

### Problem

Hardcoding credentials is dangerous.

### Solution

IAM Roles

### Learn

Roles provide:

* [ ] Temporary credentials
* [ ] Secure access
* [ ] Automatic rotation

### Common Roles

* [ ] EC2 Role
* [ ] ECS Task Role
* [ ] Lambda Role

### Workflow

Application

↓

Assume Role

↓

Temporary Credentials

↓

AWS Resource Access

### Mastery Check

* [ ] Explain why roles are safer than access keys.

---

# Phase 6: IAM for EC2

## Learn

### EC2 Instance Profile

Attach role to instance.

### Example

EC2

↓

IAM Role

↓

S3 Access

### Project

* [ ] Create EC2 role
* [ ] Access S3 without credentials

### Mastery Check

* [ ] Eliminate hardcoded AWS keys.

---

# Phase 7: IAM for ECS

## Learn

### ECS Task Roles

Each container gets permissions.

### Benefits

* [ ] Fine-grained access
* [ ] Least privilege
* [ ] Better security

### Example

API Container

↓

Task Role

↓

DynamoDB Access

### Project

* [ ] Create ECS task role

### Mastery Check

* [ ] Secure container permissions.

---

# Phase 8: Least Privilege Access

## First Principle

Grant only necessary permissions.

### Bad Practice

AdministratorAccess

### Good Practice

Specific permissions only

### Example

Allow:

s3:GetObject

Deny:

s3:DeleteBucket

### Exercise

Reduce excessive permissions.

### Mastery Check

* [ ] Design least-privilege policies.

---

# Phase 9: Understanding Security Groups

## Learn

### Security Groups

Instance-level virtual firewall.

### Control

* [ ] Inbound traffic
* [ ] Outbound traffic

### Characteristics

* [ ] Stateful
* [ ] Allow rules only

### Project

Create:

* [ ] Web Server SG
* [ ] Database SG
* [ ] Application SG

### Mastery Check

* [ ] Secure EC2 networking.

---

# Phase 10: Understanding Network ACLs

## First Principle

Network protection should exist beyond instances.

### Learn

### Network ACLs

Subnet-level firewall.

### Characteristics

* [ ] Stateless
* [ ] Allow and Deny rules

### Architecture

Internet

↓

NACL

↓

Security Group

↓

Instance

### Comparison

Security Group

* [ ] Instance level
* [ ] Stateful

NACL

* [ ] Subnet level
* [ ] Stateless

### Mastery Check

* [ ] Explain SG vs NACL differences.

---

# Phase 11: Defense-in-Depth Architecture

## Learn

### Multiple Security Layers

User

↓

IAM

↓

VPC

↓

NACL

↓

Security Group

↓

Application

↓

Database

### Benefits

* [ ] Redundancy
* [ ] Reduced blast radius
* [ ] Improved resilience

### Project

* [ ] Build layered security architecture

### Mastery Check

* [ ] Design secure cloud infrastructure.

---

# Phase 12: Monitoring and Auditing

## Learn

### CloudTrail

Tracks:

* [ ] Login activity
* [ ] API calls
* [ ] Configuration changes

### AWS Config

Tracks:

* [ ] Resource compliance
* [ ] Configuration history

### Project

* [ ] Audit AWS account activity

### Mastery Check

* [ ] Investigate security incidents.

---

# Phase 13: Advanced IAM Security

## Learn

### Multi-Factor Authentication (MFA)

* [ ] User MFA
* [ ] Root MFA

### Temporary Credentials

* [ ] STS
* [ ] Role assumption

### Federation

* [ ] SSO
* [ ] Identity providers

### Project

* [ ] Implement secure authentication strategy

### Mastery Check

* [ ] Secure enterprise IAM environments.

---

# Phase 14: Security Architecture for Production

## Learn

### Production Design

Users

↓

IAM

↓

ALB

↓

ECS

↓

Database

### Security Goals

* [ ] Least privilege
* [ ] Zero trust
* [ ] Segmentation
* [ ] Monitoring

### Project

* [ ] Design enterprise-grade AWS security

### Mastery Check

* [ ] Review cloud security architecture.

---

# Veteran Mental Models

## Core Principles

* [ ] Trust nothing by default.
* [ ] Permissions should be temporary.
* [ ] Every permission increases risk.
* [ ] Security is layered.
* [ ] Deny by default.
* [ ] Assume credentials will eventually leak.

## Architecture Thinking

Always ask:

* [ ] Who needs access?
* [ ] Why do they need access?
* [ ] Can permissions be reduced?
* [ ] What happens if credentials are compromised?

---

# Veteran Projects

## Project 1

* [ ] IAM role-based EC2 architecture

## Project 2

* [ ] ECS task role implementation

## Project 3

* [ ] Secure VPC with NACLs and SGs

## Project 4

* [ ] CloudTrail auditing environment

## Project 5

* [ ] Enterprise security architecture review

---

# Veteran Mastery Checklist

## IAM Fundamentals

* [ ] Understand IAM architecture
* [ ] Understand policies
* [ ] Understand roles

## Access Control

* [ ] Apply least privilege
* [ ] Use temporary credentials
* [ ] Avoid access keys

## Network Security

* [ ] Configure Security Groups
* [ ] Configure NACLs
* [ ] Segment networks

## Monitoring

* [ ] Enable CloudTrail
* [ ] Audit permissions
* [ ] Detect unauthorized activity

## Architecture

* [ ] Build layered security
* [ ] Design secure VPCs
* [ ] Protect production workloads

---

# Final Veteran Benchmark

You have reached veteran level when you can:

* [ ] Explain IAM from first principles
* [ ] Design least-privilege architectures
* [ ] Secure EC2 and ECS workloads
* [ ] Build layered network defenses
* [ ] Implement role-based access control
* [ ] Audit AWS environments confidently
* [ ] Respond to security incidents effectively
* [ ] Architect enterprise-grade cloud security

---

# Real-World Production Security Architecture

Developer

↓

IAM User + MFA

↓

Assume Role

↓

AWS Resources

↓

Security Groups

↓

ECS Services

↓

Private Database

↓

CloudTrail Monitoring

### Production Checklist

* [ ] Root MFA enabled
* [ ] IAM roles used
* [ ] Least privilege policies applied
* [ ] Security Groups hardened
* [ ] NACLs configured
* [ ] CloudTrail enabled
* [ ] Secrets Manager used
* [ ] No hardcoded credentials
* [ ] Regular permission audits performed

### Golden Rule

Security is not a feature added later.

It is a continuous process of controlling identity, permissions, network access, and trust boundaries throughout the entire cloud architecture.

```
```
