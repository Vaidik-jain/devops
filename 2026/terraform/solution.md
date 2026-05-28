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

  
## Task 4: Create and Use Terraform Modules

**Scenario:**  
Enhance reusability by creating a Terraform module for commonly used resources, and integrate it into your main configuration.


**Steps:**
1. **Create a Module:**  
   - In a separate directory (e.g., `modules/ec2_instance`), create a module with `main.tf`, `variables.tf`, and `outputs.tf` for provisioning an EC2 instance.

<img width="783" height="596" alt="Screenshot (675)" src="https://github.com/user-attachments/assets/88c55dc0-1949-43f0-bb7c-d354a3c334ca" />

<img width="942" height="503" alt="Screenshot (676)" src="https://github.com/user-attachments/assets/b5ed3e5d-4c78-497a-94d2-166365d16bbc" />

<img width="844" height="469" alt="Screenshot (677)" src="https://github.com/user-attachments/assets/9cf823f7-a3b1-4a91-92ca-c4a38cde6b5d" />

2. **Reference the Module:**  
   - Update your main configuration to call the module using a `module` block.

  <img width="811" height="610" alt="Screenshot (678)" src="https://github.com/user-attachments/assets/76a36944-3f97-4f98-98a7-565ed0aa1cd6" />

3. **Document in `solution.md`:**  
   - Provide the module code and the main configuration.
   - Explain how modules promote consistency and reduce code duplication.

### How Modules Promote Consistency

- Every environment (Dev, Test, Prod) uses the same infrastructure template.
- Naming conventions, tags, security groups, and configurations remain uniform.
- Changes made inside the module automatically apply wherever the module is used.
- Reduces configuration drift between environments.

### How Modules Reduce Code Duplication

**Without modules:**

- You repeatedly write EC2, VPC, Security Group, or S3 configurations in multiple files/projects.

**With modules:**

- Create reusable templates once.
- Pass different values using variables.
- Reuse the same module multiple times.

**Interview Questions:**
#### 1. What are the advantages of using modules in Terraform?

- Terraform modules offer these key advantages:
- Reusability: Write code once; deploy multiple times.
- Consistency: Enforces standard security and compliance blueprints.
- Simplicity: Hides complex code behind simple inputs.
- Organization: Breaks massive configurations into manageable pieces.
- Speed: Accelerates deployment using pre-built community templates.

#### 2. How would you structure a module for reusable infrastructure components?

modules/

└── compute-instance/

    ├── README.md      # Documentation
    
    ├── main.tf        # Core resource logic
    
    ├── variables.tf   # Configuration inputs
    
    ├── outputs.tf     # Exported data
    
    └── providers.tf   # Provider requirements

## Task 5: Resource Dependencies and Lifecycle Management

**Scenario:**  
Ensure correct resource creation order and safe updates by managing dependencies and customizing resource lifecycles.

**Steps:**
1. **Define Resource Dependencies:**
   Terraform automatically detects dependencies when one resource references another.
   In some cases, you must explicitly define dependencies using the depends_on meta-argument.
   
   - Use the `depends_on` meta-argument in your configuration to specify dependencies explicitly.

     <img width="710" height="380" alt="Screenshot (679)" src="https://github.com/user-attachments/assets/b5d1bae5-aa5d-408a-8a1d-5d25ff322260" />

### Why Use depends_on?
- Ensures Terraform creates the security group before launching the EC2 instance.
- Prevents resource creation failures caused by missing dependencies.
- Useful when dependencies are not automatically detected.

2. **Configure Resource Lifecycles:**

Terraform lifecycle rules help manage how infrastructure changes are applied.

Example: Using create_before_destroy

resource "aws_instance" "app_server" {

  ami           = "ami-0abcdef1234567890"
  
  instance_type = "t2.micro"
  

  lifecycle {
  
    create_before_destroy = true
    
  }
  
}

Purpose of create_before_destroy

Normally, Terraform:

- Destroys the old resource
- Creates the new resource

With create_before_destroy = true:

- Terraform creates the new resource first
- Then destroys the old resource

This minimizes downtime during updates.

3. **Document in `solution.md`:**  
   - Include examples of resource dependencies and lifecycle configurations in your code.
  
   <img width="999" height="603" alt="Screenshot (680)" src="https://github.com/user-attachments/assets/7282a45d-84aa-4182-85a6-4ecdd67fa8bf" />
   

   - Explain how these settings prevent downtime during updates.

1. Resource Dependencies

- Ensure infrastructure components are created in the correct order.
- Avoid failures caused by missing or partially configured resources.
  
2. Lifecycle Configuration
   
- create_before_destroy keeps the old resource running until the replacement is fully available.
- Reduces service interruptions during deployments and updates.
- Useful in production systems where availability is important.

**Interview Questions:**
- How does Terraform handle resource dependencies?
  
   - Terraform automatically builds a dependency graph using resource references.
   - If dependencies are not directly referenced, depends_on can be used to define them explicitly.
   
- Can you explain the purpose of the `create_before_destroy` lifecycle argument?
   
  It ensures a new resource is created before the old resource is destroyed, helping prevent downtime during infrastructure updates.

## Task 6: Infrastructure Drift Detection and Change Management

