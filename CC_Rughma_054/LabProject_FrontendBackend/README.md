# Lab Project: Terraform + Ansible Roles (Nginx HA + 3 Backends)

**Name:** Rughma Malik

**Roll Number:** 2023-BSE-054

**Semester:** V-B

**Course:** Cloud Computing Lab

---

## Project Overview
This project deploys a **High Availability (HA) Web Architecture** on AWS using **Infrastructure as Code (IaC)**.
It uses **Terraform** to provision the infrastructure and **Ansible Roles** to automatically configure the software.

### Architecture Design
- **1 Frontend Server (Nginx):** Acts as a reverse proxy and load balancer.
- **3 Backend Servers (Apache HTTPD):**
  - **2 Active Servers:** Handle normal traffic (Round-robin).
  - **1 Backup Server:** Only handles traffic if *both* active servers fail.
- **Automation:** Terraform automatically generates the Ansible inventory and runs the playbook upon provisioning.

---

## How to Run
1. **Initialize Terraform:**
   ```bash
   terraform init
   ```
2. **Deploy Infrastructure & Config:**
   ```bash
   terraform apply -auto-approve
   ```
   Note: This command will provision EC2 instances, wait for SSH to be ready, and trigger the Ansible playbook automatically.
3. **Verify Output: Terraform will output the public IPs of the frontend and backends.**
   ```bash
   terraform output
   ```

## Verification Checklist

### Repo Structure:

![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image.png)
### Terraform Plan/Apply:

1. **terraform init works.**
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image0.png)
2. **terraform apply -auto-approve successfully:**
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image-1.png)
### Runtime Behavior:

1. **`http://<backend-N-public-ip>/` shows distinct backend pages.**
- Backend-1:
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image-2.png)
- Backend-2:
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image-3.png)
**2. `http://<frontend-public-ip>/` alternates between backend 1 and backend 2 responses.**
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image-4.png)
**3. When backend 1 and 2 httpd services are stopped:**
- `http://<frontend-public-ip>/` returns backup backend page.
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image-5.png)

### Automation:

```bash
terraform destroy -auto-approve
```
![alt text](/CC_Rughma_054/LabProject_FrontendBackend/screenshots/image-6.png)

