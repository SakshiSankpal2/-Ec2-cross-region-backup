# Enable Cross-Region Backup Replication for EC2 using AWS Backup

## 🧭 Objective

Automatically back up an EC2 instance in the **Mumbai (ap-south-1)** region and replicate it to **N. Virginia (us-east-1)** or **Oregon (us-west-2)** using AWS Backup. This setup enhances **disaster recovery**, **data durability**, and **regional resilience** with minimal manual intervention.

---

## 🛠️ Tools & Services Used

| Service           | Purpose                                        |
|-------------------|------------------------------------------------|
| Amazon EC2        | Primary instance to be backed up               |
| AWS Backup        | Service to create and manage backup lifecycle  |
| IAM Role          | Grants AWS Backup access to EC2                |
| AWS Backup Vault  | Secure location to store backup data           |

---

## 📋 Implementation Steps

### ✅ 1. EC2 Instance Setup in Mumbai
- Launch EC2 in **ap-south-1** (Amazon Linux 2)
- Configure security group to allow SSH (22) and HTTP (80)
- Instance Name: `MyBackupEC2`

### ✅ 2. Create Backup Vault
- Go to AWS Backup → **Backup vaults** → Create vault
- Name: `My_Backup`
- Encryption: Default

### ✅ 3. Configure Backup Plan
- Navigate to AWS Backup → Create Backup Plan
- Plan Name: `MyBackupPlan`
- Rule Name: `DailyEC2Backup`
- Frequency: Daily
- Backup Vault: `My_Backup`

### ✅ 4. Assign EC2 to Backup Plan
- Assignment Name: `EC2Assignment`
- Resource Type: EC2
- Select `MyBackupEC2`
- IAM Role: `Backup_Default_Role`

### ✅ 5. Enable Cross-Region Backup Copy
- Destination Region: **N. Virginia** or **Oregon**
- Create destination vault: `My_Backup_US` or `My_Backup_OR`
- Retention Period: 30 days

### ✅ 6. Validate Backup & Replication
- Trigger **On-Demand Backup**
- Monitor Backup Jobs → Ensure `Completed` status
- Switch to target region → Check recovery points

---

## 📦 Final Deliverables

| Deliverable                         | Status    |
|------------------------------------|-----------|
| Source & Destination Vaults        | ✅ Created |
| Backup Plan with Copy Rules        | ✅ Configured |
| EC2 Backup Jobs                    | ✅ Verified |
| Cross-Region Recovery Points       | ✅ Verified |

---

## ✅ Key Benefits

- **Regional fault tolerance**
- **Automated disaster recovery**
- **Secure and scalable backups**
- **No third-party tools required**

---

## ⚠️ Common Challenges & Solutions

| Challenge                     | Resolution                        |
|------------------------------|------------------------------------|
| IAM Role permission issues   | Used `Backup_Default_Role`         |
| Region mismatch errors       | Verified destination != source     |
| EC2 not listed in resources  | Ensured same account & region      |

---

## 📌 Conclusion

This solution demonstrates how to set up a robust, **cross-region EC2 backup strategy** using native AWS services. It ensures **business continuity**, **compliance**, and **cost-effective disaster recovery** without the need for complex tooling.