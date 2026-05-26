# Week 8: Terraform (Infrastructure as Code) Challenge

## Task 1: Install Terraform, Initialize, and Provision a Basic Resource

**Scenario:**  
Begin by installing Terraform, initializing a project, and provisioning a basic resource (e.g., an AWS EC2 instance) to validate your setup.

**Steps:**
1. **Install Terraform:**  
   - Download and install Terraform on your local machine.
   - validate using terraorm -version :white_check_mark:
2. **Initialize a Terraform Project:**  
   - Create a new directory for your Terraform project.
   - Run `terraform init` to initialize the project.

<img width="1073" height="504" alt="Screenshot (662)" src="https://github.com/user-attachments/assets/426b5df6-878e-4e9b-ab1d-6e59b8b69bf1" />

3. **Provision a Basic Resource:**  
   - Create a configuration file (e.g., `main.tf`) to provision an AWS EC2 instance (or a similar resource for your cloud provider).
     
<img width="1366" height="538" alt="Screenshot (663)" src="https://github.com/user-attachments/assets/3c3f5d64-af96-4e1e-8bbc-3fd25f121671" />

   - Run `terraform apply` and confirm the changes.

<img width="709" height="297" alt="Screenshot (664)" src="https://github.com/user-attachments/assets/5d779146-f56b-45f8-96b8-4ebaccfe0e11" />


<img width="709" height="107" alt="Screenshot (666)" src="https://github.com/user-attachments/assets/61d075da-91fc-4622-befd-02d1a3b0706a" />

## Interview Questions

### 1.How does Terraform manage resource creation and state?
Terraform uses configuration files (.tf) to define infrastructure resources. When terraform apply is executed, Terraform compares the desired configuration with the current infrastructure state and creates, updates, or deletes resources accordingly. Terraform stores the infrastructure details in a terraform.tfstate file, known as the state file, which helps track existing resources and manage future changes efficiently.
### 2.What is the significance of the terraform init command in a new project?
The terraform init command initializes a Terraform project. It downloads the required provider plugins (such as AWS provider), sets up the backend configuration, and prepares the working directory so Terraform commands like plan and apply can run successfully. It is the first command that should be executed in any new Terraform project.

