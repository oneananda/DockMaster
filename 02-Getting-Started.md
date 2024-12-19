# ⚙️ **2. Getting Started**

This section will guide you through setting up Docker on your system and running your first container. By the end of this tutorial, you’ll have Docker installed and see it in action with the **Hello World** container.

---

## **Step 1: Install Docker**

Docker can be installed on various operating systems, including **Windows**, **macOS**, and **Linux**. Follow the official documentation for your OS to ensure you get the latest version.

### **1.1 Installation Guides**

- **Windows**  
  Install Docker Desktop for Windows. Ensure your system meets the requirements (Windows 10/11 or Windows Server 2016+).  
  👉 [Follow the Official Guide](https://docs.docker.com/desktop/install/windows-install/)

- **macOS**  
  Install Docker Desktop for macOS. Supported on Apple Silicon and Intel-based Macs.  
  👉 [Follow the Official Guide](https://docs.docker.com/desktop/install/mac-install/)

- **Linux**  
  Install Docker Engine on your distribution (Ubuntu, Debian, CentOS, etc.).  
  👉 [Follow the Official Guide](https://docs.docker.com/engine/install/)

---

### **1.2 Verify Installation**

After installation, verify Docker is installed correctly by checking the version:

```bash
docker --version
```

Expected output:
```
Docker version XX.XX.XX, build XXXXXXX
```

---

## **Step 2: Run Your First Container**

Now that Docker is installed, let’s run the **Hello World** container to confirm everything is set up correctly.

### **2.1 Pull and Run the Hello World Image**

Run the following command in your terminal:

```bash
docker run hello-world
```

### **2.2 What Happens?**
1. **Pull the Image**:  
   If the `hello-world` image is not already on your system, Docker will pull it from the Docker Hub repository.
2. **Run the Container**:  
   Docker creates a container from the image and runs it.

### **2.3 Output Example**

When you run the command, you should see output similar to this:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

---

## **Step 3: Understand What Just Happened**

Here’s what occurred behind the scenes when you ran the `hello-world` container:

1. **Docker Daemon**: The Docker client communicated with the Docker Daemon (background service) to execute the command.
2. **Image Pulling**: The `hello-world` image was pulled from **Docker Hub**, the default Docker image registry.
3. **Container Execution**: Docker created a container from the image and ran its default command, which printed the message.

---

## **Step 4: Clean Up (Optional)**

To remove the `hello-world` container and free up space:

1. View all containers (running and stopped):
   ```bash
   docker ps -a
   ```

2. Remove the container:
   ```bash
   docker rm [CONTAINER_ID]
   ```

3. Remove the `hello-world` image:
   ```bash
   docker rmi hello-world
   ```

---

By following these steps, you’ve successfully set up Docker and run your first container! 🎉 You’re now ready to explore more advanced topics and unleash Docker's full potential.

