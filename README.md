# Docker Compose Health Check Examples

This repository contains examples of different health check strategies in Docker Compose. Each example is located in its own directory with a corresponding `docker-compose.yml` file. These examples demonstrate how to ensure that services in a Docker Compose environment are healthy and ready to serve requests.

## Directory Structure

```
.
├── startup-example
│   └── docker-compose.yml
│   └── Dockerfile
│   └── app.jar
├── service-completed
│   └── docker-compose.yml
├── process-id
│   └── docker-compose.yml
└──port-listening
    └── docker-compose.yml
```

## Examples

### Control startup and shutdown order in Compose

**Directory:** `startup-example`

This example is based on the Docker Compose startup example from the official Docker documentation. For more details, please refer to the following link: [https://docs.docker.com/compose/startup-order/](https://docs.docker.com/compose/startup-order/).


#### Usage:

1. Navigate to the `startup-example` directory.
2. Run the Docker Compose build:
    ```bash
    docker-compose build
    ```
3. Run the Docker Compose setup:
   ```bash
   docker-compose up -d
   ```
4. Observe how the health check is performed by 'service_healthy' and 'service_started'.
5. Note that the `web` service will only start after the `db` service is healthy and `redis` service is started.

### Service Completed Successfully

**Directory:** `service-completed`

This example demonstrates how to use the `service_completed_successfully` condition in Docker Compose to manage dependencies between services. A `healthcheck` service is used to ensure that `app1` and `app2` are ready before `app3` starts.

#### Usage:

1. Navigate to the `service-completed` directory.
2. Run the Docker Compose setup:
   ```bash
   docker-compose up -d
   ```
3. The app3 service will only start after app1 and app2 have been confirmed as healthy and the healthcheck container has completed successfully.

### Process ID Check

**Directory:** `process-id`

This example uses `pidof` to check if a Java application is running by monitoring its process ID. This approach is useful in minimal Docker images where traditional tools might not be available.

#### Usage:

1. Navigate to the `process-id` directory.
2. Run the Docker Compose setup:
   ```bash
   docker-compose up -d
   ```
3. The health check will verify if the Java process is running by checking its PID.

### TCP Port Listening Check

**Directory:** `port-listening`

This example demonstrates how to check if a specific TCP port is in the LISTEN state, indicating that the service is ready to accept connections. It uses `grep` to monitor the `/proc/net/tcp` file for the port number.

#### Usage:

1. Navigate to the `port-listening` directory.
2. Run the Docker Compose setup:
   ```bash
   docker-compose up -d
   ```
3. The health check will ensure that the application is listening on the expected port before marking the service as healthy.

## Conclusion

These examples provide practical strategies for implementing health checks in Docker Compose environments. Depending on your application and infrastructure, you can choose the most suitable method to ensure your services are ready and healthy.

For more detailed information, refer to each example's `docker-compose.yml` file and modify them according to your needs.
