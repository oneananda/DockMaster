# 🧑‍💻 **8. Docker in Development**

Docker is not just for production—it’s also a powerful tool for local development and debugging. It helps create consistent environments, simplifies dependency management, and integrates seamlessly with developer workflows.

---

## **1. Environment Variables**

Environment variables allow you to configure container behavior dynamically without hardcoding values into your code or Dockerfiles.

### **Setting Environment Variables**
1. **Inline with `docker run`**:
   ```bash
   docker run -e "ENV_VAR_NAME=value" my-app
   ```
   Example:
   ```bash
   docker run -e "NODE_ENV=development" my-app
   ```

2. **Using `docker-compose.yml`**:
   Define environment variables for services in `docker-compose.yml`:
   ```yaml
   version: '3'
   services:
     app:
       image: my-app
       environment:
         - NODE_ENV=development
         - API_URL=http://localhost:8080
   ```

3. **From an `.env` File**:
   Create an `.env` file with key-value pairs:
   ```plaintext
   NODE_ENV=development
   API_URL=http://localhost:8080
   ```

   Reference the `.env` file in `docker-compose.yml`:
   ```yaml
   version: '3'
   services:
     app:
       image: my-app
       env_file:
         - .env
   ```

**Tip**: Use environment variables to switch between development and production configurations or inject secrets (e.g., API keys).

---

## **2. Hot Reloading**

Hot reloading improves productivity by automatically applying code changes to running containers without needing to rebuild images or restart containers.

### **Set Up Hot Reloading**
1. **Bind Mount the Source Code**:
   Use a bind mount to share the source code directory with the container:
   ```bash
   docker run -v $(pwd):/app my-app
   ```

   In `docker-compose.yml`:
   ```yaml
   version: '3'
   services:
     app:
       image: my-app
       volumes:
         - ./src:/app/src
   ```

2. **Install a File Watcher**:
   Ensure your application supports file watching for automatic reloading. Examples:
   - **Node.js**: Use `nodemon` to restart the server on changes.
     ```bash
     npm install -g nodemon
     nodemon server.js
     ```
   - **Python**: Use `watchdog` or frameworks with built-in reload support (e.g., Flask's debug mode).

3. **Test Hot Reloading**:
   Modify a file in your project directory and verify the application updates automatically in the container.

---

## **3. Debugging Containers**

Debugging a running container is essential for troubleshooting issues during development.

### **3.1 Access the Container Shell**
Attach to a running container’s shell for manual inspection:
```bash
docker exec -it <container_id> /bin/bash
```
Example:
```bash
docker exec -it my-app-container /bin/bash
```

### **3.2 Check Logs**
View real-time logs for a container:
```bash
docker logs -f <container_id>
```

### **3.3 Debug with Docker Compose**
Use `docker-compose logs` to see logs for all services in a multi-container setup:
```bash
docker-compose logs -f
```

### **3.4 Expose Debugging Ports**
Expose debugging ports to connect with debuggers like **VS Code**, **PyCharm**, or **Chrome DevTools**:
1. Update `docker-compose.yml`:
   ```yaml
   services:
     app:
       image: my-app
       ports:
         - "9229:9229" # Node.js debugger port
   ```
2. Start the container:
   ```bash
   docker-compose up
   ```
3. Attach your IDE debugger to the exposed port.

### **3.5 Use Debugging Tools Inside Containers**
Install debugging tools in your container:
- **Node.js**: Run with the `--inspect` flag to enable debugging.
  ```bash
  docker run -p 9229:9229 -v $(pwd):/app my-app node --inspect server.js
  ```
- **Python**: Use `debugpy` to attach a remote debugger.

---

## **4. Example: Dockerized Development Workflow**

Here’s an example setup for a Node.js application with hot reloading and debugging:

### **Dockerfile**
```Dockerfile
FROM node:16
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "run", "start:dev"]
```

### **docker-compose.yml**
```yaml
version: '3'
services:
  app:
    build: .
    volumes:
      - .:/app
    ports:
      - "3000:3000"
      - "9229:9229" # Debugger port
    environment:
      NODE_ENV: development
```

### **Start the Services**
```bash
docker-compose up
```

---

## **5. Summary**

| **Feature**              | **Command/Configuration**                                                                     |
|--------------------------|-----------------------------------------------------------------------------------------------|
| Set environment variables | `-e "VAR_NAME=value"` or `environment` in `docker-compose.yml`.                              |
| Use hot reloading         | Bind mount source code and use file watchers (e.g., `nodemon`, Flask debug mode).            |
| Access container shell    | `docker exec -it <container_id> /bin/bash`.                                                  |
| View container logs       | `docker logs -f <container_id>` or `docker-compose logs -f`.                                 |
| Debug application         | Expose debugging ports (e.g., `9229` for Node.js) and attach a debugger from your IDE.       |

---

With these techniques, you can efficiently develop, debug, and test applications using Docker. Let me know if you'd like more examples or advanced configurations! 🚀

