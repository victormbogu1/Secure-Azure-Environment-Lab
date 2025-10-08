# 🔐 Building a Secure Azure Environment

**Author:** Victor Mbogu  
**Title:** MSc in IT Security Management | Microsoft Certified: Azure Fundamentals | Microsoft Certified: Azure Security Engineer  
**Focus:** Secure Azure Environment with Logging, Key Vault Encryption, Networking, and Access Controls  
**Region:** Germany West Central  
**Subscription:** Azure Subscription 1  

---

## 🌍 Overview  

This project demonstrates how to design and implement a **secure cloud infrastructure** on **Microsoft Azure** using best security practices.  

We’ll build a **layered security environment** that covers:  
- 🔐 Identity and Access Management (IAM)  
- 📜 Logging and Activity Monitoring  
- 🧱 Network Segmentation with NSGs  
- 🔑 Data Encryption with Azure Key Vault  
- 🧩 Secure VM Deployment with Bastion Access  
- ⚠️ Alerts, Defender for Cloud, and Real-Time Monitoring  

Every component is configured **step-by-step**, tested, and validated.  

---

## 🧩 Project Architecture  

Here’s an overview of the key Azure components we created:  

| Component | Name | Purpose |
|------------|------|----------|
| Resource Group | `secure-lab-rg` | Logical container for all Azure resources |
| Users & Groups | Alice (Admin), Bob (Developer), Charlie (Viewer) | Identity and Access setup |
| Log Analytics Workspace | `secure-lab-logs` | Centralized logging and diagnostics |
| Storage Account | `teststorageforlogs12` | Blob diagnostics and CMK encryption testing |
| Key Vault | `securelab-keyvault` | Holds customer-managed encryption keys |
| Virtual Network | `securelab-vnet` | Private internal network |
| Subnets | `app-subnet`, `db-subnet`, `AzureBastionSubnet` | Segmented network tiers |
| NSGs | `app-nsg`, `db-nsg` | Firewall rules for inbound/outbound control |
| VMs | `app-vm`, `db-vm` | Front-end and database workloads |
| Bastion | `securelab-bastion` | Secure, browser-based RDP access (no public IP) |
| Defender for Cloud | Enabled | Continuous security assessment and recommendations |

---

## 🧱 Architecture Diagram (with Monitoring)

