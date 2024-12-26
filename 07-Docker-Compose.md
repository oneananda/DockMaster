# 🛠️ **7. Docker Compose**

Docker Compose simplifies the management of multi-container applications by using a single configuration file (`docker-compose.yml`). This tool enables you to define, configure, and manage interconnected services effortlessly.

---

## **1. What is Docker Compose?**

Docker Compose allows you to:
- Define multi-container applications with all configurations in a single YAML file.
- Manage containers as a group using simple commands.
- Set up networks, volumes, and environment variables for your services.

---

## **2. Install Docker Compose**

Docker Compose is included with **Docker Desktop** on Windows and macOS. For Linux, it may require a separate installation.

### **Installation Instructions**
1. **Windows/Mac**: Installed automatically with Docker Desktop.
2. **Linux**: Use the official installation script:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep -Po '"tag_name": "\K.*?(?=")')/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```
3. **Verify Installation**:
   ```bash
   docker-compose --version
   ```

---

## **3. Write a `docker-compose.yml` File**

A `docker-compose.yml` file defines your application’s services, their configurations, networks, and volumes.

### **Example: Web and Database**
Here’s an example YAML configuration for a web server and a MySQL database:

```yaml
version: '3'
services:
  web:
    image: nginx             # Uses the NGINX image
    ports:
      - "8080:80"            # Maps host port 8080 to container port 80

  db:
    image: mysql             # Uses the MySQL image
    environment:             # Sets environment variables
      MYSQL_ROOT_PASSWORD: password
```

---

## **4. Run a Multi-Container Application**

### **Start Services**
Run the following command to start the services defined in `docker-compose.yml`:
```bash
docker-compose up
```

**Output**: Docker Compose pulls the images, creates containers, and starts them. The web server will be accessible at `http://localhost:8080`.

### **Run in Detached Mode**
To run containers in the background:
```bash
docker-compose up -d
```

---

### **Stop Services**
Stop all running containers:
```bash
docker-compose down
```

---

## **5. Understand the Example**

### **How It Works**
1. **Web Service**:
   - Runs an NGINX container.
   - Maps port 8080 on the host to port 80 in the container.

2. **Database Service**:
   - Runs a MySQL container.
   - Sets the root password using the `environment` key.

---

## **6. Key Docker Compose Commands**

| **Command**                          | **Description**                                               |
|--------------------------------------|---------------------------------------------------------------|
| `docker-compose up`                  | Start services (create containers if they don’t exist).       |
| `docker-compose up -d`               | Start services in detached mode (run in the background).      |
| `docker-compose down`                | Stop and remove containers, networks, and volumes.            |
| `docker-compose ps`                  | List all running services.                                    |
| `docker-compose logs`                | View logs for all services.                                   |
| `docker-compose build`               | Build images specified in `docker-compose.yml`.               |
| `docker-compose stop`                | Stop running services without removing containers.            |
| `docker-compose restart`             | Restart services.                                             |

---

## **7. Advanced Features**

### **Add Volumes**
Persist data by defining volumes:
```yaml
version: '3'
services:
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: password
    volumes:
      - db-data:/var/lib/mysql

volumes:
  db-data:
```

### **Define Networks**
Customize how containers communicate:
```yaml
version: '3'
services:
  web:
    image: nginx
    networks:
      - app-network

  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: password
    networks:
      - app-network

networks:
  app-network:
```

---

## **8. Summary**

| **Action**                | **Command**                                                                                 |
|---------------------------|---------------------------------------------------------------------------------------------|
| Define services           | Use `docker-compose.yml` to configure containers, ports, volumes, and networks.            |
| Start services            | `docker-compose up`                                                                        |
| Stop services             | `docker-compose down`                                                                      |
| Scale services            | `docker-compose up --scale <service>=<count>`                                              |
| Debug issues              | Use `docker-compose logs` and `docker-compose ps` for troubleshooting.                     |

---

Docker Compose simplifies the orchestration of multi-container applications, making it easier to manage interconnected services. Let me know if you’d like a more complex example or an introduction to using Docker Compose with Docker Swarm or Kubernetes! 🚀

