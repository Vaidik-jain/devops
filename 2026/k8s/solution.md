# Week 7 : Kubernetes Basics & Advanced Challenges

## Task 1: Understand Kubernetes Architecture & Deploy a Sample Pod

**Scenario:**  
Familiarize yourself with Kubernetes’ control plane and worker node components, then deploy a simple Pod manually.

**Steps:**
1. **Study Kubernetes Architecture:**  
   - Review the roles of control plane components (API Server, Scheduler, Controller Manager, etcd, Cloud Controller) and worker node components (Kubelet, Container Runtime, Kube Proxy).
 
 To understand Kubernetes (K8s) architecture simply, think of it like a large shipping company.
 
 There is a Management Office (the Control Plane) that takes orders and makes decisions, and there are Ships/Warehouses (Worker Nodes) that do the actual heavy lifting of carrying the cargo (your applications).

 A Kubernetes cluster is split into two main parts: the Control Plane and the Worker Nodes.

 1. The Control Plane (The "Brain" or Management Office)
The Control Plane is responsible for managing the cluster, making global decisions (like scheduling), and detecting/responding to cluster events.

**It consists of four main components:**

- API Server (kube-apiserver): This is the "Front Desk" of Kubernetes. Everything (users, administrators, and the worker nodes) communicates with the cluster through the API server.

- etcd: This is the "Filing Cabinet" or memory of the cluster. It is a highly reliable database that stores all the configuration data and the exact current state of the cluster. If the cluster goes down, etcd is what helps it remember exactly how things were.

- Scheduler (kube-scheduler): This is the "Dispatcher". When you ask Kubernetes to run a new application, the scheduler looks for a worker node that has enough available resources (CPU, memory) to handle the job and assigns it there.

- Controller Manager (kube-controller-manager): This is the "Quality Assurance Supervisor". It constantly watches the state of the cluster. If you asked for 3 copies of your application to run, and one crashes, the controller manager notices the mismatch and asks the scheduler to spin up a new one to replace it.

2. The Worker Nodes (The "Muscle" or Workhorses)
Worker nodes are the actual machines (virtual or physical) that run your applications. A cluster usually has multiple worker nodes.

**Each worker node runs three main components:**

- Kubelet: This is the "Ship Captain" or the main agent on the node. It listens to instructions from the API Server and makes sure that the requested containers are running healthily on its specific node.

- Kube-Proxy: This is the "Traffic Cop". It manages network rules on the node, ensuring that network traffic is routed correctly to the right applications, both from inside and outside the cluster.

- Container Runtime: This is the "Engine" that actually runs the containers (for example, containerd, CRI-O, or Docker). Kubernetes doesn't run the containers itself; it tells the container runtime to do it.

3. Pods (The Cargo)
Inside the worker nodes, your applications run inside Pods. A Pod is the smallest, most basic deployable unit in Kubernetes. You can think of a Pod as a "shipping container" that holds one or more tightly coupled application containers. When Kubernetes scales an application, it doesn't add more containers to an existing Pod; it adds more Pods.

**How it all works together:**

- You (the developer) send a blueprint to the API Server saying: "I want 3 copies of my web application running."

- The API Server saves this request in etcd.

- The Controller Manager notices that 0 copies are currently running, but you want 3. It tells the API Server about this gap.

- The Scheduler sees that 3 new Pods need a home. It looks at the Worker Nodes, checks their available resources, and assigns the Pods to specific nodes.

- The Kubelet on those specific nodes receives the assignment from the API Server and tells its Container Runtime to start up the Pods.

- Kube-Proxy updates the network rules so users can actually access the new web applications.
- 
2. **Deploy a Sample Pod:**  
   - Create a YAML file (e.g., `pod.yaml`) to deploy a simple Pod (such as an NGINX container).
  
  <img width="351" height="179" alt="Screenshot (641)" src="https://github.com/user-attachments/assets/870b589e-4dd1-4b96-bb4f-0c17c419ba31" />

   - Apply the YAML using:
     ```bash
     kubectl apply -f pod.yaml
     ```
  <img width="712" height="320" alt="Screenshot (640)" src="https://github.com/user-attachments/assets/e5239d85-3454-48a8-a4ad-ab3562f53d5a" />

## Task 2: Deploy and Manage Core Kubernetes Objects

