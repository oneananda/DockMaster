# 🌐 **6. Docker Networking**

Docker networking enables containers to communicate with each other, with the host system, and with external networks. By understanding Docker’s networking capabilities, you can build isolated environments, connect services, and manage container communication effectively.

---

## **1. Default Networks**

Docker provides several pre-configured network types, each suited for specific use cases:

### **1.1 Bridge Network (Default)**
- Containers in the same bridge network can communicate with each other via IP or container name.
- The default network mode for standalone containers.
  
**Example:**
```bash
docker run -d --name container1 nginx
docker run -d --name container2 nginx
```
Both `container1` and `container2` can communicate because they are on the default bridge network.

---

### **1.2 Host Network**
- The container shares the host's network stack.
- Removes network isolation, allowing the container to use the host's IP address directly.

**Use Case:** Low network latency or access to host-specific resources.

**Example:**
```bash
docker run --network host nginx
```

---

### **1.3 None Network**
- Disables networking for the container.
- Useful for security or testing scenarios where no network access is required.

**Example:**
```bash
docker run --network none nginx
```

---

## **2. Custom Networks**

Custom networks give you more control over container communication and isolation.

### **2.1 Create a Custom Network**
To create an isolated network:
```bash
docker network create my-network
```

**Features:**
- Containers in a custom network can communicate using their container names.
- By default, custom networks use the **bridge driver**.

---

### **2.2 Run Containers on a Custom Network**
```bash
docker run -d --name app1 --network my-network nginx
docker run -d --name app2 --network my-network nginx
```

- Containers `app1` and `app2` can communicate because they are on the same custom network.

**Test Communication:**
1. Enter one container:
   ```bash
   docker exec -it app1 bash
   ```
2. Ping the other container by name:
   ```bash
   ping app2
   ```

---

## **3. Inspect Networks**

### **View All Networks**
List all available networks:
```bash
docker network ls
```

**Example Output:**
```
NETWORK ID     NAME          DRIVER    SCOPE
1a2b3c4d5e6f   bridge        bridge    local
7g8h9i0j1k2l   host          host      local
3m4n5o6p7q8r   my-network    bridge    local
```

---

### **Inspect a Specific Network**
Get detailed information about a network:
```bash
docker network inspect my-network
```

**Output Details:**
- Connected containers
- Subnet and gateway
- Driver type (e.g., bridge, overlay)

---

## **4. Disconnect and Remove Networks**

### **Disconnect a Container from a Network**
```bash
docker network disconnect my-network app1
```

### **Remove a Custom Network**
```bash
docker network rm my-network
```

**Note**: You can’t remove a network if containers are still connected.

---

## **5. Example: Connecting Multiple Services**

### **Scenario**
You have a web server and a database that need to communicate privately.

### **Steps**:
1. **Create a Custom Network**:
   ```bash
   docker network create web-network
   ```

2. **Run the Database**:
   ```bash
   docker run -d --name db --network web-network postgres
   ```

3. **Run the Web Server**:
   ```bash
   docker run -d --name web --network web-network nginx
   ```

4. **Test Communication**:
   - Enter the web container:
     ```bash
     docker exec -it web bash
     ```
   - Ping the database:
     ```bash
     ping db
     ```

---

## **6. Summary of Commands**

| **Command**                                  | **Description**                                           |
|----------------------------------------------|-----------------------------------------------------------|
| `docker network ls`                          | List all Docker networks                                  |
| `docker network create my-network`           | Create a custom network                                   |
| `docker run --network my-network nginx`      | Connect a container to a specific network                |
| `docker network inspect my-network`          | View details of a specific network                       |
| `docker network disconnect my-network app1`  | Disconnect a container from a network                    |
| `docker network rm my-network`               | Remove a custom network                                  |

---

## **Use Cases for Networking**

| **Scenario**                        | **Recommended Network**            |
|-------------------------------------|------------------------------------|
| Isolated containers for testing     | **None**                           |
| High performance, host-level access | **Host**                           |
| Inter-container communication       | **Bridge or Custom Network**       |
| Multi-host networking               | **Overlay (with Swarm or Kubernetes)** |

---

With Docker networking, you can build scalable and isolated environments for your applications. Let me know if you need examples involving Docker Compose or Kubernetes! 🚀