# 🛡️ Secure Azure Environment Lab (Step-by-Step Implementation Guide)

**Author:** Victor Mbogu  
**Title:** MSc in IT Security Management | Microsoft Certified: Azure Fundamentals | Microsoft Certified: Azure Security Engineer
**Focus:** Building a Secure Azure Environment with Logging, Key Vault Encryption, Networking, and Access Controls  
**Region:** Germany West Central  
**Subscription:** Azure Subscription 1  

---

## 📘 Overview

This project documents the complete hands-on setup of a **Secure Azure Environment** from scratch, including:
- Identity & Access Management (RBAC, MFA)
- Activity & Diagnostic Logging
- Key Vault encryption with customer-managed keys (CMK)
- Virtual network segmentation with NSGs
- Bastion access for VMs (no public IPs)
- Alert rules using Log Analytics
- Security baselines with Microsoft Defender for Cloud

This serves as a reusable **blueprint** for secure Azure deployments — ideal for cybersecurity, cloud administration, or DevSecOps demonstrations.

---

## 🧩 Architecture Overview

**Key components:**
| Component | Name | Purpose |
|------------|------|----------|
| Resource Group | `secure-lab-rg` | Logical container for all resources |
| Log Analytics Workspace | `secure-lab-logs` | Centralized log collection |
| Storage Account | `teststorageforlogs12` | Blob diagnostics & encryption test |
| Key Vault | `securelab-keyvault` | Stores encryption keys |
| Virtual Network | `securelab-vnet` | Private network (10.0.0.0/16) |
| Subnets | `app-subnet`, `db-subnet`, `AzureBastionSubnet` | Segmented network tiers |
| NSGs | `app-nsg`, `db-nsg` | Network access control |
| VMs | `app-vm`, `db-vm` | Front-end and database tiers |
| Bastion | `securelab-bastion` | Secure remote access |
| Defender for Cloud | Enabled | Continuous security assessment |

---

## 🧱 Azure Secure Architecture Diagram

                +---------------------------------------------+
                |           Azure Resource Group              |
                |               (secure-lab-rg)               |
                +---------------------------------------------+
                              |              ^
                              |              |
                              v              |
               +---------------------------+ | Logs & Alerts
               |   Log Analytics Workspace |<----------------+
               |       (secure-lab-logs)   |
               +---------------------------+
                              |
                              v


                       +---------------------------+
                       |     Azure Key Vault       |
                       |   (securelab-keyvault)    |
                       | Stores CMKs for encryption|
                       +------------+--------------+
                                    |
                                    v
                       +---------------------------+
                       |  Storage Account          |
                       | (teststorageforlogs12)    |
                       | CMK Encryption via KV Key |
                       +---------------------------+

                       
| Virtual Network: securelab-vnet (10.0.0.0/16) |
| |
| +--------------------+ +--------------------+ |
| | app-subnet | | db-subnet | |
| | (10.0.1.0/24) | | (10.0.2.0/24) | |
| |--------------------| |--------------------| |
| | NSG: app-nsg | | NSG: db-nsg | |
| | VM: app-vm | <------> | VM: db-vm | |
| | Allow: 443 | | Allow: 1433 | |
| +--------------------+ +--------------------+ |
| |
| +-----------------------------------------+ |
| | AzureBastionSubnet (10.0.3.0/27) | |
| | Bastion Host: securelab-bastion |-------------+
| | (Secure RDP/SSH - No Public IPs) |
| +-----------------------------------------+
| |
+-----------------------------------------------------------------------+
