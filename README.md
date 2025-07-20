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

## 🛠️ Scripts Overview

| Script                          | Purpose                                                                 |
|----------------------------------|-------------------------------------------------------------------------|
| `create_zero_node_aws.sh`       | Launch EC2 instance with admin IAM role, instance profile, and tagging |
| `setup_zero_node_tools.sh`      | Update system, install CLI tools (AWS CLI, Git, jq, etc), setup SSH key and folders |
| `create_zero_terraform.sh`      | Install Terraform, create S3 bucket and DynamoDB table for backend     |
| `hcl.vault.sh`                  | Install Vault, configure `vault.hcl`, enable and start systemd service |

## 🚀 Quick Start
1. ✅ Launch EC2 with admin IAM role via AWS CLI:
```bash
create_zero_node_aws.sh
```

2. 🔐 Connect via SSH:
```bash
ssh -i ~/.ssh/My_mac.pem ubuntu@<PUBLIC_IP>
```

3. 🛠️ Install CLI toolchain and system setup:
```bash
setup_zero_node_tools.sh
```

4. 📦 Install Terraform and create backend (S3 + DynamoDB):
```bash
create_zero_terraform.sh
```

5. 🔒 Install and configure Vault:
```bash
hcl.vault.sh
```

6. 📍 Export Vault address:
```bash
export VAULT_ADDR=http://127.0.0.1:8200
```

7. 🧪 Check Vault status:
```bash
vault status
```

8. 🧷 (Optional) Initialize and unseal Vault (dev/test only):
```bash
vault operator init
vault operator unseal
```

9. 🏁 Vault is ready for use. You can now store and access secrets securely via CLI or API.nstall_vault.sh
```
---

## 📦 Terraform Remote Backend Sample

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-backend-zero-<timestamp>"
    key            = "terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks-zero-<timestamp>"
    encrypt        = true
  }
}
```

---

## 🧪 Requirements

- AWS CLI configured and authenticated
- SSH Key Pair (e.g., `My_mac.pem`)
- IAM permission to create:
  - EC2 instances
  - IAM roles / instance profiles
  - S3 buckets and DynamoDB tables

---

## 📄 License

MIT – free to use, modify, share.

---

## 👨‍💻 Author

**Alex Neverov**  
Platform Engineer · DevOps Engineer · Cloud & Infrastructure Automation · Industry PhD

- **GitHub:** [AlexandrNeverov](https://github.com/AlexandrNeverov)  
- **LinkedIn:** [linkedin.com/in/alexneverov](https://www.linkedin.com/in/alexneverov)  
- **Upwork:** [upwork.com/freelancers/~01c616035669bbf379](https://www.upwork.com/freelancers/~01c616035669bbf379)  
- **Website:** [neverov-it.com](https://neverov-it.com) · [neverov-science.com](https://neverov-science.com)  
- **Email:** [alex@neverov-it.com](mailto:alex@neverov-it.com)  
- **Phone:** +1 (754) 236‑5715




