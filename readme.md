# Docker Compose Templates

This repository contains Docker Compose templates for common development services including databases, message queues, caching, and configuration management tools.

All services are configured with minimal resource limits optimized for running multiple services simultaneously on a development machine.

## Quick Links

- [Prerequisites](#prerequisites)
  - [Docker Desktop](#option-1-docker-desktop)
  - [Podman Desktop](#option-2-podman-desktop)
- [Resource Limits](#resource-limits)
- [Running Services](#running-services)
  - [Using Docker Desktop](#using-docker-desktop)
  - [Using Podman Desktop](#using-podman-desktop)
- [Managing Services](#managing-services)
- [Service Access](#service-access)
- [Container Names](#container-names)
- [Notes](#notes)

## Prerequisites

You can use either **Docker Desktop** or **Podman Desktop** to run these containers.

### Option 1: Docker Desktop

Download and install Docker Desktop:
- **Windows/Mac**: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
- **Linux**: [https://docs.docker.com/desktop/install/linux-install/](https://docs.docker.com/desktop/install/linux-install/)

Docker Desktop includes `docker-compose` by default.

Verify installation:
```bash
docker --version
docker-compose --version
```

### Option 2: Podman Desktop

Download and install Podman Desktop:
- **All platforms**: [https://podman-desktop.io/downloads](https://podman-desktop.io/downloads)

For Podman, you'll need to install `podman-compose`:

Make sure you have pip installed:
```bash
pip --version
```

Expected output:
```
pip 25.0.1 from c:\python38\lib\site-packages\pip (python 3.8)
```

Install podman-compose:
```bash
pip install podman-compose
```

Verify installation:
```bash
podman-compose --version
```
Expected output:
```
podman-compose version 1.4.1
podman version 5.5.1
```

## Resource Limits

All services are configured with minimal resource limits:
- **Cache services** (Redis, Memcached): 0.1 CPU / 64MB
- **Databases** (PostgreSQL, MongoDB): 0.25 CPU / 128MB
- **Kafka & Zookeeper**: 0.25 CPU / 256MB
- **Consul & Vault**: 0.25 CPU / 128MB
- **pgAdmin**: 0.1 CPU / 64MB

Total if all services run: ~1.8 CPUs / ~1.2GB RAM

## Running Services

### Using Docker Desktop

#### Database Services (PostgreSQL & MongoDB)
```bash
docker-compose -f ./docker-compose-db.yml up -d
```

#### Kafka and Zookeeper
```bash
docker-compose -f ./docker-compose-kafka.yml up -d
```

#### Consul and Vault
```bash
docker-compose -f ./docker-compose-consul-vault.yml up -d
```

#### Cache Services (Redis & Memcached)
```bash
docker-compose -f ./docker-compose-cache.yml up -d
```

#### pgAdmin
```bash
docker-compose -f ./docker-compose-pgadmin.yml up -d
```

### Using Podman Desktop

#### Database Services (PostgreSQL & MongoDB)
```bash
podman-compose -f ./docker-compose-db.yml up -d
```

#### Kafka and Zookeeper
```bash
podman-compose -f ./docker-compose-kafka.yml up -d
```

#### Consul and Vault
```bash
podman-compose -f ./docker-compose-consul-vault.yml up -d
```

#### Cache Services (Redis & Memcached)
```bash
podman-compose -f ./docker-compose-cache.yml up -d
```

#### pgAdmin
```bash
podman-compose -f ./docker-compose-pgadmin.yml up -d
```

## Managing Services

### Stop Services

**Docker Desktop:**
```bash
docker-compose -f ./docker-compose-[service].yml down
```

**Podman Desktop:**
```bash
podman-compose -f ./docker-compose-[service].yml down
```

### View Logs

**Docker Desktop:**
```bash
docker-compose -f ./docker-compose-[service].yml logs -f
```

**Podman Desktop:**
```bash
podman-compose -f ./docker-compose-[service].yml logs -f
```

### Restart Services

**Docker Desktop:**
```bash
docker-compose -f ./docker-compose-[service].yml restart
```

**Podman Desktop:**
```bash
podman-compose -f ./docker-compose-[service].yml restart
```

## Service Access

Once services are running, you can access them at:

- **PostgreSQL**: `localhost:5432` (user: admin, password: admin)
- **MongoDB**: `localhost:27017` (user: mongo, password: mongo)
- **Redis**: `localhost:6379`
- **Memcached**: `localhost:11211`
- **Kafka**: `localhost:9092`
- **Zookeeper**: `localhost:2181`
- **Consul UI**: `http://localhost:8500`
- **Vault**: `http://localhost:8200`
- **pgAdmin**: `http://localhost:8181`

## Container Names

All containers are named with their service name and version for easy identification:

- `redis-6.2` - Redis cache server
- `memcached-1.6.18` - Memcached cache server
- `postgres-16.1` - PostgreSQL database
- `mongodb-6.0` - MongoDB database
- `kafka-3.6` - Apache Kafka
- `zookeeper-3.9` - Apache Zookeeper
- `consul-server` - HashiCorp Consul
- `vault-server` - HashiCorp Vault
- `pgadmin4` - pgAdmin web interface

You can view running containers with:
```bash
# Docker Desktop
docker ps

# Podman Desktop
podman ps
```

## Notes

- Resource limits are set to minimum values for development purposes
- If services fail to start or become unresponsive, you may need to increase resource limits
- For production use, significantly higher resource limits are recommended
- All credentials shown here are defaults for development only - change them for production use
- All containers are named with their version for easy identification