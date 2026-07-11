

Phase 1 — Networking (Week 1)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Build only the networking layer.

Learn
CIDR
Public vs Private Subnets
Internet Gateway
NAT Gateway
Route Tables
Build
terraform/
    vpc.tf
    subnet.tf
    igw.tf
    nat.tf
    routes.tf

Deploy

VPC
2 Public Subnets
2 Private App Subnets
2 Private DB Subnets
Internet Gateway
NAT Gateway
Route Tables
Deliverable

Your first architecture should look like:

VPC

├── Public Subnet A
├── Public Subnet B
├── Private App A
├── Private App B
├── Private DB A
└── Private DB B


Phase 2 — Security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create

Security Groups
IAM Roles

Rules

Internet

↓

ALB SG

↓

EC2 SG

↓

RDS SG

Meaning

Internet can only access ALB.

EC2 accepts traffic only from ALB.

Database accepts traffic only from EC2.


Phase 3 — Compute Layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Deploy

Launch Template
EC2
Auto Scaling Group

Instead of launching EC2 manually,

Terraform creates

Launch Template

↓

Auto Scaling Group

↓

EC2 Instances

Install

Nginx
Apache
Demo application

using User Data.


Phase 4 — Database Layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Deploy

RDS MySQL

Requirements

Private subnet only
Multi-AZ
Automated backups
Encryption enabled

Don't expose the DB publicly.


Phase 5 — Load Balancer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create

Internet

↓

Application Load Balancer

↓

Target Group

↓

EC2 Auto Scaling Group

Configure

Health Checks
Listener
Target Group

Test

Stop one EC2 instance.

Traffic should automatically go to the healthy instance.


Phase 6 — Monitoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add

CloudWatch

CPU Alarm
Memory Alarm
Disk Alarm

SNS

Receive email alerts.


Phase 7 — Logging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Enable

CloudTrail
VPC Flow Logs
ALB Access Logs
CloudWatch Logs


Phase 8 — Terraform Best Practices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Your repository should be structured like this:

terraform-project/

├── README.md
├── architecture.png
├── .gitignore
├── backend.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars.example
├── versions.tf
│
├── modules/
│   ├── vpc/
│   ├── security/
│   ├── alb/
│   ├── ec2/
│   ├── rds/
│   └── monitoring/
│
├── environments/
│   ├── dev/
│   ├── stage/
│   └── prod/
│
└── scripts/

This modular layout is much closer to what you'll find in production environments than a flat directory of .tf files.


Phase 9 — CI/CD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a GitHub Actions workflow:

GitHub

↓

Terraform fmt

↓

Terraform validate

↓

Terraform plan

↓

Approval

↓

Terraform apply

This demonstrates infrastructure automation and change management.


Phase 10 — Production Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add features that distinguish your project from basic tutorials:

Auto Scaling based on CPU utilization.
Multi-AZ deployment for high availability.
S3 remote backend with DynamoDB state locking.
Parameterize resources with variables.
Use remote modules.
Store sensitive values securely (avoid hardcoding).
Health checks and self-healing.
Reusable code for different environments.
Resource tagging for cost allocation.
Lifecycle rules for Terraform-managed resources.