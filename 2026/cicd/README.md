# Week 6 : Jenkins ( CI/CD ) Basics and Advanced real world challenge

## Task 1: Create a Jenkins Pipeline Job for CI/CD

### 1. Set Up a Pipeline Job:
  - Create a new Pipeline job in Jenkins.
  - Write a basic Jenkinsfile that automates the build, test, and deployment of a sample application (e.g., a simple web app).
  - Suggested stages: Build, Test, Deploy.

<img width="512" height="768" alt="Screenshot (614)" src="https://github.com/user-attachments/assets/094fb766-a48d-42ff-b226-25764384bf14" />

### 2.Run and Verify the Pipeline
  - Trigger the pipeline and ensure each stage runs successfully.
  - Verify the execution by checking console logs and, if applicable, using docker ps to confirm container status.

<img width="512" height="189" alt="Screenshot (613)" src="https://github.com/user-attachments/assets/6acb1e6e-b2b3-4fdb-a076-679aa94a729d" />

### 3. Document in solution.md:
  - Include your Jenkinsfile code and explain the purpose of each stage.
  - Note any issues you encountered and how you resolved them.
   - Already Done

## Task 3: Configure and Scale Jenkins Agents/Nodes

### 1.Set Up Multiple Agents:
- Configure at least two agents (e.g., one Linux-based and one Windows-based) in Jenkins.
- Use Docker containers or VMs to simulate different environments.

<img width="512" height="382" alt="Screenshot (622)" src="https://github.com/user-attachments/assets/f2f07a26-7e9d-461b-92ef-9f3cecab509e" />

### 2.Label Agents:

- Assign labels (e.g., linux, windows) and modify your Jenkinsfile to run appropriate stages on the correct agent.

<img width="512" height="768" alt="Screenshot (621)" src="https://github.com/user-attachments/assets/113f2d2d-0c0c-4ea0-b0c0-c330895bd83c" />

### 3.Run Parallel Jobs:
- Create jobs that run in parallel across these agents.

<img width="512" height="768" alt="Screenshot (620)" src="https://github.com/user-attachments/assets/58031db9-d784-4fad-b5c0-cc486d4510b9" />
