# AWS VPC Terraform Infrastructure

This Terraform code provisions a VPC in AWS, along with public and private subnets, an EC2 instance in a public subnet, and an associated security group. It also sets up necessary routing configurations and a NAT Gateway for internet access.

## Architecture Overview

- **VPC**: The code creates a Virtual Private Cloud (VPC) with CIDR block `10.0.0.0/16`.
- **Subnets**:
  - 3 **public subnets** spread across 3 different Availability Zones (AZs).
  - 3 **private subnets** spread across the same 3 Availability Zones.
- **Internet Gateway (IGW)**: Public subnets have an IGW attached to provide internet access.
- **NAT Gateway**: A NAT Gateway is deployed in one of the public subnets to allow private subnets to access the internet without direct inbound internet access.
- **Security Group**: A security group is created allowing HTTP (port 80) and SSH (port 22) access.
- **EC2 Instance**: A web server (nginx) is deployed on an EC2 instance in one of the public subnets, configured via user data.

## Requirements

- Terraform (v0.12 or later)
- AWS account with necessary permissions
- AWS credentials configured on your local machine

## Configuration

Before applying the Terraform code, modify the `variables.tf` file to set the values for:

- `vpc_cidr`: CIDR block for the VPC.
- `public_subnet_cidrs`: List of CIDR blocks for the public subnets.
- `private_subnet_cidrs`: List of CIDR blocks for the private subnets.
- `azs`: List of Availability Zones to deploy your resources.
- `ami_id`: The AMI ID for the EC2 instance (Amazon Linux 2 is recommended).
- `instance_type`: The instance type for the EC2 instance (e.g., `t2.micro`).
- `key_name`: The name of your AWS EC2 key pair for SSH access.

## Usage

1. Clone this repository:

   ```bash
   git clone <repository_url>
   cd <repository_directory>

   ```

2. Initialize the Terraform configuration:

`terraform init`

3. Review the execution plan:

`terraform plan`

4. Apply the Terraform configuration to create the resources:

`terraform apply`

5. To destroy the resources:

`terraform destroy`

6. Clean Up: If you no longer need the infrastructure, run the following command to clean up and destroy all the resources:

`terraform destroy`