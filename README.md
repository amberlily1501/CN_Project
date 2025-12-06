**NU Information Exchange System — README**

**Overview**

This project implements a campus-to-campus communication system using **C++ TCP/UDP socket programming**. Each campus acts as a client, while the **Islamabad campus** serves as the centralized server. The system supports real-time messaging, UDP heartbeats, campus announcements, and department switching.

The project simulates FAST-NU campuses: **Lahore, Karachi, Peshawar, CFD, and Multan**, with each client representing a campus department (Academics / Admissions).


## **Concurrency Handling**

We used **`std::thread`** in both server and client programs to handle multiple tasks simultaneously:

### **Server Concurrency**

* One thread **per TCP client connection**
  → Allows Islamabad Server to handle many campuses at the same time.
* One dedicated thread for **UDP heartbeat listener**
  → Updates campus connectivity in real time.
* One thread for the **Admin Console**
  → Lets the server broadcast announcements and check client status.
* Message routing is synchronized using **`std::mutex`** to protect shared maps like `campus_clients`.

### **Client Concurrency**

Each client uses multiple background threads:

* One thread to **receive TCP messages**
* One thread to **send UDP heartbeats every 5 seconds**
* One thread to **receive UDP announcements from server**

This enables the client to receive messages & announcements even while navigating menus.

---

## **Main Features**

* **TCP Messaging:**
  Campus-to-campus communication with ACK delivery status.
* **UDP Heartbeats:**
  Clients send periodic signals to maintain “online/offline” tracking.
* **UDP Announcements:**
  Server broadcasts admin messages to all campuses.
* **Authentication System:**
  Each campus connects with a unique password.
* **Department Switching:**
  Clients can switch departments anytime.
* **Real-Time Server Logs:**
  Shows connected campuses, message flow, and heartbeat timestamps.

---

## **How to Run**

1. **Run Server**

```
g++ server.cpp -o server
./server
```

2. **Run Client**

```
g++ client.cpp -o client
./client
```

3. Choose campus, department, and interact with the menu.
