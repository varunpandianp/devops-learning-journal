# Terraform

## Overview

Terraform is an Infrastructure as Code (IaC) tool used to provision and manage cloud infrastructure using configuration files.

I am learning Terraform to automate AWS infrastructure creation and follow DevOps best practices.


# Why Terraform is Important in DevOps

Terraform helps engineers:

- Automate infrastructure creation
- Maintain infrastructure as code
- Version control infrastructure
- Create repeatable environments
- Reduce manual configuration


# Core Concepts Learned


## Providers

Plugins that allow Terraform to communicate with cloud platforms.

Example:

AWS Provider


## Resources

Infrastructure components managed by Terraform.

Examples:

- EC2
- VPC
- Subnet
- Security Group


## Variables

Used to make configurations reusable.


## Outputs

Display useful information after deployment.


## State File

Terraform state stores information about managed infrastructure.


## Modules

Reusable Terraform configurations.


# Terraform Workflow


Write Configuration

↓

terraform init

↓

terraform plan

↓

terraform apply

↓

Infrastructure Created


# AWS Resources Practiced

- EC2
- VPC
- Subnets
- Internet Gateway
- Route Tables
- Security Groups
- Load Balancers
- Auto Scaling


# Terraform Best Practices Learned

- Use modules
- Maintain state securely
- Use variables
- Follow folder structure
- Review plans before applying


# Troubleshooting Areas

- AWS permission errors
- State issues
- Resource conflicts
- Module errors


# Related Technologies

- AWS
- Docker
- Kubernetes
- CI/CD