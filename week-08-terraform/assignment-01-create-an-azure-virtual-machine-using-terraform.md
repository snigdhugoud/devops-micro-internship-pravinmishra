# Assignment 1 — Create an Azure Virtual Machine using Terraform

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will use Terraform to provision a complete Azure Virtual Machine environment, including a resource group, virtual network, subnet, public IP, network interface, and a Linux-based virtual machine. You will set up and verify the required local tools, define the infrastructure in Terraform, initialize the project, review and apply the plan, verify the running VM through Azure CLI, capture the public IP output, and destroy the resources after testing.

---

# Task 0 — Set Up and Verify the Terraform and Azure CLI Environment

## Goal

Prepare your local environment for Terraform deployment by installing Terraform, Azure CLI, and the HashiCorp Terraform extension in VS Code, signing in to your Azure account, and confirming that all required tools are working correctly.

### Evidence

#### Screenshot 1 — Terminal showing successful `terraform version` output

<img width="1920" height="1080" alt="Screenshot (82)" src="https://github.com/user-attachments/assets/1e65ea41-27e6-4d6c-974d-0a999d0d39fa" />
<img width="1920" height="1080" alt="Screenshot (83)" src="https://github.com/user-attachments/assets/c9594207-d46e-4fa0-916e-d90cc5523da7" />
<img width="1920" height="1080" alt="Screenshot (84)" src="https://github.com/user-attachments/assets/aa548101-56a1-4aed-a3e1-5672b153a7b9" />
<img width="1920" height="1080" alt="Screenshot (85)" src="https://github.com/user-attachments/assets/31125b7a-87af-4f98-b1c0-88c997aecadb" />
<img width="1920" height="1080" alt="Screenshot (86)" src="https://github.com/user-attachments/assets/0b22cf41-ae12-4365-94c6-c914c1aae329" />


---

#### Screenshot 2 — Terminal showing successful `az version` output

Add your screenshot here.

---

#### Screenshot 3 — VS Code Extensions panel showing the HashiCorp Terraform extension installed and enabled

Add your screenshot here.

---

# Task 1 — Create a New Terraform Project and Define the Infrastructure

## Goal

Create a new Terraform project and define the complete Azure Virtual Machine environment in `main.tf` by using the official Terraform Registry documentation.

### Evidence

#### Screenshot 4 — VS Code showing the AzureRM provider configuration and resource group configuration in `main.tf`

Add your screenshot here.

---

#### Screenshot 5 — VS Code showing the Linux virtual machine configuration and public IP `output` block in `main.tf`. Ensure that the VM password is hidden or redacted

Add your screenshot here.

---

# Task 2 — Initialize Terraform

## Goal

Initialize the Terraform working directory and download the required provider components.

### Evidence

#### Screenshot 6 — Terminal showing the successful `terraform init` output

Add your screenshot here.

---

# Task 3 — Plan and Apply the Configuration

## Goal

Review the Terraform execution plan and provision the Azure resources.

### Evidence

#### Screenshot 7 — Terraform plan summary showing the proposed resources

Add your screenshot here.

---

#### Screenshot 8 — Terraform apply output showing successful completion

Add your screenshot here.

---

#### Screenshot 9 — Terraform output showing the public IP address of the VM

Add your screenshot here.

### Question

VM Public IP Address: [Enter the public IP shown by terraform output]

---

# Task 4 — Verify the Deployment

## Goal

Confirm through Azure CLI that the virtual machine was created successfully and is currently running.

### Evidence

#### Screenshot 10 — Azure CLI output showing the deployed VM name and `VM running` status

Add your screenshot here.

---

# Task 5 — Destroy the Resources

## Goal

Remove all Azure resources created by Terraform after completing the deployment and verification.

### Evidence

#### Screenshot 11 — Terminal showing successful `terraform destroy` completion

Add your screenshot here.

---

# Submission Instructions

- Complete all tasks in sequence and include all required screenshots specified in Tasks 0–5.
- Do not expose passwords, keys, account IDs, or other sensitive information in screenshots.

---

# Completion Checklist

- Installed Terraform and verified it using `terraform version`
- Installed Azure CLI and verified it using `az version`
- Signed in to Azure using `az login`
- Confirmed the correct Azure subscription
- Installed and enabled the HashiCorp Terraform extension in VS Code
- Created the `terraform-azure-vm` project directory and `main.tf`
- Added the Terraform and AzureRM provider configuration
- Defined the resource group, virtual network, subnet, public IP, and network interface
- Defined the Linux virtual machine with username and password-based authentication
- Added the Terraform output for the VM public IP address
- Completed `terraform init` successfully
- Reviewed the Terraform execution plan using `terraform plan`
- Completed `terraform apply` successfully
- Captured and recorded the VM public IP using `terraform output`
- Verified that the VM is running using Azure CLI
- Completed `terraform destroy` successfully
- Captured all required screenshots
- Checked that no passwords, keys, account IDs, or other sensitive information are visible in the screenshots

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
