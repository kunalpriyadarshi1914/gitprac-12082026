# 🚀 gitprac-12082026 - Azure Terraform IaC Repository

![Terraform](https://img.shields.io/badge/Terraform-v1.0%2B-623CE4?logo=terraform&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-Cloud-0089D6?logo=microsoftazure&logoColor=white)
![Environments](https://img.shields.io/badge/Environments-Dev%20%7C%20Prod-10B981)
![Modules](https://img.shields.io/badge/Child%20Modules-14%20Modules-8B5CF6)

Yeh repository Ek **Modular Azure Infrastructure-as-Code (IaC)** project hai jisme reusable Terraform **Child Modules** aur **Parent Environments (`dev` & `prod`)** ka upyog karke Azure resources dynamic tarike se provision kiye jaate hain.

---

## 🌟 💻 Interactive Developer Portal (Single Click Portal)

Developers aur DevOps engineers ke samajhne ke liye humne ek **Interactive Visual Explorer (`index.html`)** banaya hai.

👉 **Interactive File Launch Karein:** [Open `index.html`](file:///c:/Users/kp4u2/OneDrive/Desktop/github-prac12082026/gitprac-12082026/index.html) *(`index.html` ko kisi bhi browser me open karein)*

### Interactive Portal Features:
- 🗺️ **Interactive Infrastructure Topology Graph**: Resource Groups, VNets, Subnets, VMs aur Public IPs ka live visual canvas map.
- 📦 **14 Child Modules Explorer**: Har module ka description, parameters, aur embedded source code modal preview.
- ⚖️ **Dev vs Prod Environment Comparison**: Subnet CIDRs, VM sizes (`Standard_B1s`), aur resource allocations ka dynamic breakdown.
- 💻 **DevOps Command Builder**: One-click copy ke saath `terraform init`, `plan`, `apply`, `destroy` aur target-based execution commands.
- 🌙 **Dark/Light Mode & Real-time Search**: Sleek design system & quick search filter.

---

## 🏗️ Architecture Overview

```mermaid
graph TD
    subgraph Resource_Group ["📦 Azure Resource Group (mod-rg8 / vmrg1-dev)"]
        subgraph VNet ["🌐 Virtual Network (10.0.0.0/16)"]
            subgraph Subnet1 ["🔒 App Subnet 1 (10.0.1.0/24)"]
                VM1["💻 Linux VM 1 (Standard_B1s)"]
                PIP1["🌍 Public IP 1 (Dynamic)"]
                VM1 --- PIP1
            end
            subgraph Subnet2 ["🔒 App Subnet 2 (10.0.2.0/24)"]
                VM2["💻 Linux VM 2 (Standard_B1s)"]
                PIP2["🌍 Public IP 2 (Dynamic)"]
                VM2 --- PIP2
            end
            subgraph BastionSubnet ["🛡️ Azure Bastion Subnet (10.0.4.0/26)"]
                Bastion["🏰 Azure Bastion Host"]
            end
        end
    </div>
```

---

## 📁 Repository Directory Structure

```text
gitprac-12082026/
├── index.html                       # 🌟 Interactive Developer Portal & Topology Visualizer
├── README.md                        # 📖 Comprehensive Repository Documentation
│
├── parent_modules/                  # 🏢 Environment Deployment Layers
│   ├── dev/                         # 🛠️ Development Environment
│   │   ├── main.tf                  # Module calls for DEV
│   │   ├── provider.tf              # AzureRM Provider configuration
│   │   ├── variable.tf              # Input variable definitions
│   │   └── terraform.tfvars         # Dev environment variables & map loops
│   └── prod/                        # 🚀 Production Environment
│       ├── main.tf                  # Module calls for PROD
│       ├── provider.tf              # AzureRM Provider configuration
│       ├── variable.tf              # Input variable definitions
│       └── terraform.tfvars         # Prod environment variables
│
└── child_modules/                   # 📦 Reusable Infrastructure Modules (14 Modules)
    ├── azurerm_resource_group/      # Resource Group provisioning
    ├── azurerm_vnet/                # Virtual Network management
    ├── azurerm_subnet/              # Subnet allocation
    ├── azurerm_virtual_machine/     # Linux VM + NIC + Public IP module
    ├── azurerm_public_ip_address/   # Public IP assignment
    ├── azurerm_NIC/                 # Network Interface Cards
    ├── azurerm_bastion/             # Azure Bastion Host gateway
    ├── azurerm_loadbalancer/        # Load Balancer & Backend pools
    ├── azurerm_NAT_gateway/         # NAT Gateway for outbound traffic
    ├── azurerm_nsg/                 # Network Security Groups
    ├── azurerm_nsg-rules/           # Security Rules filtering
    ├── azurerm_nsg_association/     # NSG Subnet association
    ├── azurerm_storage_account/     # Blob/Table Storage Accounts
    └── azurerm_vnet_peering/        # Cross-VNet Peering
```

---

## 📦 Child Modules Summary

| Module Name | Category | Description | Primary Input Variable |
| :--- | :--- | :--- | :--- |
| `azurerm_resource_group` | Core | Resource Group creation via dynamic maps | `var.rgs` / `var.rgprac` |
| `azurerm_vnet` | Network | Virtual Networks with custom address spaces | `var.vnets` / `var.vnetprac` |
| `azurerm_subnet` | Network | Subnets within VNets (App & Bastion subnets) | `var.subnets` / `var.subnetprac` |
| `azurerm_virtual_machine` | Compute | Ubuntu 22.04 LTS VMs with NICs & Public IPs | `var.vms` |
| `azurerm_public_ip_address` | Network | Dynamic/Static Public IP allocation | `var.pips` |
| `azurerm_NIC` | Network | Network Interface Cards | `var.nics` |
| `azurerm_bastion` | Security | RDP/SSH Secure Bastion Access | `var.bastion_hosts` |
| `azurerm_nsg` & `nsg-rules` | Security | Inbound/Outbound Port Filtering | `var.nsgs` & `var.nsg_rules` |
| `azurerm_storage_account` | Storage | Standard LRS Storage Accounts | `var.storage_accounts` |

---

## ⚖️ Environment Breakdown (`dev` vs `prod`)

| Feature | DEV (`parent_modules/dev`) | PROD (`parent_modules/prod`) |
| :--- | :--- | :--- |
| **Resource Groups** | `mod-rg8`, `git-rg11` | `vmrg1-dev`, `vmrg2-dev` |
| **VNet Address Space** | `10.0.0.0/16` (`mod-vnet8`) | `10.0.0.0/16`, `10.1.0.0/16` |
| **Subnets** | `10.0.1.0/24`, `10.0.2.0/24` | `10.0.1.0/24`, `10.0.2.0/24`, `10.0.4.0/26` (`AzureBastionSubnet`) |
| **VM Workloads** | `mod-vm8`, `mod-vm9` (`Standard_B1s`) | `shiva-vm1`, `shiva-vm2` (`Standard_B1s`) |
| **Bastion Host** | Optional | Configured (`bastion-production1914`) |

---

## 🛠️ Step-by-Step Deployment Guide

### 1. Azure Login
```bash
az login
az account set --subscription "<YOUR_SUBSCRIPTION_ID>"
```

### 2. Deploy DEV Environment
```bash
# Move to Dev folder
cd parent_modules/dev

# Initialize Terraform
terraform init

# Validate configuration
terraform validate

# Preview changes
terraform plan -var-file="terraform.tfvars"

# Apply changes
terraform apply -var-file="terraform.tfvars" -auto-approve
```

### 3. Deploy Target Module Only (e.g. Virtual Machines)
```bash
terraform apply -target=module.virtual_machine -var-file="terraform.tfvars"
```

### 4. Cleanup Infrastructure
```bash
terraform destroy -var-file="terraform.tfvars" -auto-approve
```

---

## 🔒 Security Best Practices

> [!CAUTION]
> - Never commit plain text passwords in production repositories. Use Azure Key Vault or Environment Variables (`TF_VAR_admin_password`).
> - Store `.tfstate` files in remote Azure Storage Containers with State Locking enabled.
> - Ensure Bastion Host or VPN access is enforced instead of exposing VM SSH ports directly to 0.0.0.0/0.

---

### 👤 Author & Contributor
- **DevOps Team**: Infrastructure & DevOps Practice
- **Project**: Azure Terraform Modular Automation (`gitprac-12082026`)
