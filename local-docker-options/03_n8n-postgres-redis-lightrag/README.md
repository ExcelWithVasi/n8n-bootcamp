# n8n Bootcamp Repository

This repository contains a docker-compose file with n8n, PostgreSQL, Redis, and LightRAG images.

## Here's a detailed look at what you can expect

Below is a brief introduction to each component and its purpose:

- **n8n**: Workflow automation tool for connecting apps and automating tasks.
- **Postgres**: Relational database for storing workflow data and application state.
- **Redis**: In-memory data store for caching, queues, and fast data access.
- **LightRAG**: Retrieval-Augmented Generation system for AI-powered document search and knowledge retrieval.

This docker-compose setup provides the essential components needed for running n8n workflows with persistent storage, improved performance, and AI-powered document processing capabilities.

## Overview

This Docker Compose architecture creates a streamlined workflow automation environment with four core components:

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
  - Purpose: Queue management, workflow execution distribution, storage for LightRAG
  - Health checks: Verifies Redis availability before n8n and LightRAG start

- **LightRAG Container**: AI-powered document processing system
  - Image: LightRAG latest
  - Ports: 9621 (configurable)
  - Volumes: Storage for RAG data, inputs, and tokenization
  - Configuration: Via environment variables and config.ini
  - Dependencies: Redis for storage
  - Features: Document embedding, retrieval, and AI-powered search
  - Models: Configured to use OpenAI models for both LLM and embeddings via environment variables

### Data Flow

- n8n orchestrates workflows and connects to external services
- Postgres provides persistent data storage for workflow configurations and state
- Redis manages execution queues, enables distributed execution mode, and provides storage for LightRAG
- LightRAG processes documents and provides AI-powered search capabilities

### Network Configuration

All services are connected through an internal Docker network, with n8n's port and LightRAG's port exposed for external access.

### Environment Variables

The setup uses environment variables for configuration, allowing easy customization of:

- Connection details (host, ports)
- Database credentials
- Redis connection settings
- Authentication settings
- Encryption keys
- LightRAG configuration (embedding models, LLM settings)

### Data Folders

The following folders need to be available before running the docker-compose setup:

- `./n8n_data`: Stores n8n configuration, workflows, and credentials
- `./postgres_data`: Contains PostgreSQL database files
- `./redis_data`: Stores Redis persistence data
- `./lightrag_data/rag_storage`: Storage for LightRAG's vector database
- `./lightrag_data/inputs`: Input documents for LightRAG
- `./lightrag_data/tiktoken`: Tokenization data for LightRAG

**_Note:_** These folders should be created in the same directory as your `docker-compose.yml` file and should be empty before starting the containers for the first time.

#### Creating Required Folders

Before running the docker-compose setup, create these folders using one of the following commands based on your operating system:

**DOS/CMD (Windows):**

```cmd
mkdir n8n_data postgres_data redis_data
mkdir lightrag_data
mkdir lightrag_data\rag_storage lightrag_data\inputs lightrag_data\tiktoken
```

**PowerShell (Windows):**

```powershell
New-Item -ItemType Directory -Path "n8n_data", "postgres_data", "redis_data" -Force
New-Item -ItemType Directory -Path "lightrag_data" -Force
New-Item -ItemType Directory -Path "lightrag_data\rag_storage", "lightrag_data\inputs", "lightrag_data\tiktoken" -Force
```

**Shell (Linux/macOS):**

```bash
mkdir -p n8n_data postgres_data redis_data
mkdir -p lightrag_data/rag_storage lightrag_data/inputs lightrag_data/tiktoken
```

Make sure to run these commands in the same directory as your docker-compose.yml file.

**Important:** You'll also need to create a `config.ini` file for LightRAG in the same directory as your docker-compose.yml file before starting the containers. Additionally, you must create an `.env` file with your OpenAI API key and other configuration values for LightRAG to properly utilize OpenAI's models for both LLM and embedding functionality. This environment configuration is critical for the proper functioning of the AI capabilities.

