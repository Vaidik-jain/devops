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
