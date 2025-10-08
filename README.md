# 🔐 Building a Secure Azure Environment

**Author:** Victor Mbogu  
**Title:** MSc in IT Security Management | Microsoft Certified: Azure Fundamentals | Microsoft Certified: Azure Security Engineer  
**Focus:** Secure Azure Environment with Logging, Key Vault Encryption, Networking, and Access Controls  
**Region:** Germany West Central  
**Subscription:** Azure Subscription 1  

---

## ✨ Introduction

This project demonstrates how to **build a fully secure, monitored, and segmented Azure environment** from scratch.  
It’s designed for **cloud enthusiasts, cybersecurity professionals, and learners** seeking hands-on exposure to real-world Azure security practices.

By following this lab, you’ll learn how to:  
- Implement **Identity and Access Management (IAM)** using least privilege and MFA.  
- Enable **centralized logging and monitoring** using Azure Monitor, Log Analytics, Defender, and Sentinel.  
- Secure data using **Key Vault** and **Customer-Managed Keys (CMK)** for encryption.  
- Design **segmented networks** using NSGs, subnets, and Bastion for controlled, private access.  

This project isn’t just theoretical — it’s a **replicable, portfolio-ready lab environment** that demonstrates your ability to design and deploy enterprise-grade cloud security architecture in Microsoft Azure.

---

## 🌍 Overview  

This lab focuses on building a **layered, defense-in-depth Azure environment** following Microsoft’s **Zero Trust principles**.  
Each security control — from IAM to encryption — is configured step by step, tested, and validated to ensure full compliance with Azure best practices.

**Core areas covered:**  
- 🔐 Identity and Access Management (IAM)  
- 📜 Logging and Activity Monitoring  
- 🧱 Network Segmentation and Traffic Control  
- 🔑 Data Encryption using Key Vault  
- 🧩 Secure VM Deployment with Bastion Access  
- ⚠️ Threat Detection with Defender for Cloud and Azure Sentinel  

---

## 🧩 Project Architecture  

| Component | Name | Purpose |
|------------|------|----------|
| **Resource Group** | `secure-lab-rg` | Logical container for all Azure resources |
| **Users & Groups** | Alice (Admin), Bob (Developer), Charlie (Viewer) | Role-based access control setup |
| **Log Analytics Workspace** | `secure-lab-logs` | Centralized log collection |
| **Storage Account** | `teststorageforlogs12` | Blob diagnostics and encryption testing |
| **Key Vault** | `securelab-keyvault` | Stores and manages encryption keys |
| **Virtual Network** | `securelab-vnet` | Private internal network |
| **Subnets** | `app-subnet`, `db-subnet`, `AzureBastionSubnet` | Segmented network tiers |
| **NSGs** | `app-nsg`, `db-nsg` | Control inbound/outbound traffic |
| **VMs** | `app-vm`, `db-vm` | Front-end and database workloads |
| **Bastion** | `securelab-bastion` | Secure browser-based RDP/SSH access |
| **Defender for Cloud** | Enabled | Continuous threat detection and compliance monitoring |
| **Azure Sentinel** | Integrated | Advanced SIEM and SOAR for real-time threat visibility |

---

## 🧱 Architecture Diagram  