**Scenario:**  
Deploy core Kubernetes objects for the SpringBoot BankApp application, including Deployments, ReplicaSets, StatefulSets, DaemonSets, and use Namespaces to isolate resources.

**Steps:**
1. **Create a Namespace:**  
  - Write a YAML file to create a Namespace for the SpringBoot BankApp application.
   <img width="409" height="149" alt="Screenshot (642)" src="https://github.com/user-attachments/assets/94c3f8f5-9891-4a7c-a5cb-212f47c18d6a" />
   - Apply the YAML:
     ```bash
     kubectl apply -f namespace.yaml
     ```
   <img width="512" height="190" alt="image" src="https://github.com/user-attachments/assets/9adac0b9-3711-4153-84cf-75eb4c374265" />


1. **Deploy a Deployment:**  
- Create a YAML file for a Deployment (within your Namespace) that manages a set of Pods running a component of SpringBoot BankApp.

   <img width="1092" height="573" alt="Screenshot (645)" src="https://github.com/user-attachments/assets/5f5ea1d9-f068-436b-854d-aeb749ff4ddb" />

   - Verify that a ReplicaSet is created automatically.
  
   <img width="512" height="81" alt="Screenshot (646)" src="https://github.com/user-attachments/assets/f1520da6-88f0-4948-88d2-1a5235129ce9" />

2. **Deploy a StatefulSet:**  
   - Write a YAML file for a StatefulSet (for example, for a database component) and apply it.

   <img width="689" height="631" alt="Screenshot (647)" src="https://github.com/user-attachments/assets/1bae7274-b029-4448-a441-efe29035f267" />

3. **Deploy a DaemonSet:**  
   - Create a YAML file for a DaemonSet to run a Pod on every node.
4. **Document in `solution.md`:**  
   - Include the YAML files for the Namespace, Deployment, StatefulSet, and DaemonSet.

### 🔹 Namespace
- Used to isolate resources
- Helps in managing environments (dev, staging, prod)
- Avoids naming conflicts

#### 👉 Example: bankapp-namespace

### 🔹 Deployment
- Manages stateless applications
- Ensures desired number of Pods
- Supports:
  - scaling
  - rolling updates
  - self-healing

#### 👉 Used for:

 - Spring Boot backend
 - Frontend apps
   
### 🔹 ReplicaSet
- Ensures a fixed number of Pods are running
- Automatically created by Deployment

#### 👉 Rarely used directly

### 🔹 StatefulSet
- Used for stateful applications
- Provides:
  - stable pod names (mysql-0)
  - persistent storage
  - ordered deployment

#### 👉 Used for:

  - Databases (MySQL, MongoDB)
### 🔹 DaemonSet
- Runs one pod per node
- Automatically schedules on all nodes

#### 👉 Used for:

- logging agents
- monitoring tools
- node-level services
   - Explain the differences between these objects and when to use each.
 
⚖️ Key Differences
Feature	    |Deployment |	StatefulSet |	DaemonSet

Use case	    |Stateless apps |	Stateful apps |	Node-level pods

Pod identity |Random	| Stable | One per node

Storage	    |Not required |	Required	| Not required

Scaling	    |Yes	| Limited |	Auto (per node)

## Task 3: Networking & Exposure – Create Services, Ingress, and Network Policies

**Scenario:**  
Expose your SpringBoot BankApp application to internal and external traffic by creating Services and configuring an Ingress, while using Network Policies to secure communication.

**Steps:**
1. **Create a Service:**  
   - Write a YAML file for a Service of type ClusterIP.
   
  <img width="825" height="369" alt="Screenshot (648)" src="https://github.com/user-attachments/assets/7bb3f43e-f8cf-4e35-90e6-bde7c5b2ff7a" />

   - Modify the Service type to NodePort or LoadBalancer and apply the YAML.

<img width="774" height="561" alt="Screenshot (649)" src="https://github.com/user-attachments/assets/98b9af56-49f5-4d13-a3eb-939528479832" />


2. **Configure an Ingress:**  
   - Create an Ingress resource to route external traffic to your application.
   
   <img width="999" height="489" alt="Screenshot (650)" src="https://github.com/user-attachments/assets/c3ab1927-de78-45bb-87c7-42af46da72f0" />

