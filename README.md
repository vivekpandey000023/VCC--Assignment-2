# GCP VM Auto-Scaling & Security Config For VCC Project

## Overview

The repository contains:
- Scripts to create a VM instance with Apache installed.
- Scripts to create an instance template and Managed Instance Group (MIG) for auto-scaling.
- Scripts to configure custom firewall rules (allowing only a specific IP, e.g., `223.238.204.234/32`).
- Scripts to set up IAM roles for restricted access

## Setup and Deployment Instructions

### 1. Create and Configure a VM Instance

#### Using the `scripts/create_vm.sh` Script:
1. **Edit the Script:**  
   Replace `your-project-id` with your actual GCP project ID.
2. **Make It Executable and Run:**
   ```bash
   chmod +x scripts/create_vm.sh
   ./scripts/create_vm.sh
   ```

This script creates a VM instance (named assignment-2-gcp-vm) in the specified zone with the Apache web server installed (which listens on port 80).

**Manual Verification:**
- **SSH into the Instance:**
  From the GCP Console, click the "SSH" button next to your VM.
- **Check Apache Status:**
  Run:
  ```bash
  sudo systemctl status apache2
  ```
  You should see Apache running.

### 2. Configure Auto-Scaling

**Create an Instance Template with scripts/create_instance_template.sh:**
1. **Edit the Script:**
   Replace `your-project-id` with your actual project details.
2. **Run the Script:**
   ```bash
   chmod +x scripts/create_instance_template.sh
   ./scripts/create_instance_template.sh
   ```

**Create a Managed Instance Group (MIG) with scripts/create_mig.sh:**
1. **Edit the Script:**
   Adjust any necessary parameters.
2. **Run the Script:**
   ```bash
   chmod +x scripts/create_mig.sh
   ./scripts/create_mig.sh
   ```

The script creates a MIG using the instance template and configures auto-scaling with the following parameters:
- Target CPU Utilization: 60%
- Min Instances: 1
- Max Instances: 5
- Cooldown Period: 60 seconds

### 3. Configure Security Measures

**Firewall Rules via scripts/setup_firewall.sh:**
1. **Edit the Script:**
   Set the ALLOWED_IP variable to your allowed IP (e.g., 223.238.204.234/32).
2. **Run the Script:**
   ```bash
   chmod +x scripts/setup_firewall.sh
   ./scripts/setup_firewall.sh
   ```

This configures firewall rules to allow only HTTP (port 80) and HTTPS (port 443) traffic from the specified IP.

**IAM Roles via scripts/setup_iam.sh:**
1. **Edit the Script:**
   Replace `your-project-id` and `user@example.com` with your project ID and the appropriate user email.
2. **Run the Script:**
   ```bash
   chmod +x scripts/setup_iam.sh
   ./scripts/setup_iam.sh
   ```

This assigns the Compute Viewer role (or any additional roles) to the specified user.



## Conclusion

This repository delivers a professional, complete implementation of GCP auto-scaling and security measures. It covers:

1. Automated VM creation and Apache installation.
2. Auto-scaling configuration with Managed Instance Groups.
3. Firewall and IAM setup to restrict access.
4. Comprehensive testing using curl, nmap, stress, and online tools.
5. Optional Terraform configuration for Infrastructure-as-Code.
6. Detailed documentation and a final project report.
