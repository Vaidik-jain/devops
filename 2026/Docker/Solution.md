# 🐳Week 5: Docker Basics & Advanced Challenge

## Tasks

### Task 1: Introduction and Conceptual Understanding

#### 1. Write an Introduction:
**A brief explanation of Docker’s purpose in modern DevOps.**

- In modern operating systems, the primary purpose of Docker is to provide a standardized, portable, and isolated environment (containers) for applications to run consistently across different computing environments, from a developer's laptop to production cloud servers.
- It helps eliminate the "but it works on my machine" problem by packaging an application with all its dependencies into a single unit.
- Key aspects of Docker's purpose include:
  - **Portability:** Docker containers encapsulate an application, its runtime, system tools, libraries, and configuration into a single, lightweight image that can run on any system with the Docker Engine installed, regardless of the underlying infrastructure (cloud or on-premises).
  - **Consistency:** By providing an identical runtime environment from development through testing and into production, Docker ensures that applications behave the same way everywhere, which speeds up the development lifecycle and reduces bugs.
  - **Isolation and Security:** Containers run as isolated processes on the host OS kernel but are separate from other containers and the host system, which enhances security and prevents conflicts between applications or dependencies (e.g., two apps requiring different versions of the same library).
  - **Resource Efficiency:** Unlike traditional virtual machines (VMs) that require a full, separate operating system for each instance, containers share the host OS kernel. This makes them much lighter (measured in megabytes vs. gigabytes for VMs) and faster to start, maximizing the use of available hardware resources
  - **Rapid Deployment and Scalability:** The lightweight nature of containers allows for fast startup times (seconds instead of minutes) and easy scaling. In conjunction with orchestration tools like Kubernetes or Docker Swarm, many instances of an application can be quickly deployed and managed to handle varying demand.

   **Compare Virtualization vs. Containerization and explain why containerization is the preferred approach for microservices and CI/CD pipelines.**

  1️⃣ Virtualization

    Virtualization abstracts the hardware. Each Virtual Machine (VM) includes a full copy of an operating system, the application, and all necessary binaries and libraries.

   - Hypervisor: The software (like VMware or Hyper-V) that creates and runs VMs.

   - Size: Large (gigabytes) because each VM carries its own Guest OS.

   - Startup: Slow (minutes) because the entire OS has to boot up.
     
  2️⃣ Containerization

  Containerization abstracts the app layer. Containers share the host machine’s OS kernel and isolate the application processes from the rest of the system.

    - Container Engine: The software (like Docker) that manages containers.

    - Size: Small (megabytes) because they only contain the app and its dependencies.

    - Startup: Instant (seconds) because the OS is already running.
    - 
  **Why Containers Win for Microservices**
    - **Efficiency:** Since containers don't need a separate OS, you can pack far more services onto a single server than you could with VMs. This saves massive amounts of money on cloud infrastructure.

    - **Scalability:** If your "Payment Service" gets a sudden spike in traffic, you can spin up ten new containers in seconds. Doing that with VMs would take far too long to meet the demand.

    - **Independence:** Each microservice can be written in a different language (Python, Java, Go) within its own container without worrying about library conflicts on the host server.
 ### Task 2: Create a Dockerfile for a Sample Project
 #### 1. Select or Create a Sample Application:
      - Write a Dockerfile:
        - Create a Dockerfile that defines how to build an image for your application.
        - Include comments in your Dockerfile explaining each instruction.
 <img width="512" height="454" alt="Screenshot (580)" src="https://github.com/user-attachments/assets/bcced71b-031d-4742-a9bc-5a22baced464" />
- Build your image using:
  
docker build -t java-quotes:latest .

<img width="512" height="110" alt="Screenshot (578)" src="https://github.com/user-attachments/assets/cbca6bb0-49e3-482d-801f-bfb104b8c7f2" />

#### 2. Verify Your Build:
-Run your container locally to ensure it works as expected:

docker run -d -p 8080:80 <your-username>/sample-app:latest

-Verify the container is running with:

docker ps
-Check logs using:

docker logs <container_id>

<img width="512" height="212" alt="Screenshot (579)" src="https://github.com/user-attachments/assets/1efb9712-0634-495b-864c-958ad5d5ff5b" />

### Task 3: Explore Docker Terminologies and Components

**1️⃣ Image**

A Docker Image is a lightweight, read-only template used to create containers.
It contains application code, runtime, libraries, dependencies, and configuration files.
Images are built using a Dockerfile.

**2️⃣ Container**

A Container is a runnable instance of a Docker image.
It is isolated, lightweight, and shares the host OS kernel.
Containers can be started, stopped, deleted, and scaled easily.

**3️⃣ Dockerfile**

A Dockerfile is a text file containing instructions to build a Docker image.
It defines:

- Base image

- Application code

- Dependencies

- Commands to run
**4️⃣ Volume**

A Volume is used to persist data generated by containers.

Since containers are ephemeral (temporary), volumes store data outside the container lifecycle.

Use cases:

- Database storage

- Log storage

- Shared data between containers

**5️⃣ Network**

Docker Network allows containers to communicate with each other and with external systems.

Types:

- Bridge (default)

- Host

- Overlay (used in clustering)

#### 🔹 Main Docker Components

**1️⃣ Docker Engine**

Docker Engine

Docker Engine is the core runtime responsible for:

- Building images

- Running containers

- Managing networks and volumes

It consists of:

- Docker Daemon (dockerd)

- REST API

- Docker CLI

**2️⃣ Docker CLI**

The command-line tool used to interact with Docker.

- docker build

- docker run

- docker ps

- docker images

**3️⃣ Docker Hub**

Docker Hub is a cloud-based registry where Docker images are stored and shared.

Features:

- Public and private repositories

- Official images

- Image versioning

**4️⃣ Docker Registry**

A storage and distribution system for Docker images.

Docker Hub is the default public registry, but private registries can also be set up.

**🔹 How Docker Components Interact**

- Developer writes a Dockerfile.

- Docker CLI sends build command to Docker Engine.

- Docker Engine builds an Image.

- The image can be pushed to Docker Hub (Registry).

- Docker Engine pulls image from Hub and runs it as a Container.

- Containers use Volumes for persistent storage and Networks for communication.