![Architecture Diagram](https://github.com/victormbogu1/Reports-Presentations/blob/53862c002d00376b59e1e2ab7c604fcac4aba0f2/Pics/Diagram.png)

---

## 🔑 1. Identity and Access Management (IAM)

IAM ensures that **only authorized users and systems** can access resources while following **least privilege principles**.

**Key Concepts:**  
- **Principle of Least Privilege (PoLP):** Grant the minimal permissions needed.  
- **RBAC (Role-Based Access Control):** Assign roles instead of direct permissions.  
- **Privileged Identity Management (PIM):** Provide just-in-time elevated access.  
- **Conditional Access:** Enforce login policies based on device, risk, or location.  
- **Multi-Factor Authentication (MFA):** Add an additional security layer.  
- **Managed Identities:** Enable secure, passwordless access for applications.  

🎯 **Goal:** Prevent unauthorized access and privilege abuse.

---

## 📜 2. Logging & Monitoring  

Comprehensive logging provides full visibility into resource activities and user behavior.  

**Key Components:**  
- **Azure Monitor & Log Analytics:** Centralize log ingestion.  
- **Azure Activity Logs:** Track resource operations and changes.  
- **Azure AD Sign-In Logs:** Detect abnormal login attempts.  
- **Microsoft Defender & Sentinel:** Enable proactive threat detection and SIEM capabilities.  
- **Audit Logs:** Record configuration and policy changes.  
- **Retention Policies:** Define data storage duration for compliance.  

🎯 **Goal:** Detect, investigate, and respond to incidents effectively.

---

## 🔐 3. Encryption  

Encryption ensures that sensitive data remains protected both **at rest** and **in transit**.  

**Key Concepts:**  
- **Encryption in Transit:** Secure communication via TLS/HTTPS.  
- **Encryption at Rest:** Protect storage, database, and VM disks.  
- **Customer-Managed Keys (CMK):** Control encryption with your own keys in Key Vault.  
- **Secrets Management:** Store credentials securely — never hardcode them.  
- **Key Rotation:** Automate and enforce cryptographic hygiene.  

🎯 **Goal:** Maintain data confidentiality, integrity, and compliance.

---

## 🌐 4. Network Segmentation  

Proper segmentation limits exposure and minimizes lateral movement within the environment.  

**Key Concepts:**  
- **Virtual Networks (VNets):** Isolate workloads by function.  
- **Subnets & NSGs:** Apply firewall rules for traffic flow control.  
- **Zero Trust Architecture:** Always verify before granting access.  
- **Azure Bastion:** Secure VM access without exposing public IPs.  
- **Private Endpoints:** Enable private connections to Azure services.  
- **Azure Firewall/WAF:** Add an extra inspection layer for inbound/outbound protection.  

🎯 **Goal:** Reduce the attack surface and contain potential threats.

---

## ✅ 5. Integrated Security Layers  

| Common Breach Cause | Mitigation Strategy |
|--------------------|--------------------|
| Compromised accounts | Strong IAM + MFA |
| Undetected threats | Continuous logging + Sentinel |
| Data exposure | Encryption in transit & at rest |
| Malware spread | Network segmentation & NSG rules |

Each of these layers works together to create a **resilient, zero-trust cloud environment**.

---

## 🧩 Step-by-Step Implementation  

Follow these steps to replicate this secure Azure environment and validate each control:

### 🔑 Step 1: IAM

1. Create Resource Group:
   Name: secure-lab-rg
   Region: Germany West Central

2. Enable MFA in Azure AD for admins.

3. Assign RBAC roles:
   - Owner/Contributor for admins
   - Reader for monitoring
   - Key Vault Crypto Officer for encryption

4. Implement least privilege using custom roles if needed.

5. Enable System-assigned Managed Identity for VMs and Storage.

### 📜 Step 2: Logging:

1. Create Log Analytics Workspace:
   Name: secure-lab-logs
   Resource Group: secure-lab-rg

2. Connect Diagnostic Logs for Storage, Key Vault, and VMs.

3. Test logging by uploading/deleting files.

4. Create alerts:
   - Scope: secure-lab-logs
   - Condition: query results > 0
   - Action: send email
   - Name: Blob Deletion Alert

### 🔐 Step 3: Encryption:

1. Create Key Vault: securelab-keyvault
   - Access: Azure RBAC
   - Soft Delete: Enabled

2. Generate Key: storageencryptionkey (RSA 2048)

3. Enable CMK encryption on Storage Account using Key Vault.

4. Configure Key Rotation:
   - Expiry: 180 days
   - Auto-rotation: Enabled
   - Notify on rotation

### 🌐 Step 4: Network Segmentation

1. Create VNet: securelab-vnet (10.0.0.0/16)
   - Subnets: app-subnet (10.0.1.0/24), db-subnet (10.0.2.0/24)

2. Create NSGs:
   - app-nsg: Inbound HTTPS, Outbound Web
   - db-nsg: Inbound SQL, Outbound Deny

3. Associate NSGs with subnets.

4. Deploy VMs:
   - App VM: app-subnet
   - DB VM: db-subnet

5. Enable Azure Bastion for secure RDP/SSH
- AzureBastionSubnet (10.0.3.0/26) Bastion Host: securelab-bastion ---+ (Secure RDP/SSH - No Public IPs)

### 🧱 Step 5: Defender & Sentinel:

- Enable Microsoft Defender for Cloud on Storage, Key Vault, Servers, Network.
- Add Azure Sentinel to 'secure-lab-logs'.
- Create rules for blob deletion, failed logins, and unusual network traffic.
- Test and verify alerting.

### 🔒 Step 6: Private Endpoints:

- Create private endpoints for Storage & Key Vault.
- Connect to 'securelab-vnet' → 'db-subnet'.
- Disable public network access.
- Verify private connectivity.

### ✅ Step 7: Final Verification

- Check logs in Log Analytics.
- Confirm Defender & Sentinel monitoring.
- Test alerts and key rotation.

---

## 🧰 Troubleshooting Summary  

During deployment, several challenges were identified and resolved to ensure a seamless setup.  
Common issues included **RBAC propagation delays**, **Key Vault permission errors**, and **network rule misconfigurations**.  

Each was resolved through:
- Assigning correct **Key Vault Crypto Officer** roles to managed identities.  
- Allowing propagation time for **RBAC role assignments** (5–10 minutes).  
- Adjusting **key rotation policies** to comply with Azure limits.  
- Fine-tuning **NSG rules** to allow required inter-VM communication.  

This troubleshooting process reinforces the importance of patience, validation, and role verification when managing complex Azure environments.

---

## 📸 Final Resource Overview  

The screenshot below shows all resources used and configured for this project within the resource group:

![Resource_Group](https://github.com/victormbogu1/Reports-Presentations/blob/53862c002d00376b59e1e2ab7c604fcac4aba0f2/Pics/Screenshot%202025-10-07%20152013.jpg)

---

## 🧾 Final Checklist  

✅ **Resource Group:** `secure-lab-rg` created  
✅ **IAM:** Users & groups added, MFA enforced, RBAC applied  
✅ **Logging:** Log Analytics connected to Activity Logs and resources  
✅ **Storage:** Diagnostics enabled, blob deletion alerts tested  
✅ **Key Vault:** CMK linked to storage, key rotation configured  
✅ **Networking:** VNets, subnets, NSGs, and Bastion deployed  
✅ **Defender for Cloud:** Enabled and recommendations reviewed  
✅ **Sentinel:** Integrated for real-time monitoring  

---

## 🧩 Conclusion  

🎯 This project successfully demonstrates a **secure, monitored, and segmented Azure environment** featuring:  

| Security Layer | Implementation Highlights |
|----------------|---------------------------|
| **IAM** | MFA + RBAC with least privilege enforcement |
| **Logging** | Centralized log collection with alert automation |
| **Encryption** | CMK via Key Vault with auto-rotation |
| **Network Security** | Multi-tier architecture with NSGs and Bastion |
| **Monitoring** | Defender for Cloud & Sentinel threat detection |

All configurations were **tested for performance, logging, encryption, and monitoring reliability**, confirming a hardened, production-grade environment.

This project serves as a **blueprint for building enterprise-level Azure security architecture** — showcasing skills in **cloud governance, protection, and monitoring**.  

Whether you’re:  
- Preparing for Azure security certifications,  
- Showcasing your skills to potential employers, or  
- Building a secure environment for professional projects —  

this lab provides **hands-on, real-world experience** that bridges the gap between theory and practical implementation.

---

👨‍💻 *Built with passion for cloud security by **Victor Mbogu***  
© 2025 **Victor Mbogu** | Secure Azure Environment Project
