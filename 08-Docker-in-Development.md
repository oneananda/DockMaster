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
