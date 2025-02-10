# Docker-container-communication 🌐🐳

## Overview  
This project explores **Docker Networking**, focusing on creating and managing Docker networks that allow containers to communicate. We'll go over basic networking concepts and commands to get you started with **Docker networks**.

## 📚 Documentation & Prerequisites  
Ensure you have the following installed:  
- [Docker](https://www.docker.com/)  
- [Docker Desktop](https://www.docker.com/products/docker-desktop)  
- [Docker Hub Account](https://hub.docker.com/)

## 📌 Networking Concepts & Types of Network Drivers  

### **1️⃣ Types of Docker Network Drivers**  
- **bridge**: Default network type. Containers are isolated and communicate via the bridge network.  
- **host**: Containers share the host system’s network stack, removing isolation.  
- **none**: No networking; containers cannot communicate with each other or the host.  
- **overlay**: Used for communication between containers across different Docker daemons in a Docker Swarm.  
- **ipvlan**: Provides control over IPv4 and IPv6 addressing within a network.  
- **macvlan**: Allows assigning **MAC addresses** to containers, enabling them to appear as physical devices on the network.  

## 🚀 Installation & Setup  

### **1️⃣ Verify Docker Installation**  
Check if Docker is installed and running:  
```sh
docker network ls
```

### **2️⃣ Launch a Container on the Default Network**  
Run a simple Redis container on the default **bridge** network:  
```sh
docker run -itd --name cont_database redis
```

### **3️⃣ Create a Custom Network**  
You can create a custom Docker network with the `--driver` flag. Here’s how to create a **bridge** network:  
```sh
docker network create --driver bridge --subnet 172.20.0.0/16 --ip-range 172.20.240.0/20 net-bridge
```

### **4️⃣ Connect a Container to a Network**  
Use the `docker network connect` command to add an existing container to a network:  
```sh
docker network connect net-bridge cont_database
```

### **5️⃣ Inspect a Docker Network**  
Inspect a network to view detailed information about its containers and settings:  
```sh
docker network inspect net-bridge
```

### **6️⃣ Inspect a Container’s Network Settings**  
Retrieve the IP address of a running container:  
```sh
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' cont_database
```

### **7️⃣ Inspect Network Containers in JSON Format**  
View detailed network settings of containers in JSON format:  
```sh
docker inspect --format='{{json .Containers}}' net-bridge | python -m json.tool
```

### **8️⃣ Executing Commands in a Container**  
Access a running container's shell using `docker container exec`:  
```sh
docker container exec -it <CONTAINER ID> bash
```

### **9️⃣ Installing Network Utilities**  
Install networking tools like `ping` to test network connectivity within containers:  
```sh
apt-get update  
apt-get install iputils-ping
```

### **🔟 Ping from a Container**  
Use the **ping** command to test connectivity between containers:  
```sh
ping <target-container-ip>
```

## 🏆 Conclusion  
You’ve learned the basics of **Docker Networking**, including how to create, manage, and inspect Docker networks and containers. This setup will help ensure seamless communication between your containers and enable scalable, multi-container applications.

---

