# Hermes Agent

A fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — an AI agent framework powered by Hermes models with tool-use and function-calling capabilities.

> **Personal fork** — I'm using this to experiment with local LLM agents via [Ollama](https://ollama.com/) and [LM Studio](https://lmstudio.ai/).

## Features

- 🤖 **Hermes Model Integration** — Optimized for NousResearch Hermes series models
- 🛠️ **Tool Use & Function Calling** — Native support for structured tool invocation
- 🔄 **Multi-step Reasoning** — Agentic loops with reflection and planning
- 🐳 **Docker Support** — Containerized deployment ready
- ⚙️ **Flexible Configuration** — Extensive `.env`-based configuration

## Requirements

- Python 3.10+
- An OpenAI-compatible API endpoint (local or cloud)
- Docker (optional, for containerized deployment)

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/your-org/hermes-agent.git
cd hermes-agent
```

### 2. Set up environment

```bash
cp .env.example .env
# Edit .env with your configuration
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the agent

```bash
python main.py
```

## Docker

```bash
docker build -t hermes-agent .
docker run --env-file .env hermes-agent
```

## Configuration

All configuration is handled via environment variables. See [`.env.example`](.env.example) for a full list of options.

| Variable | Description | Default |
|---|---|---|
| `OPENAI_API_BASE` | Base URL for the OpenAI-compatible API | `http://localhost:11434/v1` |
| `OPENAI_API_KEY` | API key for authentication | `sk-...` |
| `MODEL_NAME` | Model identifier to use | `NousResearch/Hermes-3-Llama-3.1-8B` |
| `MAX_ITERATIONS` | Maximum agentic loop iterations | `10` |
| `TEMPERATURE` | Sampling temperature | `0.3` |
| `REQUEST_TIMEOUT` | HTTP request timeout in seconds | `120` |
| `LOG_LEVEL` | Logging verbosity (`DEBUG`, `INFO`, `WARNING`) | `INFO` |
| `STREAM_OUTPUT` | Stream tokens to stdout as they are generated | `false` |
| `MAX_TOKENS` | Maximum tokens to generate per response | `2048` |
| `SYSTEM_PROMPT_FILE` | Path to a file containing a custom system prompt | *(unset)* |

> **Note:** I've updated `OPENAI_API_BASE` to default to `http://localhost:11434/v1` (Ollama's default port) since that's my primary local setup.

> **Note:** Bumped `MAX_ITERATIONS` default from `5` to `10` — I found 5 was too often cutting off multi-step tasks before completion during local testing.

> **Note:** Added `REQUEST_TIMEOUT` defaulting to `120s` — local models can be slow to respond, especially on first load, and the original 30s default was causing frequent timeout errors on my machine.

> **Note:** Added `LOG_LEVEL` — I set this to `DEBUG` locally when I'm actively debugging tool-call behavior, and `WARNING` when I just want to run things quietly.

> **Note:** Added `STREAM_OUTPUT` — setting this to `true` makes responses feel much more responsive when run interactively. Defaults to `false` to keep log output clean when running non-interactively or in Docker.

> **Note:** Bumped `MAX_TOKENS` default from `1024` to `2048` — some tool responses and multi-step reasoning chains were getting truncated mid-output at 1024, particularly when the model was summarizing long tool results.
