
# EKS Cluster Deployment with Terraform

This repository contains Terraform configuration files to deploy an Amazon EKS (Elastic Kubernetes Service) cluster along with a managed node group in AWS.

---

## 📘 Overview

The Terraform configuration (`main.tf`) provisions:

- A **VPC** with public and private subnets across three availability zones
- An **EKS cluster** with both private and public endpoint access
- A **managed node group** with auto-scaling
- Necessary **IAM roles and policies** for both EKS and the node group
- **Output values** including cluster endpoint, certificate authority data, and cluster name

---

## ⚙️ Prerequisites

Ensure the following tools are installed and configured:

- **Terraform:** Version `>= 1.5.0`
- **AWS CLI:** Configured with valid credentials
- **AWS Account:** With permissions to create VPC, EKS, IAM, and EC2 resources
- **kubectl:** (Optional) For interacting with the deployed EKS cluster

---

## 📦 Configuration Details

### 🔧 Variables

- `region` – AWS region (default: `us-east-1`)
- `cluster_name` – Name of the EKS cluster (default: `my-eks-cluster`)
- `cluster_version` – Kubernetes version (default: `1.28`)

### 📁 Resources Created

- **VPC:** CIDR `10.0.0.0/16` with public and private subnets
- **EKS Cluster:** Public and private endpoint enabled
- **Node Group:** Uses `t3.medium` instances with:
  - Minimum size: `1`
  - Maximum size: `3`
  - Desired size: `2`
- **IAM Roles and Policies:** For EKS and the node group

---

## 🚀 Usage

### 1. Clone the Repository

```bash

git clone https://github.com/shivendra9203/Terraform-EKS-Cluster.git
cd <repository-directory>

```

### 2. Initialize Terraform

```bash

terraform init

```

### 3. Review and Customize Variables

Edit the `main.tf` or `variables.tf` to modify:
- `region`
- `cluster_name`
- `cluster_version`

### 4. Plan the Deployment

```bash

terraform plan

```

### 5. Apply the Configuration

```bash

terraform apply

```

Confirm by typing `yes` when prompted.

---

## 🔗 Access the Cluster

After deployment, configure `kubectl` to access your cluster:

```bash

aws eks update-kubeconfig --region <region> --name <cluster_name>

```

Use the output values (`cluster_endpoint`, `cluster_ca_certificate`) for custom integrations.

---

## 📤 Outputs

- `cluster_endpoint`: EKS API server endpoint
- `cluster_ca_certificate`: Certificate authority data
- `cluster_name`: EKS cluster name
- `availability_zones`: List of availability zones used

---

## 🧹 Cleanup

To destroy the infrastructure:

```bash

terraform destroy

```

Confirm with `yes` when prompted.

---

## 📝 Notes

- Ensure AWS credentials used have the required permissions.
- Adjust instance types by editing the `instance_types` in `main.tf`.
- VPC configuration is based on the module: `terraform-aws-modules/vpc/aws (~> 5.0)`

---

## 🛠️ Troubleshooting

- **IAM Policy Errors:** Check AWS credentials and ensure IAM permissions are correct.
- **EKS Cluster Access Issues:** Confirm `kubectl` is correctly configured.
- **Terraform Errors:** Review logs and AWS provider configurations.

---

## 📄 License

This project is licensed under the **MIT License**. See the `LICENSE` file for details.
