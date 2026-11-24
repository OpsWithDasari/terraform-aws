# ☁️ Terraform with AWS – OpsWithDasari

Welcome to the **Terraform AWS Projects Repository!**

This repository is designed to help beginners and DevOps professionals learn Terraform and AWS from fundamentals to advanced concepts through hands-on practicals, infrastructure automation, and real-time cloud projects.

Learn how to provision, manage, modify, and destroy AWS infrastructure using Terraform and Infrastructure as Code (IaC).

## 🎯 Learning Objectives

- Understand Infrastructure as Code (IaC).
- Learn Terraform architecture and workflow.
- Install and configure Terraform.
- Understand Terraform providers and resources.
- Create and manage AWS infrastructure.
- Work with Terraform variables and outputs.
- Understand Terraform state management.
- Create reusable Terraform modules.
- Configure remote state using Amazon S3.
- Implement state locking.
- Understand Terraform workspaces.
- Automate AWS infrastructure provisioning.
- Implement Terraform in CI/CD pipelines.

## 📚 Topics Covered

### 1. Introduction to Terraform
- What is Terraform?
- What is Infrastructure as Code?
- Why Terraform?
- Terraform vs CloudFormation.
- Declarative vs Imperative approach.
- Terraform architecture.
- Terraform workflow.
- Terraform configuration language (HCL).

### 2. Terraform Installation and Configuration
- Terraform installation on Linux.
- Terraform installation on Windows.
- Terraform CLI configuration.
- Terraform version management.
- AWS CLI installation.
- AWS CLI configuration.
- AWS authentication and credentials.

### 3. Terraform Basic Commands
- terraform version
- terraform init
- terraform validate
- terraform fmt
- terraform plan
- terraform apply
- terraform destroy
- terraform show
- terraform output
- terraform providers

### 4. Terraform Configuration Files
- main.tf
- variables.tf
- outputs.tf
- providers.tf
- terraform.tf
- terraform.tfvars
- .gitignore

### 5. Terraform Providers and Resources
- What are Terraform providers?
- AWS provider configuration.
- Provider version constraints.
- Resource blocks.
- Data sources.
- Resource dependencies.
- Meta-arguments.
- count and for_each.
- depends_on.

### 6. Terraform Variables and Outputs
- Input variables.
- Variable types.
- Default values.
- Variable validation.
- Local values.
- Output values.
- Sensitive variables.
- Environment variables.
- tfvars files.

### 7. AWS Infrastructure Provisioning

**EC2**
- Launch EC2 instances.
- Configure instance types.
- Create key pairs.
- Security groups.
- User data scripts.

**VPC**
- Create VPC.
- Public and private subnets.
- Internet Gateway.
- NAT Gateway.
- Route tables.
- Network ACLs.

**S3**
- Create S3 buckets.
- Bucket versioning.
- Encryption.
- Bucket policies.
- Lifecycle rules.

**IAM**
- Create IAM users.
- IAM roles.
- IAM policies.
- Instance profiles.

**Other AWS Services**
- Application Load Balancer.
- Auto Scaling Groups.
- RDS databases.
- Route 53.
- CloudWatch.
- ECR.

### 8. Terraform State Management
- What is Terraform state?
- terraform.tfstate.
- Local state.
- Remote state.
- State locking.
- State backup.
- terraform state list.
- terraform state show.
- terraform state mv.
- terraform state rm.

### 9. Terraform Modules
- Introduction to modules.
- Root modules.
- Child modules.
- Module structure.
- Input variables.
- Module outputs.
- Module versioning.
- Reusable AWS modules.

### 10. Terraform Remote Backend
- What is a backend?
- Local backend.
- S3 remote backend.
- State locking with S3.
- Backend configuration.
- Remote state data source.
- Team collaboration using remote state.

### 11. Advanced Terraform Concepts
- Terraform workspaces.
- Dynamic blocks.
- Conditional expressions.
- for expressions.
- Lifecycle rules.
- Provisioners.
- Import existing infrastructure.
- Terraform refresh.
- Dependency management.
- Sensitive data management.

### 12. Terraform Automation and CI/CD
- Terraform with GitHub Actions.
- Terraform with Jenkins.
- Automated terraform plan.
- Automated terraform apply.
- Infrastructure deployment pipelines.
- Environment-based deployments.
- Terraform code validation.
- Infrastructure change management.

## 📂 Repository Structure

