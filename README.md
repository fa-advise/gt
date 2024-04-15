# Docker Compose Configuration for Application Deployment

This repository contains the Docker Compose files necessary to deploy an application stack consisting of a web service, MongoDB, RabbitMQ, and Redis. The services are configured to run with host network mode for simplified networking configuration.

## Services

### Web
The `web` service uses an image from a private registry and includes several environment variables to configure the application. It depends on `mongo_master`, `rabbitmq`, and `redis` services.

- **Image**: `reg.fa-advise.net:2083/gt:v1.4-beta.11`
- **Environment Variables**:
  - `COMPOSER_MEMORY_LIMIT=-1` — Removes limit on composer's memory usage.
  - `APP_TYPE` — (The value needs to be specified or removed if unused.)
  - `ENV=prod` — Sets the environment as production.
  - `PROD=yes` — Indicates the application is running in production mode.
- **Volumes**:
  - Binds a license file from the host to the container.
- **Network Mode**: Host
- **Extra Hosts**: Provides hostname resolution for the dependent services within the container.

### MongoDB Master
Configuration for MongoDB using version 3.4.

- **Image**: `mongo:3.4`
- **Volumes**:
  - Persistent storage for MongoDB data.
  - Custom MongoDB configuration file.
- **Network Mode**: Host

### RabbitMQ
Sets up RabbitMQ using version 3.7.12.

- **Image**: `rabbitmq:3.7.12`
- **Network Mode**: Host

### Redis
Defines the Redis service using version 5.0.3.

- **Image**: `redis:5.0.3`
- **Network Mode**: Host

## Volumes

- **mongo**: Defines a volume for MongoDB data persistence.

## Usage

To deploy this application stack, ensure Docker and Docker Compose are installed on your host machine. Run the following command in the directory containing the `docker-compose.yml` file:

```bash
docker-compose up -d
