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

