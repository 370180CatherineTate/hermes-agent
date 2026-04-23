# Hermes Agent

A fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — an AI agent framework powered by Hermes models with tool-use and function-calling capabilities.

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
| `OPENAI_API_BASE` | Base URL for the OpenAI-compatible API | `http://localhost:8000/v1` |
| `OPENAI_API_KEY` | API key for authentication | `sk-...` |
| `MODEL_NAME` | Model identifier to use | `NousResearch/Hermes-3-Llama-3.1-8B` |
| `MAX_ITERATIONS` | Maximum agentic loop iterations | `10` |
| `TEMPERATURE` | Sampling temperature | `0.7` |

## Architecture

```
hermes-agent/
├── main.py              # Entry point
├── agent/
│   ├── core.py          # Core agent loop
│   ├── tools.py         # Tool definitions and registry
│   └── prompts.py       # System prompts and templates
├── utils/
│   ├── config.py        # Configuration management
│   └── logging.py       # Logging utilities
└── tests/
    └── ...              # Test suite
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/my-feature`)
3. Commit your changes
4. Open a Pull Request

Please use the issue templates in `.github/ISSUE_TEMPLATE/` to report bugs or request features.

## License

MIT License — see [LICENSE](LICENSE) for details.

## Acknowledgements

- [NousResearch](https://nousresearch.com/) for the original hermes-agent and Hermes model series
- The open-source AI community
