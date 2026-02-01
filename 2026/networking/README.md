# ⭐Week 1: Networking Challenge <br>

## Tasks
### A. **Understand OSI & TCP/IP Models**
   
  #### ⭐ OSI Model (7 Layers)
  
   -The OSI (Open Systems Interconnection) Model is a set of rules that explains how different computer systems communicate over a          network.

   
   ##### 📌 The 7 Layers of OSI
   Let's understand the working of each layers of OSI Model .
     Suppose two friends X and Y , X wants to send a message to Y
     The Journey from X to Y
     
Layer 7. Application: X types "Hello!" into an app.

Layer 6. Presentation: The app encrypts the message so only Y can read it.

Layer 5. Session: A connection is opened to ensure Y is "online" and ready.

Layer 4. Transport: The message is chopped into numbered pieces so none are lost.

Layer 3. Network: The "GPS" adds Y's IP address to find the best path across the internet.

Layer 2. Data Link: The "Local Driver" uses Y's MAC address to find the specific house.

Layer 1. Physical: The data travels as electrical pulses over a wire.

   <img width="512" height="512" alt="osi model" src="https://github.com/user-attachments/assets/16f41c01-1780-4994-b732-f07245868a7f" />

#### ⭐ TCP/IP Model

The TCP/IP Model is a 4-layer networking model used in real-world networks and the foundation of the Internet.
It focuses on practical communication between systems and is more widely implemented than the OSI model.

 ##### 📌 The 7 Layers of TCP/IP

  Layer 4: Application - X types the message "Hello!" and the app immediately handles the translation and encryption. In TCP/IP, this one layer does the job of OSI layers 5, 6, and 7.

Layer 3: Transport - The "Quality Control" stage. X’s message is broken into segments. It ensures Y receives them in the right order and asks for a "receipt" to confirm delivery.

Layer 2: Internet - The "Global GPS." This layer stamps the data with Y’s IP address. It doesn't care how it gets there, just that it finds the right network across the globe.

Layer 1: Network Access - The "Physical Delivery." This combines the local driver (MAC address) and the actual road (cables/Wi-Fi). It’s the final step that pushes the bits out of X’s device and onto the wire.

![tcp-layers](https://github.com/user-attachments/assets/9f29c76b-d51c-474e-8178-6e1077d41827)
## <br>
### B. **Protocols and Ports for DevOps**
  #### 🔹 Protocols 
 
A protocol is a set of rules that define how data is formatted, transmitted, and received between devices over a network.

📌 Without protocols, computers wouldn’t understand how to communicate.

 #### 🔹 Prots

 A port is a logical endpoint that identifies which service or application should receive the incoming data.
 Port Range

- 0–65535 total ports

- Well-known ports: 0–1023 (standard services)

- Registered ports: 1024–49151

- Dynamic/Private ports: 49152–65535

#### 🔹 Role of Ports & Protocols in DevOps

##### 1. Server Management & SSH

  DevOps engineers access servers using:

  SSH → TCP → Port 22

  If port 22 is blocked → ❌ no server access.

##### 2. Application Deployment

  When you deploy apps:

  Backend app might run on 8080

  Frontend on 80/443

##### 3. Containers & Kubernetes

  Containers expose ports (EXPOSE 3000)

  Kubernetes maps:

  Service Port → Target Port → Pod Port

  If ports don’t match → 🚫 app won’t be reachable.

##### 4. CI/CD Pipelines

  CI tools communicate using ports:

  Jenkins → 8080

  GitHub Webhooks → 443

  Artifact repo (Nexus) → 8081

  Ports must be open for pipeline to work

#### 🔹 Some Important Ports to Remember

<img width="512" height="512" alt="Imp ports" src="https://github.com/user-attachments/assets/1084a3a1-6819-43fd-ab3c-9ca5f04d0cad" />

## <br>
### C. **Hands-On with Networking Commands**

1.**ping**

ping is used to check connectivity between your system and another system (server, website, IP address) over a network.


<img width="512" height="247" alt="Screenshot from 2026-01-31 17-06-45" src="https://github.com/user-attachments/assets/44b3c500-a54b-4509-8879-a5b5e66eb3b9" />

2.**Netstat**

netstat (network statistics) is a command used to display network connections, open ports, routing tables, and listening services on a system.

<img width="512" height="441" alt="Screenshot from 2026-01-31 12-16-48" src="https://github.com/user-attachments/assets/b2ed948f-e8d0-4455-a4d8-af832712b65a" />

3.**Ifconfig**

ifconfig (interface configuration) is used to view and configure network interfaces on a system.
It shows IP address, MAC address, and interface status (UP/DOWN).

<img width="512" height="453" alt="Screenshot from 2026-01-31 12-20-10" src="https://github.com/user-attachments/assets/2e857dc6-1880-4295-b745-9a571afcb4e2" />

4.**Traceroute**

traceroute is used to trace the path (route) that packets take from your system to a destination host.

👉 It shows each hop (router) between source and destination and how long each hop takes.


<img width="512" height="246" alt="Screenshot from 2026-01-31 17-16-59" src="https://github.com/user-attachments/assets/b95f2a80-0ee6-49b4-b6a2-a3c4d9287967" />

5.**mtr**

mtr (My Traceroute) is a combination of ping + traceroute.

👉 It continuously traces the route to a destination and shows packet loss + latency for every hop in real time.

6.**nslookup**

nslookup (Name Server Lookup) is used to query DNS servers and find information about a domain name.

It translates domain names ↔ IP addresses.

<img width="512" height="213" alt="Screenshot from 2026-01-31 17-30-17" src="https://github.com/user-attachments/assets/53814984-e5b1-440d-978a-59f9463a6558" />

7.**telnet**

telnet is a network protocol & command-line tool used to test connectivity to a specific IP and port.
In DevOps today, it’s mainly used to check if a port is open and reachable.

8.**whois**

whois is a command used to get ownership and registration details of a domain name or IP address.
It tells you who owns a domain, when it was registered, and which registrar/DNS provider is used.

9.**curl**

curl (Client URL) is a command-line tool used to send requests to URLs and interact with web servers & APIs.


<img width="512" height="467" alt="Screenshot from 2026-02-01 14-56-56" src="https://github.com/user-attachments/assets/18206987-c4b7-44a7-8acc-32ceccd8f6a7" />

10.**wget**

wget is a command-line tool used to download files from the internet using HTTP, HTTPS, or FTP.

11.**nmap**

nmap (Network Mapper) is a tool used to scan networks, discover hosts, and identify open ports & services.