3. **Implement a Network Policy:**  
   - Write a YAML file for a Network Policy that restricts traffic to your application Pods.

  <img width="1366" height="451" alt="Screenshot (651)" src="https://github.com/user-attachments/assets/434c77de-c127-41c4-b233-2bdbc095055f" />


     
4. **Document in `solution.md`:**  
   - Include the YAML files for your Service, Ingress, and Network Policy.
### 🔹 Ingress
- Acts as a smart router
- Routes HTTP/HTTPS traffic to services
#### Supports:
- Host-based routing (bankapp.local)
- Path-based routing (/api, /login)
- Requires an Ingress Controller (like NGINX)
### 🔹 Network Policy
Works like a firewall inside Kubernetes
#### Controls:
Which pods can talk to which pods
- Improves security
- Default behavior:
- If policy exists → deny all unless allowed

## Task 4: Storage Management – Use Persistent Volumes and Claims

**Scenario:**  
Deploy a component of the SpringBoot BankApp application that requires persistent storage by creating Persistent Volumes (PV), Persistent Volume Claims (PVC), and a StorageClass for dynamic provisioning.

**Steps:**
1. **Create a Persistent Volume and Claim:**  
   - Write YAML files for a static PV and a corresponding PVC.
     
     <img width="880" height="267" alt="Screenshot (652)" src="https://github.com/user-attachments/assets/f7271ef3-769a-445e-9701-52d67e42ee2f" />

2. **Deploy an Application Using the PVC:**  
   - Modify a Pod or Deployment YAML to mount the PVC.
   
     <img width="436" height="208" alt="Screenshot (653)" src="https://github.com/user-attachments/assets/cce42325-ea9f-41c6-b3a1-6610c025d719" />

3. **Document in `solution.md`:**  
   - Include your PV, PVC, and application YAML.
   - Explain how StorageClasses facilitate dynamic storage provisioning.
   
   “StorageClasses enable dynamic provisioning by allowing Kubernetes to automatically create PersistentVolumes when a PersistentVolumeClaim is requested, using a defined provisioner and configuration. This removes the need for manual storage management and ensures scalable, on-demand resource allocation.”

## Task 5: Configuration & Secrets Management with ConfigMaps and Secrets

**Scenario:**  
Deploy a component of the SpringBoot BankApp application that consumes external configuration and sensitive data using ConfigMaps and Secrets.

**Steps:**
1. **Create a ConfigMap:**  
- Write a YAML file for a ConfigMap containing configuration data.
     
   <img width="1260" height="177" alt="Screenshot (655)" src="https://github.com/user-attachments/assets/6a022e84-0b80-4fb5-a81a-a70bd90ed4bf" />

2. **Create a Secret:**  
- Write a YAML file for a Secret containing sensitive information.
  
   <img width="858" height="190" alt="Screenshot (654)" src="https://github.com/user-attachments/assets/bae3948f-111f-4a22-aa10-648f59669cf2" />.

## Task 6: Autoscaling & Resource Management

**Scenario:**  
Implement autoscaling for a component of the SpringBoot BankApp application using the Horizontal Pod Autoscaler (HPA). Optionally, explore Vertical Pod Autoscaling (VPA) and ensure the Metrics Server is running.

**Steps:**
1. **Deploy an Application with Resource Requests:**  
   - Deploy an application with defined resource requests and limits.
    resources:

     ```bash
     requests:
            memory: "32Mi"
            cpu: "50m"
          limits:
            memory: "64Mi"
            cpu: "100m"
     ```
          
2. **Create an HPA Resource:**  
   - Write a YAML file for an HPA that scales the number of replicas based on CPU or memory usage.
   
   <img width="512" height="297" alt="Screenshot (656)" src="https://github.com/user-attachments/assets/308a81c6-5d25-4088-9207-d58f13a2836d" />

3. **(Optional) Implement VPA & Metrics Server:**  
   - Optionally, deploy a VPA and verify that the Metrics Server is running.
4. **Document in `solution.md`:**  
   - Include the YAML files and explain how HPA (and optionally VPA) work.
   - Discuss the benefits of autoscaling in production.

  **“Autoscaling improves application reliability, performance, and cost efficiency by dynamically adjusting resources based on demand. It ensures high availability during traffic spikes while minimizing resource usage during low traffic periods, making systems both resilient and cost-effective.”**
  

