# n8n Bootcamp Repository

This repository going to have docker-compose file with n8n, postgress, redis images

## Here's a detailed look at what you can expect

Below is a brief introduction to each component and its purpose:

- **n8n**: Workflow automation tool for connecting apps and automating tasks.
- **Postgres**: Relational database for storing workflow data and application state.
- **Redis**: In-memory data store for caching, queues, and fast data access.

This docker-compose setup provides the essential components needed for running n8n workflows with persistent storage and improved performance.

## Overview

This Docker Compose architecture creates a streamlined workflow automation environment with three core components:

### Container Architecture

- **n8n Container**: Core workflow automation engine
  - Ports: Dynamically set through environment variable ${N8N_PORT}
  - Dependencies: Postgres, Redis
  - Volumes: n8n data directory for persistence
  - Features: Basic auth support, encryption key configuration, timezone settings
  - Security: Enforces settings file permissions

- **Postgres Container**: Primary database storage
  - Image: PostgreSQL 16
  - Volumes: Persisted database files
  - Purpose: Stores workflow data, credentials, and execution history
  - Environment: Configurable database name, user, and password
  - Health checks: Ensures database is ready before n8n starts

- **Redis Container**: In-memory data store
  - Image: Redis 7 Alpine (lightweight)
  - Volumes: Persistent Redis data
  - Configuration: Appendonly mode for data durability
  - Purpose: Queue management, workflow execution distribution
  - Health checks: Verifies Redis availability before n8n starts

### Data Flow

- n8n orchestrates workflows and connects to external services
- Postgres provides persistent data storage for workflow configurations and state
- Redis manages execution queues and enables distributed execution mode

### Network Configuration

All services are connected through an internal Docker network, with n8n's port exposed for external access.

### Environment Variables

The setup uses environment variables for configuration, allowing easy customization of:

- Connection details (host, ports)
- Database credentials
- Redis connection settings
- Authentication settings
- Encryption keys

### Data Folders

The following folders need to be available before running the docker-compose setup:

- `./n8n_data`: Stores n8n configuration, workflows, and credentials
- `./postgres_data`: Contains PostgreSQL database files
- `./redis_data`: Stores Redis persistence data

**_Note:_** These folders should be created in the same directory as your `docker-compose.yml` file. and should be empty before starting the containers for the first time.

#### Creating Required Folders

Before running the docker-compose setup, create these folders using one of the following commands based on your operating system:

**DOS/CMD (Windows):**

```cmd
mkdir n8n_data postgres_data redis_data
```

**PowerShell (Windows):**

```powershell
New-Item -ItemType Directory -Path "n8n_data", "postgres_data", "redis_data" -Force
```

**Shell (Linux/macOS):**

```bash
mkdir -p n8n_data postgres_data redis_data
```

Make sure to run these commands in the same directory as your docker-compose.yml file.

