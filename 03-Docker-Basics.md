# 🐳 **3. Docker Basics**

In this section, you'll learn the fundamental concepts of Docker and essential commands to get started with managing containers and images. These concepts and commands form the foundation for using Docker effectively.

---

## **Containers vs. Images**

### **What is a Docker Image?**
A Docker image is a read-only template used to create containers. It contains:
- Application code
- Runtime environment (e.g., Node.js, Python)
- System tools, libraries, and dependencies

Docker images are **static** and immutable. They act as a blueprint for creating containers.

**Example**: Think of an image as a class in programming—it defines how instances (containers) behave.

---

### **What is a Docker Container?**
A Docker container is a **runtime instance** of a Docker image. Containers are:
- **Ephemeral**: They can be started, stopped, or removed.
- **Isolated**: Each container runs in its own isolated environment.
- **Lightweight**: Containers share the host OS kernel, making them efficient.

**Example**: A container is like an object instantiated from a class—it runs based on the blueprint (image).

---

## **Key Commands**

### **1. List Running Containers**
```bash
docker ps
```
This command lists all currently running containers.

**Example Output:**
```
CONTAINER ID   IMAGE        COMMAND       CREATED       STATUS       PORTS       NAMES
123abc456xyz   ubuntu       "/bin/bash"   2 hours ago   Up 2 hours               funny_name
```

- **CONTAINER ID**: A unique identifier for each container.
- **IMAGE**: The image used to create the container.
- **STATUS**: Current state (e.g., `Up`, `Exited`).

---

### **2. List All Containers (Including Stopped)**
```bash
docker ps -a
```
Displays both running and stopped containers.

---

### **3. List All Images**
```bash
docker images
```
Lists all the Docker images available on your system.

**Example Output:**
```
REPOSITORY     TAG        IMAGE ID       CREATED        SIZE
ubuntu         latest     abc123xyz456   2 weeks ago    29MB
nginx          stable     def456uvw789   1 month ago    133MB
```

- **REPOSITORY**: The name of the image source.
- **TAG**: The version of the image.
- **IMAGE ID**: A unique identifier for the image.

---

### **4. Stop a Running Container**
```bash
docker stop <container_id>
```
Stops a running container gracefully by sending a termination signal. Replace `<container_id>` with the container's ID or name.

**Example:**
```bash
docker stop 123abc456xyz
```

---

### **5. Remove a Container**
```bash
docker rm <container_id>
```
Deletes a stopped container. Containers must be stopped before removal.

**Example:**
```bash
docker rm 123abc456xyz
```

---

### **6. Remove an Image**
```bash
docker rmi <image_id>
```
Deletes a Docker image from your system. Ensure no containers are running or stopped based on this image before deleting.

**Example:**
```bash
docker rmi abc123xyz456
```

---

## **Summary**

| **Command**             | **Description**                               |
|-------------------------|-----------------------------------------------|
| `docker ps`             | List running containers                      |
| `docker ps -a`          | List all containers (running and stopped)    |
| `docker images`         | List all available Docker images             |
| `docker stop <id>`      | Stop a running container                     |
| `docker rm <id>`        | Remove a stopped container                   |
| `docker rmi <id>`       | Remove a Docker image                        |

---

## **Concept Recap**

- **Images** are the blueprints; they define what a container will run.
- **Containers** are the runtime instances of images, lightweight and isolated.
- Managing containers and images effectively requires mastering these basic commands.

With this foundation, you’re ready to start building and managing containerized applications! Let me know if you'd like examples or interactive exercises to accompany these concepts. 🚀

