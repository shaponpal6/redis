

1. **Dockerfile**:

Create a file named `Dockerfile` with the following content:

```Dockerfile
# Use the official Redis image from Docker Hub
FROM redis:latest

# Expose Redis port
EXPOSE 6379
```

This Dockerfile instructs Docker to use the latest Redis image from Docker Hub and exposes port 6379, which is the default port for Redis.

2. **Docker Compose file**:

Create a file named `docker-compose.yml` with the following content:

```yaml
version: '3.8'

services:
  redis:
    image: redis:latest
    container_name: my-redis-container
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data

volumes:
  redis_data:
    driver: local
```

In this Docker Compose file:

- We define a service named `redis` using the official Redis image.
- We specify the container name as `my-redis-container`.
- We map port 6379 on the host to port 6379 on the container.
- We define a named volume `redis_data` to persist Redis data.

3. **Building and Running**:

To build and run the Redis container using Docker Compose, navigate to the directory containing the Dockerfile and docker-compose.yml file and run the following command:

```bash
docker-compose up -d
```

This command will start the Redis container in detached mode (`-d`), and you should see output indicating that the container is running.

You can verify that the Redis container is running by executing:

```bash
docker ps
```

To connect to the Redis server from another terminal window, you can use the `redis-cli` tool:

```bash
redis-cli -h localhost -p 6379
```


**Install Redis**: You can install Redis directly on your local machine. Depending on your operating system, you can use a package manager like Homebrew for macOS or APT for Debian-based Linux distributions. Once installed, you should have access to the `redis-cli` command.

**Use Docker**: If you're running Redis inside a Docker container as described previously, you can execute `redis-cli` from within another Docker container. Here's how you can do it:

   ```bash
   docker run -it --rm --network=host redis redis-cli -h localhost -p 6379
   ```

   This command runs a temporary Docker container with the Redis CLI tool (`redis-cli`) and connects it to the Redis server running on localhost.

**Use Redis Docker Container Shell**: Alternatively, you can access the Redis server's command-line interface directly from the Docker container running Redis. You can do this by executing a shell inside the Redis container:

   ```bash
   docker exec -it my-redis-container sh
   ```

Replace `my-redis-container` with the name of your Redis container. Once inside the container's shell, you can execute `redis-cli` commands directly.

Choose the method that best fits your requirements and environment.