```text
+------------------------------------------------------+
|             Azure Resource Group (secure-lab-rg)    |
+----------------------+-------------------------------+
                       |            
                       v
+-------------------------------+
|   Log Analytics Workspace     |
|       (secure-lab-logs)      |
+-------------------------------+
          ^
          |
          +----- Logs & Alerts
          |
          v
+-------------------------------+
| Microsoft Defender & Sentinel |
|   Threat Detection & SIEM     |
+-------------------------------+

+------------------------------------------------------+
| Virtual Network: securelab-vnet (10.0.0.0/16)      |
|                                                      |
|  +----------------------+  +----------------------+ |
|  | app-subnet           |  | db-subnet            | |
|  | (10.0.1.0/24)        |  | (10.0.2.0/24)        | |
|  |----------------------|  |----------------------| |
|  | NSG: app-nsg         |  | NSG: db-nsg          | |
|  | VM: app-vm           |  | VM: db-vm            | |
|  | Allow: HTTPS (443)   |  | Allow: SQL (1433)    | |
|  +----------------------+  +----------------------+ |
|                                                      |
|  +---------------------------------------------+   |
|  | AzureBastionSubnet (10.0.3.0/27)           |   |
|  | Bastion Host: securelab-bastion            |---+
|  | (Secure RDP/SSH - No Public IPs)          |
|  +---------------------------------------------+
+------------------------------------------------------+

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



## 🔑 1. Identity and Access Management (IAM)

IAM ensures only the **right people or systems** have access to resources with the **least privilege**.

**Key Concepts:**

- **Principle of Least Privilege (PoLP):** Grant minimal permissions.  
- **Role-Based Access Control (RBAC):** Assign roles instead of direct permissions.  
- **Privileged Identity Management (PIM):** Temporary admin access.  
- **Conditional Access Policies:** Secure logins based on device, location, or risk.  
- **Multi-Factor Authentication (MFA):** Adds extra security.  
- **Service Principals & Managed Identities:** For secure, credential-free app access.  

**🎯 Goal:** Prevent attackers from misusing accounts.

---

## 📜 2. Logging

Logging provides visibility and an **audit trail**.

**Key Components:**

- **Azure Monitor & Log Analytics:** Centralized log collection.  
- **Azure Activity Logs:** Tracks management-plane activities.  
- **Azure AD Sign-In Logs:** Detect suspicious logins.  
- **Microsoft Defender & Sentinel:** Advanced threat detection and SIEM/SOAR.  
- **Audit Logs:** Track configuration changes and policy violations.  
- **Retention Policies:** Define how long logs are kept.  

**🎯 Goal:** Detect, investigate, and respond to threats quickly.

---

## 🔐 3. Encryption

Encryption protects data confidentiality and integrity.

**Key Concepts:**

- **Encryption in Transit:** TLS/HTTPS for all communications.  
- **Encryption at Rest:** Understand Azure Storage/Database/VM defaults.  
- **Customer-Managed Keys (CMK):** Use Key Vault for custom keys.  
- **Secrets Management:** Avoid hardcoding passwords/keys.  
- **Disk Encryption:** Enable Azure Disk Encryption for sensitive VMs.  

**🎯 Goal:** Keep data safe even if systems are compromised.

---

## 🌐 4. Network Segmentation

Segment networks to **limit attack surfaces**.

**Key Concepts:**

- **Virtual Networks (VNets):** Isolate workloads.  
- **Subnets:** Divide VNets by trust levels.  
- **Network Security Groups (NSGs):** Control traffic per subnet/NIC.  
- **Firewalls & WAF:** Inspect traffic between segments.  
- **Zero Trust Principles:** Always verify access.  
- **Private Endpoints:** Secure service connectivity.  
- **Environment Segregation:** Keep dev/test/prod separate.  

**🎯 Goal:** Prevent lateral movement after compromise.

---

## ✅ 5. Putting It All Together

By mastering **IAM, Logging, Encryption, and Network Segmentation**, you mitigate **80% of cloud security risks**.  

| Common Breach Cause | Mitigation |
|--------------------|------------|
| Compromised accounts | Strong IAM + MFA |
| Undetected attacks | Logging & Sentinel |
| Exposed data | Encryption at rest & transit |
| Malware spread | Network segmentation |

---

## 🧩 Step-by-Step Implementation

Follow these steps to **replicate this secure Azure environment**.

---

### 🔑 Step 1: IAM

```text
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

📜 Step 2: Logging:

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

🔐 Step 3: Encryption:

1. Create Key Vault: securelab-keyvault
   - Access: Azure RBAC
   - Soft Delete: Enabled

2. Generate Key: storageencryptionkey (RSA 2048)

3. Enable CMK encryption on Storage Account using Key Vault.

4. Configure Key Rotation:
   - Expiry: 180 days
   - Auto-rotation: Enabled
   - Notify on rotation

🌐 Step 4: Network Segmentation

1. Create VNet: securelab-vnet (10.0.0.0/16)
   - Subnets: app-subnet (10.0.1.0/24), db-subnet (10.0.2.0/24)

2. Create NSGs:
   - app-nsg: Inbound HTTPS, Outbound Web
   - db-nsg: Inbound SQL, Outbound Deny

3. Associate NSGs with subnets.

4. Deploy VMs:
   - App VM: app-subnet
   - DB VM: db-subnet

5. Optional: Enable Azure Bastion for secure RDP/SSH

🧱 Step 5: Defender & Sentinel:

- Enable Microsoft Defender for Cloud on Storage, Key Vault, Servers, Network.
- Add Azure Sentinel to 'secure-lab-logs'.
- Create rules for blob deletion, failed logins, and unusual network traffic.
- Test and verify alerting.

🔒 Step 6: Private Endpoints:

- Create private endpoints for Storage & Key Vault.
- Connect to 'securelab-vnet' → 'db-subnet'.
- Disable public network access.
- Verify private connectivity.

✅ Step 7: Final Verification

- Check logs in Log Analytics.
- Confirm Defender & Sentinel monitoring.
- Test alerts and key rotation.

## 🧾 Conclusion

You’ve built a **secure, monitored, and segmented Azure environment**:

| Area             | Implementation             |
|-----------------|----------------------------|
| IAM              | RBAC & MFA                 |
| Logging          | Centralized logs & alerts  |
| Encryption       | Key Vault & CMK            |
| Network Security | NSGs, subnets, Bastion     |
| Monitoring       | Defender & Sentinel        |

This project demonstrates **real-world Azure security practices**.
