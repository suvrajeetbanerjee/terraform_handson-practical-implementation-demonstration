<!-- # terraform_handson-practical-implementation-demonstration -->
Terraform HandsOn - Practical Implementation Demonstration [CDOH]

# Terraform-Driven Three-Tier AWS Architecture

![AWS 3-Tier Architecture](https://github.com/suvrajeetbanerjee/terraform_handson-practical-implementation-demonstration/blob/main/terraform-project-images/aws_3tier_architecture.png)

This project demonstrates a production-ready **three-tier web platform** built entirely with Terraform Infrastructure as Code (IaC). The implementation showcases best practices for AWS cloud architecture, security, and operational excellence.

## Table of Contents

- [Project Achievements & Learning Outcomes](#project-achievements--learning-outcomes)
- [Three-Tier Architecture Mapping](#three-tier-architecture-mapping)
- [AWS Resources Explained](#aws-resources-explained-40-services)
- [Infrastructure Relationships](#infrastructure-relationships)
- [Project Structure](#project-structure--source-code-guide)
- [Deployment Guide](#deployment-guide)
- [File-by-File Explanation](#file-by-file-explanation)
- [Terraform Best Practices](#terraform-code-construction-tips)

## Project Achievements & Learning Outcomes

This project takes a clean AWS account from zero to a production-ready **three-tier web platform** built entirely with Terraform. Major accomplishments include:

* **Fully-isolated VPC (10.0.0.0/16)** with public, private-app, and private-db subnets across three AZs for high availability
* **Auto Scaling Group** with an **Application Load Balancer** fronting stateless web servers; HTTPS can be enabled with ACM
* **Managed Amazon RDS (MySQL 8.0)** in a dedicated DB subnet group, reachable only from the application tier
* **End-to-end IaC**: every security group rule, route table, IAM role, and bootstrap script is source-controlled and reproducible
* **Horizontal scale** (1 → 3 instances) and vertical change (instance types, AMI updates) handled by **launch-template versioning**
* **Separation of concerns** illustrated via modules (`networking`, `autoscaling`, `database`) to reinforce Terraform DRY principles

### Key Skills Gained

* Advanced Terraform composition—`for_each`, remote modules, dynamic blocks
* AWS network-security design: SG vs. NACL, NAT vs. IGW, subnet strategy
* Operational excellence—password randomization, cloud-init, tagging standards, output values for pipelines

## Three-Tier Architecture Mapping

| Tier | Purpose | AWS Services/Resources in this project |
|------|---------|----------------------------------------|
| **Presentation Tier** | Public-facing entry point, terminates HTTP/HTTPS | Application Load Balancer, Internet Gateway, LB Security Group |
| **Application Tier** | Business logic, stateless web/API servers | Auto Scaling Group, Launch Template, EC2 Instances, Web-SG, NAT Gateway, App Route Tables |
| **Data Tier** | Durable state & backups | RDS MySQL Instance, DB Subnet Group, DB-SG, DB Route Tables |

**Network Design**: 
- **Public subnets** (10.0.101/102/103) for ALB + NAT
- **Private-app subnets** (10.0.1/2/3) for EC2 instances
- **Private-db subnets** (10.0.21/22/23) with no route to Internet Gateway

## AWS Resources Explained (40+ Services)

| # | Resource | Purpose |
|---|----------|---------|
| 1 | `aws_vpc` | Isolated network for all tiers |
| 2-4 | `aws_subnet` × 9 | 3 public, 3 app-private, 3 db-private subnets |
| 5 | `aws_internet_gateway` | Ingress/egress for ALB |
| 6 | `aws_nat_gateway` | Outbound internet for private EC2 |
| 7-9 | `aws_route_table` × 3 | Public, app-private, db-private routes |
| 10-18 | `aws_route_table_association` × 9 | Attach each subnet to correct RT |
| 19 | `aws_eip` | Static IP for NAT Gateway |
| 20 | `aws_db_subnet_group` | RDS high-AZ placement |
| 21 | `aws_security_group` (lb) | Allow :80 from 0.0.0.0/0 |
| 22 | `aws_security_group` (web) | Allow :8080 from lb SG, :22 from corp CIDR |
| 23 | `aws_security_group` (db) | Allow :3306 from web SG |
| 24 | `aws_iam_role` + policy | EC2 SSM/logs/RDS access |
| 25 | `aws_iam_instance_profile` | Attach role to EC2 |
| 26 | `aws_launch_template` | Golden EC2 definition + user-data |
| 27 | `data.cloudinit_config` | Inline cloud-init (yum-install, app start) |
| 28 | `aws_autoscaling_group` | Scale web servers 1–3 |
| 29-31 | `aws_lb` + listener + target group | Layer-7 load balancer |
| 32 | `aws_rds_instance` | MySQL 8.0 managed database |
| 33 | `random_password` | Generates 16-char DB secret |
| 34-40 | Terraform state-backend, provider blocks, and output values | House-keeping objects crucial for IaC |

## Infrastructure Relationships

The architecture implements a secure three-tier design with the following traffic flow:

* **Client Traffic**: Internet → ALB (Public Subnet) → EC2 Instances (Private App Subnet) → RDS (Private DB Subnet)
* **Outbound Traffic**: EC2 Instances → NAT Gateway → Internet Gateway (for updates and patches)
* **Health Checks**: ALB continuously monitors EC2 instance health on port 8080
* **Database Access**: Only application tier can communicate with RDS on port 3306

## Project Structure & Source-Code Guide

![Project Structure](https://github.com/suvrajeetbanerjee/terraform_handson-practical-implementation-demonstration/blob/main/terraform-project-images/terraform_project_structure.png)

![Detailed Project Structure](https://github.com/suvrajeetbanerjee/terraform_handson-practical-implementation-demonstration/blob/main/terraform-project-images/terraform_project_structure%20(1).png)

The repository follows Terraform best practices with a modular structure:

```
├── main.tf                          # Root configuration, wires modules together
├── providers.tf                     # AWS provider configuration
├── variables.tf                     # Input variables definition
├── versions.tf                      # Terraform and provider version constraints
├── outputs.tf                       # Output values for consumption
├── terraform.tfvars                 # Variable values (environment-specific)
└── modules/
    ├── networking/
    │   ├── main.tf                  # VPC, subnets, security groups
    │   ├── variables.tf             # Networking module inputs
    │   └── outputs.tf               # Networking module outputs
    ├── autoscaling/
    │   ├── main.tf                  # ALB, ASG, Launch Template
    │   ├── cloud_config.yaml        # EC2 bootstrap configuration
    │   ├── variables.tf             # Autoscaling module inputs
    │   └── outputs.tf               # Autoscaling module outputs
    └── database/
        ├── main.tf                  # RDS instance and configuration
        ├── variables.tf             # Database module inputs
        └── outputs.tf               # Database module outputs
```

### Key Components

* **Root Configuration**: Orchestrates module interactions and manages state
* **Networking Module**: Handles VPC, subnets, route tables, and security groups
* **Autoscaling Module**: Manages load balancer, auto scaling group, and EC2 configuration
* **Database Module**: Provisions RDS MySQL instance with secure networking

## Deployment Guide

### Prerequisites

- AWS CLI configured with appropriate permissions
- Terraform >= 1.0 installed
- SSH key pair created in target AWS region

### Deployment Steps

1. **Initialize Terraform**
   ```bash
   terraform init
   ```

2. **Review the Plan**
   ```bash
   terraform plan -out=tfplan
   ```

3. **Apply Configuration** (~8-10 minutes)
   ```bash
   terraform apply "tfplan"
   ```

4. **Access Application**
   ```bash
   # Get load balancer DNS name
   terraform output lb_dns_name
   
   # Access application
   curl http://<lb_dns_name>
   ```

5. **Scale Testing**
   ```bash
   aws autoscaling update-auto-scaling-group \
     --auto-scaling-group-name my-3-tier-architecture-asg \
     --desired-capacity 3
   ```

6. **Cleanup**
   ```bash
   terraform destroy
   ```

### Expected Outputs

```
lb_dns_name = "my-3-tier-architecture-123456789.us-west-2.elb.amazonaws.com"
db_password = <sensitive>
```

## File-by-File Explanation

| File | Purpose | Key Components |
|------|---------|----------------|
| `main.tf` | Root configuration | Module instantiation, inter-module references |
| `providers.tf` | Provider setup | AWS provider version and region configuration |
| `variables.tf` | Input definitions | Namespace, SSH keypair, region variables |
| `versions.tf` | Version constraints | Terraform core and provider version locks |
| `outputs.tf` | Output definitions | Load balancer DNS, database password |
| `terraform.tfvars` | Variable values | Environment-specific configuration |
| `modules/networking/main.tf` | Network infrastructure | VPC creation using terraform-aws-modules/vpc |
| `modules/autoscaling/main.tf` | Compute resources | Launch template, ASG, ALB configuration |
| `modules/autoscaling/cloud_config.yaml` | Instance bootstrap | Application deployment and startup scripts |
| `modules/database/main.tf` | Data persistence | RDS instance with random password generation |

## Terraform Code Construction Tips

### Module Design Principles

* **Separation of Concerns**: Each module handles a specific architectural tier
* **Reusability**: Modules can be used across different environments
* **Composability**: Root configuration orchestrates module interactions

### Best Practices Implemented

* **State Management**: Remote state backend configuration ready
* **Version Pinning**: All provider and module versions explicitly defined
* **Security**: Sensitive values handled through Terraform sensitive outputs
* **Tagging**: Consistent resource tagging for cost allocation and management
* **Documentation**: Comprehensive variable descriptions and output explanations

### Extension Points

* **SSL/TLS**: Add ACM certificate and Route 53 configuration
* **High Availability**: Upgrade to Aurora cluster for database tier
* **Security**: Implement WAFv2 web ACL for additional protection
* **Monitoring**: Add CloudWatch dashboards and alerts
* **CI/CD**: Integrate with AWS CodePipeline for automated deployments

## Security Considerations

* **Network Isolation**: Multi-tier subnet design with proper routing
* **Security Groups**: Principle of least privilege for all traffic
* **Database Security**: RDS in private subnet with encrypted storage
* **Access Control**: IAM roles and policies for EC2 instance permissions
* **Secrets Management**: Database passwords generated and stored securely

## Monitoring and Observability

* **Health Checks**: Application Load Balancer monitors instance health
* **Auto Scaling**: CloudWatch metrics trigger scaling events
* **Logging**: EC2 instances configured for CloudWatch logs integration
* **Metrics**: Built-in AWS service metrics for all components

## Cost Optimization

* **Right-sizing**: Instance types selected based on workload requirements
* **Auto Scaling**: Dynamic capacity adjustment based on demand
* **Reserved Capacity**: Consider Reserved Instances for predictable workloads
* **Resource Tagging**: Cost allocation and optimization tracking

---

**Note**: This implementation prioritizes security, scalability, and maintainability while demonstrating Infrastructure as Code best practices. The modular design enables easy customization and extension for various use cases.
