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
 - **Efficiency:** Since containers don't need a separate OS, you can pack far more services onto a single server than you could with VMs. This  saves massive amounts of money on cloud infrastructure.

 - **Scalability:** If your "Payment Service" gets a sudden spike in traffic, you can spin up ten new containers in seconds. Doing that with VMs would take far too long to meet the demand.

  - **Independence:** Each microservice can be written in a different language (Python, Java, Go) within its own container without worrying about library conflicts on the host server.
### Task 2: Create a Dockerfile for a Sample Project
 #### 1. Select or Create a Sample Application:
 - Write a Dockerfile:
    - Create a Dockerfile that defines how to build an image for your application.
    - Include comments in your Dockerfile explaining each instruction.
<img width="512" height="367" alt="Screenshot (584)" src="https://github.com/user-attachments/assets/11f78974-4435-43b9-aaad-6e99a89c7ba8" />

- Build your image using:
  
docker build -t python-app-full:latest .

<img width="512" height="218" alt="Screenshot (589)" src="https://github.com/user-attachments/assets/b7829e07-456e-4c92-a22e-d40e6e04433e" />

#### 2. Verify Your Build:
-Run your container locally to ensure it works as expected:

docker run -d -p 8080:80 <your-username>/sample-app:latest

-Verify the container is running with:

docker ps
-Check logs using:

docker logs <container_id>

<img width="512" height="224" alt="Screenshot (587)" src="https://github.com/user-attachments/assets/4f0ca0bb-1016-4c5e-863d-566ab5054b0f" />

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

### Task 4: Optimize Your Docker Image with Multi-Stage Builds

**1.Implement a Multi-Stage Docker Build**

- Modify your existing Dockerfile to include multi-stage builds.

- Aim to produce a lightweight, distroless (or minimal) final image.

<img width="512" height="512" alt="Screenshot (588)" src="https://github.com/user-attachments/assets/07c5e164-4f89-46e6-afa6-afa803b8852e" />


**2.Compare Image Sizes:**
- Build your image before and after the multi-stage build modification and compare their sizes using:
  - docker images


<img width="512" height="250" alt="Screenshot (590)" src="https://github.com/user-attachments/assets/987c3f74-1323-445a-a202-55f4ef1d206d" />

**3.Document the Differences:**

- Explain in solution.md the benefits of multi-stage builds and the impact on image size.
  
#### 1. Reduced Image Size

Multi-stage builds allow developers to separate the build environment from the runtime environment.
Tools required only for building the application (such as compilers, package managers, and development dependencies) are kept in the builder stage and are not included in the final image.
This significantly reduces the final image size, making it faster to download, transfer, and deploy.

#### 2. Improved Security

By excluding unnecessary build tools and packages from the final image, the attack surface is reduced.
A smaller runtime image means fewer vulnerabilities and a more secure container environment.

#### 3. Better Performance and Faster Deployments

Smaller images require less storage space and can be pulled faster from container registries.
This improves CI/CD pipeline performance and speeds up deployments in container orchestration platforms like Kubernetes.

#### 4. Cleaner and More Maintainable Dockerfiles

Multi-stage builds allow developers to clearly separate build logic and runtime configuration within the same Dockerfile.
This improves readability, maintainability, and organization of the container build process.

##### Impact on Image Size

In a traditional Docker build, all build tools and dependencies remain in the final image, which can lead to very large images.
With multi-stage builds, only the essential runtime files and dependencies are copied into the final stage.
As a result, image sizes can often be reduced by 50–80% or more, depending on the application and build tools used.

### Task 5: Manage Your Image with Docker Hub

#### 1.Tag Your Image:

- command > docker image tag python-app-mini:latest vaidikjain/python-app-mini:latest

#### 2.Push Your Image to Docker Hub:
- command > docker push vaidikjain/python-app-mini:latest
  
<img width="512" height="685" alt="Screenshot (591)" src="https://github.com/user-attachments/assets/d7eaf5f5-db0f-4c78-9655-2ddf20d7a141" />


<img width="512" height="334" alt="Screenshot (592)" src="https://github.com/user-attachments/assets/81b873ad-a8bb-4e7a-8ad3-df59a65a160b" />

### Task 6: Persist Data with Docker Volumes

#### 1.Create a Docker Volume:

- command > docker volume create flask_volume

<img width="512" height="147" alt="Screenshot (593)" src="https://github.com/user-attachments/assets/19496078-867a-4b7b-b75b-2bd3062af8bc" />


#### 2.Run a Container with the Volume:

- command > docker run -d -v flask_volume:/app/data -p 80:80 python-app-mini:latest

<img width="512" height="201" alt="Screenshot (594)" src="https://github.com/user-attachments/assets/b469b11a-9442-4f9e-8464-324afd6f525b" />

#### 3.Document the Process:

**explain how Docker volumes help with data persistence and why they are useful.**

Docker volumes are used to store data outside of a container’s filesystem. Normally, when a container stops or is deleted, any data stored inside the container is lost. Volumes solve this problem by keeping the data on the host machine, separate from the container lifecycle.

When a Docker volume is mounted to a container directory, any data written to that directory is stored in the volume instead of inside the container. This means:

 - If the container stops or is removed, the data remains safe in the volume.
 - A new container can mount the same volume and continue using the existing data.
 - Data can be shared between multiple containers if they mount the same volume.

### Task 7: Configure Docker Networking

#### 1. Create a Custom Docker Network:

- command > docker network create flask_network
  
<img width="512" height="104" alt="Screenshot (595)" src="https://github.com/user-attachments/assets/506e66a9-3e96-4d73-9e81-a11c8c8a2ae8" />

#### 2. Run Containers on the Same Network:

- Run two containers (e.g., your sample app and a simple database like MySQL) on the same network to demonstrate inter-container communication:
 
    docker run -d --name sample-app --network my_network <your-username>/sample-app:v1.0
    
    docker run -d --name my-db --network my_network -e MYSQL_ROOT_PASSWORD=root mysql:latest

<img width="512" height="393" alt="Screenshot (596)" src="https://github.com/user-attachments/assets/4e9680ba-fb34-496c-9ae5-7b7cce1f0770" />

#### 3. Document the Process:
 **describe how Docker networking enables container communication and its significance in multi-container applications.**

 Docker networking allows Docker containers to communicate with each other, with the host system, and with external networks. Since containers run in isolated environments, networking provides a way to connect them so they can exchange data.

**Key Points**

- Each container gets its own network interface and IP address.

- Containers on the same Docker network can communicate directly.

- Communication can happen using container names, IP addresses, or exposed ports.

 **Common Types of Docker Networks**

- Bridge Network – Default network used for communication between containers on the same host.

- Host Network – The container shares the host machine’s network.

- Overlay Network – Connects containers running on different Docker hosts (used in Docker Swarm).

- None Network – Disables networking for the container.