```text
terraform-aws/
│
├── README.md
│
├── 01-terraform-fundamentals/
├── 02-terraform-installation/
├── 03-terraform-basic-commands/
├── 04-terraform-configuration/
├── 05-terraform-variables-outputs/
│
├── 06-aws-ec2/
├── 07-aws-vpc/
├── 08-aws-s3/
├── 09-aws-iam/
├── 10-aws-security-groups/
├── 11-aws-load-balancer/
├── 12-aws-auto-scaling/
├── 13-aws-rds/
│
├── 14-terraform-modules/
├── 15-terraform-state-management/
├── 16-terraform-remote-backend/
├── 17-terraform-workspaces/
├── 18-terraform-advanced/
│
├── 19-terraform-github-actions/
├── 20-terraform-jenkins/
│
└── real-time-projects/
    ├── project-01-ec2-provisioning/
    ├── project-02-custom-vpc/
    ├── project-03-s3-bucket/
    ├── project-04-three-tier-architecture/
    ├── project-05-terraform-modules/
    └── project-06-terraform-cicd/
```

## 💻 First Terraform Practical – Create an AWS EC2 Instance

### Step 1: Configure AWS CLI

```bash
aws configure
```

Provide your AWS access key, secret key, region, and output format. Prefer IAM roles or temporary credentials when available.

### Step 2: Create Terraform Configuration

Create a file named `main.tf`.

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "devops_server" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t3.micro"

  tags = {
    Name        = "OpsWithDasari-EC2"
    Environment = "Dev"
  }
}

output "instance_id" {
  value = aws_instance.devops_server.id
}

output "public_ip" {
  value = aws_instance.devops_server.public_ip
}
```

**Note:** Replace the AMI placeholder with a valid AMI ID for your selected AWS region. Choose an instance type and configuration supported by your AWS account.

### Step 3: Initialize Terraform

```bash
terraform init
```

### Step 4: Validate Configuration

```bash
terraform validate
```

### Step 5: Review Infrastructure Changes

```bash
terraform plan
```

### Step 6: Create AWS Infrastructure

```bash
terraform apply
```

Review the execution plan and confirm when prompted.

### Step 7: Display Outputs

```bash
terraform output
```

### Step 8: Destroy Infrastructure

```bash
terraform destroy
```

Always verify the resources and costs before provisioning or destroying infrastructure.

## 📝 Sample Terraform Variables

Create `variables.tf`.

```hcl
variable "instance_type" {
  description = "AWS EC2 instance type"
  type        = string
  default     = "t3.micro"
}

variable "environment" {
  description = "Deployment environment"
  type        = string
  default     = "dev"
}

variable "aws_region" {
  description = "AWS deployment region"
  type        = string
  default     = "ap-south-1"
}
```

Use the variables in `main.tf`:

```hcl
provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "devops_server" {
  ami           = "ami-xxxxxxxx"
  instance_type = var.instance_type

  tags = {
    Name = "OpsWithDasari"
    Env  = var.environment
  }
}
```

## 🚀 Real-Time Terraform AWS Projects

1. Create EC2 instances using Terraform.
2. Build custom AWS VPC architecture.
3. Create public and private subnets.
4. Provision S3 buckets with versioning.
5. Automate IAM roles and policies.
6. Build an Application Load Balancer.
7. Configure Auto Scaling Groups.
8. Deploy a three-tier AWS architecture.
9. Create reusable Terraform modules.
10. Configure S3 remote state and state locking.
11. Deploy AWS infrastructure using Terraform and Jenkins.
12. Build an automated Terraform CI/CD pipeline using GitHub Actions.
13. Deploy container infrastructure using AWS ECR and ECS.
14. Provision an EKS cluster using Terraform.

## 🛠️ Prerequisites

- Basic Linux knowledge.
- Git and GitHub fundamentals.
- AWS account.
- Basic AWS service knowledge.
- Terraform installed.
- AWS CLI installed.
- Basic networking knowledge.
- Basic HCL and YAML knowledge.

## 🔐 Security Best Practices

- Never upload AWS access keys or secret keys to GitHub.
- Never commit terraform.tfstate files.
- Add sensitive files to .gitignore.
- Use IAM roles and temporary credentials.
- Enable encryption for remote state.
- Restrict access to S3 state buckets.
- Review Terraform plans before applying changes.
- Use approved versions of Terraform providers.
- Avoid storing secrets in plain-text tfvars files.

## 🎓 Who Can Use This Repository?

- Beginners learning Terraform.
- DevOps Engineers.
- AWS Cloud Engineers.
- Infrastructure Engineers.
- Site Reliability Engineers (SRE).
- Cloud Architects.
- Professionals preparing for Terraform and AWS interviews.

## 🌟 Learn. Practice. Automate. Deploy.

Follow **OpsWithDasari** for practical DevOps tutorials covering Linux, Shell Scripting, Git, GitHub, Docker, Kubernetes, Jenkins, Terraform, AWS, and CI/CD automation.

Happy Learning! 🚀
