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
