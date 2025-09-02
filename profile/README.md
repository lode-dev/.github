<p align="center">
  <img src="https://raw.githubusercontent.com/lode-dev/.github/main/lode-logo-solid.png" alt="Lode Logo" width="150">
</p>

<h1 align="center">Lode - The AI Log Assistant</h1>

<p align="center">
  <strong>An opinionated, developer-first AI log assistant for the local development lifecycle.</strong>
  <br />
  Designed for solo developers and small projects where enterprise tools are overkill.
</p>

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#architecture">Architecture</a> •
  <a href="#repositories">Repositories</a> •
  <a href="#getting-started">Getting Started</a>
</p>

---

**Lode's entire philosophy is 'zero-to-insight in under 5 minutes'—a single command to launch, no complex setup, and an interactive UI that prioritizes clarity over complexity.** It's the precision screwdriver for a developer's local workbench, not the sledgehammer for enterprise-wide data collection.

## ✨ Key Features

* **Conversational AI Assistant:** Chat with your logs. Ask questions in natural language ("summarize the errors from the last hour") and get **streaming responses** from a local LLM to accelerate debugging.
* **Minimal Setup:** Launch the entire multi-container stack (API, UI, databases, cache, LLM) with a single `docker-compose up` command.
* **Real-Time Tailing:** See raw logs appear instantly with a WebSocket-powered "Live Tail."
* **Powerful Filtering & Search:** An intelligent autocomplete bar for specific field filtering (`level:error`) and robust full-text search.
* **Performance Caching:** Integrates **Redis** to cache expensive queries and aggregation results, ensuring a snappy user experience.
* **Drop-in Python Logger:** Includes the `lode-logger`, a lightweight client designed as a simple replacement for Python's standard logging module.

## 🛠️ Tech Stack

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React">
  <img src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="Redis">
  <img src="https://img.shields.io/badge/OpenSearch-005EB8?style=for-the-badge&logo=opensearch&logoColor=white" alt="OpenSearch">
  <img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama">
</p>

---

## 🏗️ Architecture

Lode uses a multi-repository, microservice-oriented architecture. It demonstrates proficiency with both NoSQL and SQL databases, caching layers, and interaction with a local LLM.

```mermaid
graph LR
    subgraph "Developer's Machine"
        A["Browser (Lode UI)"]
        B["Your App (Log Source)"]
    end

    subgraph "Docker Network (Lode Stack)"
        C["Lode API (FastAPI)"]
        D["OpenSearch (Logs)"]
        E["Postgres (Chat History)"]
        F["Redis (Cache)"]
        G["Ollama (LLM)"]
    end

    A -- "UI/Chat Requests" --> C
    B -- "POST Logs" --> C
    C -- "WebSocket Stream" --> A
    
    C -- "Search/Write" --> D
    D -- "Results" --> C
    
    C -- "Read/Write History" --> E
    C -- "Read/Write Cache" --> F
    
    C -- "Prompts" --> G
    G -- "Streaming Tokens" --> C

    style A fill:#E3F2FD,stroke:#0D47A1
    style B fill:#E8F5E9,stroke:#1B5E20
    style C fill:#FFF3E0,stroke:#E65100
    style D fill:#ECEFF1,stroke:#263235
    style E fill:#D1E7DD,stroke:#0f5132
    style F fill:#F8D7DA,stroke:#842029
    style G fill:#D1ECF1,stroke:#0c5460
```

## 📚 Repositories

This organization contains all the components that make up the Lode platform.

| Repository                                     | Description                                                                 |
| ---------------------------------------------- | --------------------------------------------------------------------------- |
| 🚀 [**lode-deployment**](https://github.com/lode-dev/lode-deployment)     | The command center. Contains the `docker-compose.yml` to launch the stack.    |
| 🧠 [**lode-api**](https://github.com/lode-dev/lode-api)                   | The FastAPI backend for ingestion, querying, caching, and AI chat streaming.  |
| 🎨 [**lode-ui**](https://github.com/lode-dev/lode-ui)                     | The interactive React frontend for viewing logs and chatting with the AI.     |
| 📦 [**lode-logger**](https://github.com/lode-dev/lode-logger)             | A lightweight Python client library for easy log shipping.                  |
| ⚙️ [**.github**](#)                    | Project-wide assets and this README file.                       |

-----

## 🚀 Getting Started

Ready to run Lode on your machine?

1.  **Clone the deployment repository:**

    ```bash
    git clone https://github.com/lode-dev/lode-deployment.git
    cd lode-deployment
    ```

2.  **Launch the stack:**

    ```bash
    docker-compose up --build
    ```

3.  **Pull an LLM model (in a new terminal):**

    ```bash
    docker exec -it ollama ollama pull phi3:mini
    ```

4.  **You're live\!**

      * **Lode UI:** [http://localhost:5173](http://localhost:5173)
      * **Lode API Docs:** [http://localhost:8000/docs](http://localhost:8000/docs)
