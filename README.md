# n8n Bootcamp Repository

This repository will be made publicly available and will serve as a hub for various n8n-related projects. Our goal is to provide a comprehensive resource for both beginners and experienced users looking to leverage the power of n8n.

## Available Docker Compose Flavors

This repository offers multiple Docker Compose configurations to suit different needs:

### 1. Standard Setup (01_n8n-postgres-redis)

A streamlined workflow automation environment with core components:

- **n8n**: Workflow automation engine with webhook support
- **Postgres**: Relational database for persistent storage of workflows and data
- **Redis**: In-memory data store for queue management and improved performance

**Best for**: General automation workflows, production deployments, and standard n8n implementations.

### 2. AI-Enhanced Setup (02_n8n-postgres-redis-ollama-qdrant)

A comprehensive environment with built-in AI capabilities:

- **n8n**: Core workflow automation engine
- **Postgres**: Relational database for workflow data storage
- **Redis**: In-memory data store for queues and caching
- **Ollama**: Local LLM runtime for on-premise AI capabilities without external API dependencies
- **Qdrant**: Vector database for semantic search and AI-powered similarity queries

**Best for**: AI-enhanced workflows, semantic search implementations, and projects requiring local LLM processing.

## Component Overview

Below is a brief introduction to each component and its purpose:

- **n8n**: Workflow automation tool for connecting apps and automating tasks.
- **Ollama**: Local LLM (Large Language Model) runtime for AI-powered features and chatbots.
- **Postgres**: Relational database for storing workflow data and application state.
- **Redis**: In-memory data store for caching, queues, and fast data access.
- **Qdrant**: Vector database for semantic search and AI-powered similarity queries.

Each component is included in the docker-compose setups to provide a complete environment for building, testing, and running advanced automation workflows with AI and data capabilities.

## Getting Started

To use any of the provided Docker Compose configurations:

1. Navigate to the desired setup directory:

   ```bash
   cd local-docker-options/01_n8n-postgres-redis
   # OR
   cd local-docker-options/02_n8n-postgres-redis-ollama-qdrant
   ```

2. Create the required data directories (see each directory's README for specific folders)

   For Standard Setup:

   ```bash
   mkdir -p n8n_data postgres_data redis_data
   ```

   For AI-Enhanced Setup:

   ```bash
   mkdir -p shared n8n_data postgres_data redis_data qdrant_data ollama_data
   ```

3. Create a `.env` file with the necessary environment variables (see README in each directory for details)

4. Start the services:

   ```bash
   docker-compose up -d
   ```

5. Access the n8n web interface at `http://localhost:5678` (or your configured port)

6. To stop the services:

   ```bash
   docker-compose down
   ```

Each configuration directory contains its own README with more detailed information about the specific setup and environment variables needed.

## System Requirements

- Docker and Docker Compose installed on your system
- Minimum 4GB RAM (8GB recommended for AI-enhanced setup)
- At least 10GB of free disk space (more if using multiple LLM models with Ollama)
- Internet connection for initial container downloads

## Use Cases

- **Standard Setup**: Perfect for building automations that connect various services, process data, or create custom API workflows.
- **AI-Enhanced Setup**: Ideal for:
  - Automated content generation
  - Document analysis and summarization
  - Sentiment analysis
  - Knowledge base creation with semantic search
  - Text classification and extraction
  - AI-powered decision making

## Contributing

Contributions to this repository are welcome. Please feel free to submit pull requests or open issues for bugs, feature requests, or documentation improvements.

