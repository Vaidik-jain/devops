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

## Task 2: Manage Terraform State with a Remote Backend

**Scenario:**  
Ensuring state consistency is critical when multiple team members work on infrastructure. Configure a remote backend (e.g., AWS S3 with DynamoDB for locking) to store your Terraform state file.

**Steps:**
1. **Configure a Remote Backend:**  
   - Create a backend configuration in your `main.tf` or a separate backend file to configure a remote backend.

<img width="999" height="424" alt="Screenshot (667)" src="https://github.com/user-attachments/assets/c7ef102b-00a6-4ff0-a152-e8a35c44940b" />

<img width="1047" height="352" alt="Screenshot (668)" src="https://github.com/user-attachments/assets/2ea8d4ca-c8cf-46f1-8fbd-dd81282bfe3c" />

<img width="870" height="435" alt="Screenshot (669)" src="https://github.com/user-attachments/assets/22ae4fff-46ec-474a-af45-dbf34ccf13de" />

2. **Reinitialize Terraform:**  
   - Run `terraform init` to reinitialize your project with the new backend.
  

<img width="1041" height="594" alt="Screenshot (670)" src="https://github.com/user-attachments/assets/28d12d43-0c1d-48a6-80cf-1abb52038419" />

3. **Document in `solution.md`:**  
   - Include the backend configuration details.
   A common production setup uses:

-- S3 bucket → stores the state file remotely
-- DynamoDB table → provides state locking
   - Explain the benefits of using a remote backend and state locking in collaborative environments.

### Benefits of Using Remote Backend
**1. Centralized State Management**
-- State file is stored in a shared remote location (S3).
-- All team members use the same infrastructure state.
-- Avoids mismatch between local state files.
**2. Better Collaboration**
-- Multiple developers can work on the same infrastructure safely.
-- Everyone accesses the latest infrastructure changes.
**3. State File Safety**
-- S3 provides durability and backup.
-- State is not lost if a local machine crashes.
**4. Versioning Support**
-- S3 bucket versioning helps recover older state files if mistakes happen.
**5. Security**
-- Access can be controlled using IAM roles and policies.
-- Sensitive state files remain protected.
-- Benefits of State Locking (DynamoDB)

### Terraform uses DynamoDB to prevent multiple users from modifying infrastructure simultaneously.

#### Why It Is Important

Without locking:

-- Two users may run terraform apply at the same time.
-- State file can become corrupted.
-- Infrastructure may enter an inconsistent state.

With locking:

-- Only one Terraform operation can modify the state at a time.
-- Other users must wait until the lock is released.
   -- Example Scenario

Suppose:

Developer A runs terraform apply
Developer B also runs terraform apply

Without locking:

Both try updating the same state file
Resources may duplicate or fail

With DynamoDB locking:

Terraform locks the state for Developer A
Developer B gets a lock wait/error message
Prevents conflicts and corruption

**Interview Questions:**
- Why is remote state management important in Terraform?

Remote state management allows teams to securely share and maintain a single source of truth for infrastructure state, improving collaboration, consistency, and reliability. 

- How does state locking prevent conflicts during collaborative updates?

State locking prevents multiple users from updating the same Terraform state simultaneously, avoiding conflicts and protecting infrastructure consistency.

## Task 3: Use Variables, Outputs, and Workspaces

**Scenario:**  
Improve the flexibility and reusability of your Terraform configuration by using variables, outputs, and workspaces to manage multiple environments.

**Steps:**
1. **Define Variables and Outputs:**  
   - Create a `variables.tf` file to define configurable parameters (e.g., region, instance type).

   <img width="686" height="391" alt="Screenshot (671)" src="https://github.com/user-attachments/assets/21162708-9cc4-43d2-b300-098d0505bebf" />

   - Create an `outputs.tf` file to output key information (e.g., public IP address of the EC2 instance).

<img width="617" height="360" alt="Screenshot (672)" src="https://github.com/user-attachments/assets/252a942d-1407-4e08-b5f0-b25ee09e4587" />

2. **Implement Workspaces:**  
   - Use `terraform workspace new` to create separate workspaces for different environments (e.g., dev, staging, prod).

   <img width="765" height="328" alt="Screenshot (674)" src="https://github.com/user-attachments/assets/ef94498c-f2f1-4f56-a328-ef35504de8fc" />

3. **Document in `solution.md`:**  
   - Include your `variables.tf`, `outputs.tf`, and a summary of your workspace setup.
     Terraform workspaces were used to create separate environments such as:

      - dev
      - staging
      - prod
- Explain how these features enable dynamic and multi-environment deployments.

   1.Environment Isolation

   Each workspace works independently:

   Dev changes do not affect production

  Separate state files prevent conflicts

   2. Dynamic Configuration

  Using terraform.workspace allows Terraform to automatically select:

  instance types
  tags
  resource names
  environment-specific settings

  based on the active workspace.

   3. Reusable Infrastructure Code

  Same Terraform code can deploy:

  development infrastructure
  testing infrastructure
  production infrastructure

  without duplicating files.

   4. Safer Multi-Environment Management

  Teams can:

  test changes safely in dev/staging
  deploy stable infrastructure to prod
  manage all environments consistently
