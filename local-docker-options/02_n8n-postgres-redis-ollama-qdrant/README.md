# n8n Bootcamp Repository

This repository going to have docker-compose file with n8n, ollama, postgress, redis, qdrant images

## Here's a detailed look at what you can expect

Below is a brief introduction to each component and its purpose:

- **n8n**: Workflow automation tool for connecting apps and automating tasks.
- **Ollama**: Local LLM (Large Language Model) runtime for AI-powered features and chatbots.
- **Postgres**: Relational database for storing workflow data and application state.
- **Redis**: In-memory data store for caching, queues, and fast data access.
- **Qdrant**: Vector database for semantic search and AI-powered similarity queries.

Each component is included in this docker-compose setup to provide a complete environment for building, testing, and running advanced automation workflows with AI capabilities.

## Overview

This Docker Compose architecture creates a comprehensive workflow automation environment with built-in AI capabilities:

### Container Architecture

- **n8n Container**: Core workflow automation engine
  - Ports: 5678:5678 (Web UI access)
  - Dependencies: Postgres, Redis, Qdrant, Ollama
  - Volumes: Shared folder for file exchange with Ollama, n8n data persistence
  - Features: Basic auth support, secure configuration options

- **Postgres Container**: Primary database storage
  - Ports: 5432:5432
  - Volumes: Persisted database files
  - Purpose: Stores workflow data, credentials, and execution history
  - Health checks: Ensures database is ready before n8n starts

- **Redis Container**: In-memory data store
  - Volumes: Persistent Redis data
  - Configuration: Appendonly mode for data durability
  - Purpose: Queue management, workflow execution distribution
  - Health checks: Verifies Redis availability before n8n starts

- **Qdrant Container**: Vector database for AI operations
  - Ports: 6333:6333 (API), 6334:6334 (gRPC)
  - Volumes: Vector database storage
  - Purpose: Enables semantic search and vector operations for AI workflows

- **Ollama Container**: Local LLM runtime
  - Ports: 11434:11434
  - Volumes: Model storage, shared folder with n8n
  - Purpose: Provides on-premise AI language model capabilities
  - Configuration: Configured for network accessibility

### Data Flow

- n8n orchestrates workflows between all components
- Postgres provides persistent data storage for workflows and state
- Redis manages execution queues and real-time data
- Ollama provides local LLM capabilities without external API dependencies
- Qdrant enables vector-based operations for AI-enhanced workflows

### Network Configuration

All services are connected through an internal Docker network, with selected ports exposed for external access.

