# Cloud Bootstrap Automation with Terraform & Vault ☁️

![Admin Terraform Bootstrap EC2 Demo](https://raw.githubusercontent.com/AlexandrNeverov/vault-iac-bootstrap/main/image.png)

## 🚀 Why This Matters

Setting up an EC2 instance for Terraform and Vault experiments usually takes time: configuring IAM roles, launching instances, installing tools, provisioning backend state storage — all manually.

**`zero-node-infra-bootstrap` automates this process in 4 isolated scripts**:

- You get an EC2 instance with full admin rights via IAM role
- It comes preinstalled with Terraform, Vault, and CLI tools
- Remote backend is auto-configured: S3 + DynamoDB
- Vault is installed, configured, and launched as a systemd service

This is ideal for:

- 🔁 Reproducible lab/test environments
- 💡 Bootstrapping Terraform experiments without local setup
- 🧪 Teaching and running Vault or backend workshops on real AWS infra
- ⚙️ Minimal secure AWS setups via instance profile (no static credentials)

---

## ✅ Features

- 🖥️ EC2 provisioning script with admin IAM role & instance profile
- 🪄 Automated creation of:
  - S3 bucket (versioning enabled)
  - DynamoDB table for state locking
- 🧰 Preinstalled tools:
  - Terraform, AWS CLI, Vault
  - Git, jq, curl, unzip, tmux, htop, Python3, pip3
- 🔐 Vault installation with systemd service and basic `vault.hcl`
- 📦 Directory setup: `~/projects/terraform`, `~/projects/ansible`, public IP logging
- 🔑 SSH key generation and export
- 🧱 Fully modular: each script works standalone or combined

> All actions are performed via CLI using official AWS APIs and require only existing access credentials with IAM privileges.