**Scenario:**  
In production, changes might occur outside of Terraform. Use Terraform commands to detect infrastructure drift and manage changes.

**Steps:**
1. **Detect Drift:**  
   - Run `terraform plan` to identify differences between your configuration and the actual infrastructure.
   

## 1. Detect Drift

Infrastructure drift occurs when the actual infrastructure differs from the Terraform configuration or state file.

Terraform can detect drift using the following command:

```bash
terraform plan
```

This command compares:

* Terraform configuration files
* Terraform state file
* Actual infrastructure in the cloud provider

and shows any differences.

---

## Example: Drift Detection

Suppose an EC2 instance type was manually changed in AWS from `t2.micro` to `t2.small`.

### Terraform Configuration

```hcl id="0a5j3r"
resource "aws_instance" "web_server" {
  ami           = "ami-0abcdef1234567890"
  instance_type = "t2.micro"
}
```

### Drift Detection Output

```bash
terraform plan
```

Example output:

```bash
~ instance_type = "t2.small" -> "t2.micro"
```

This indicates the infrastructure has drifted from the Terraform configuration.

---

# 2. Reconcile Changes

When drift is detected, there are two common approaches:

## Approach 1: Reapply Terraform Configuration

If the manual changes are not intended:

```bash
terraform apply
```

Terraform updates the infrastructure to match the configuration files.

### Use Case

* Unauthorized manual changes
* Restoring infrastructure consistency
* Enforcing Infrastructure as Code practices

---

## Approach 2: Update Terraform Configuration or State

If the manual changes are intentional:

### Update Configuration

Modify the Terraform code to match the real infrastructure.

Example:

```hcl id="dkx1sh"
resource "aws_instance" "web_server" {
  ami           = "ami-0abcdef1234567890"
  instance_type = "t2.small"
}
```

Then run:

```bash
terraform plan
terraform apply
```

---

## Refresh Terraform State

You can also refresh Terraform state information:

```bash
terraform refresh
```

or

```bash
terraform plan -refresh-only
```

This updates the state file with the latest infrastructure information.

---

# 3. Importance of Change Management in Infrastructure as Code

Proper change management is critical in Terraform environments because:

* Prevents configuration drift
* Maintains consistency across environments
* Reduces unexpected failures in production
* Ensures infrastructure changes are version-controlled
* Improves auditing and rollback capabilities

---

# Best Practices to Prevent Drift

* Avoid manual infrastructure changes in cloud consoles
* Use CI/CD pipelines for deployments
* Store Terraform state remotely
* Enable code reviews for infrastructure changes
* Run `terraform plan` before every deployment
* Use monitoring and policy enforcement tools

---

# Interview Questions

## What is infrastructure drift, and why is it a concern in production environments?

Infrastructure drift happens when the actual infrastructure differs from the Terraform configuration or state file due to manual changes or external updates.

It is a concern because it can:

* Cause deployment failures
* Create inconsistent environments
* Introduce security or compliance risks
* Make troubleshooting difficult

---

## How would you resolve discrepancies between your Terraform configuration and actual infrastructure?

1. Run `terraform plan` to identify differences.
2. Determine whether the infrastructure changes are intentional.
3. If unintentional:

   * Run `terraform apply` to restore the desired state.
4. If intentional:

   * Update Terraform configuration and state to reflect the changes.
5. Re-run `terraform plan` to confirm consistency.


## Task 7: (Optional) Dynamic Pipeline Parameterization for Terraform

**Scenario:**  
Enhance your Terraform configurations by using dynamic input parameters and conditional logic to deploy resources differently based on environment-specific values.

**Steps:**
1. **Enhance Variables with Conditionals:**  
   - Update your `variables.tf` to include default values and conditional expressions for environment-specific configurations.

   <img width="1028" height="447" alt="Screenshot (681)" src="https://github.com/user-attachments/assets/c4bc0d9e-82af-4d17-8e8e-4e1e73b3f6e1" />

2. **Apply Conditional Logic:**  
   - Use conditional expressions in your resource definitions to adjust attributes based on variable values.

   <img width="545" height="83" alt="Screenshot (682)" src="https://github.com/user-attachments/assets/e2b32c46-fd79-4a66-a69a-023ea76111fe" />

3. **Document in `solution.md`:**  
   - Explain how dynamic parameterization improves flexibility.
     
    **Dynamic parameterization helps by:**

- Reusing the same Terraform code across environments
- Reducing code duplication
- Simplifying deployment management
- Making infrastructure scalable and maintainable
- Supporting automated CI/CD pipelines

Instead of maintaining separate files for dev, staging, and production, one configuration can dynamically adapt using variables and conditionals.

**Interview Questions**

1.How do conditional expressions in Terraform improve configuration flexibility?

Conditional expressions allow Terraform resources to dynamically change values based on variables or environment settings.

This helps:

- Reuse configurations
- Reduce duplicate code
- Support multiple deployment environments
- Automate infrastructure decisions

2.Provide an example scenario where dynamic parameters are critical in a deployment pipeline.

In a CI/CD pipeline:

- Development environments may use low-cost resources like t2.micro
- Production environments may require larger instances like t2.large

Using conditional expressions, the same Terraform configuration can automatically provision different infrastructure depending on the deployment stage, improving automation and consistency.

