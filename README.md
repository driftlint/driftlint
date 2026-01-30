# DriftLinter - GitHub Action

> **Stop lying to your frontend team.**
> The only CI tool that guarantees your implementation matches your OpenAPI specification.

**DriftLinter** is a governance tool for modern engineering teams. It runs in your GitHub Actions pipeline to detect "API Drift"—the moment your code diverges from your documentation.

**Demo Repository** https://github.com/driftlint/driftlint-demo/pull/2

---


## ⚡ The Problem
You add a new route, change a parameter, or deprecate an endpoint in code, but you forget to update `openapi.yaml`.

1.  ❌ **Frontend Breaks:** Clients ship bugs based on outdated docs.
2.  ❌ **Compliance Fails:** Your published API catalog is incorrect.
3.  ❌ **AI Hallucinates:** Internal AI agents (RAG/Co-pilots) fail because they rely on broken specs.

## ✅ The Solution
DriftLinter performs static analysis on your codebase and compares it against your OpenAPI 3.0+ definition.

## 🚀 Features

### 🔍 Precision Governance
*   **Missing Routes:** Detects endpoints that exist in your source code but are missing from the OpenAPI spec.
*   **Zombie Routes:** Identifies endpoints defined in the spec that have been deleted from the codebase.
*   **Schema Validation:** Verifies that query parameters, request bodies, and HTTP methods match the implementation.

### 🛠️ Polyglot Support
DriftLinter is built for modern, multi-language stacks.

| Language | Frameworks Supported | Release |
| :--- | :--- | :--- |
| **Python** | Flask, FastAPI, Django (WIP) | Production Ready |
| **TypeScript/JS** | Express, NestJS, Fastify | Beta |
| **PHP** | Laravel, Symfony | Beta |

### 🧠 Agentic AI (Beta)
*   **Auto-Fix Suggestions:** Don't just fail the build. DriftLinter analyzes the code logic and provides the exact YAML snippet needed to fix the drift.
*   **Privacy-First Architecture:** The analysis engine runs locally. For enterprise users, you can connect it to your internal LLM gateway so no code leaves your perimeter.

---

## 🔮 The Vision: API-Agent Interoperability

### 🔌 Verified MCP Generation (Coming Soon)
Because DriftLinter mathematically validates that your Code matches your Spec, it is uniquely positioned to bridge the gap to AI.
*   **The Feature:** We are building a native engine to compile your validated OpenAPI specs into **Model Context Protocol (MCP)** servers.
*   **The Result:** Instantly turn your internal API into a reliable toolset for **Claude Desktop**, **Cursor**, and **Windsurf**—with zero hallucinations.

### 🧠 Intelligent Governance

Self-Healing Specifications. Our goal is to create a system where documentation maintains itself, ensuring your APIs are robust enough for the next generation of autonomous development.
 
---


## Quick Start

Add the `driftlinter` action to your workflow file (e.g., `.github/workflows/drift-check.yml`).

```yaml
name: API Drift Check

on: [pull_request]

jobs:
  driftlint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run DriftLinter
        uses: driftlint/driftlint@v0.0.2
        with:
          config: 'path/to/.driftlinter.yml'
```

Add the .driftlinter.yml file to your root directory
```yaml
# .driftlinter.yml
version: 1
projects:
  - name: "Python Service"
    source_dir: "src/api/flask"          # Where the code lives
    spec_file: "src/api/flask/openapi.yaml"   # Where the spec lives
    language: "python"                        # python, typescript, php

  - name: "Payments Service"
    source_dir: "services/payments/src"
    spec_file: "shared/specs/payments-v1.yaml"
    language: "typescript"
```

## 🏢 Enterprise: Governance & Security

### 🔒 Zero Data Exfiltration
*   **Local Execution:** The DriftLinter container runs entirely inside your self-hosted or private GitHub Runners.

### 🔑 Bring Your Own Key (BYOK) (Coming Soon)
*   **Direct Connection:** You provide the API keys via GitHub Secrets. The tool connects directly from your runner to your AI provider.
*   **Secret Rotation:** Easily rotate keys within GitHub without updating the DriftLinter configuration.

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `config` | Path to your driftlinter yaml configuration. | `.driftlinter.yml` |

## How it Works

This action uses a pre-built Docker image hosted on GitHub Container Registry. It mounts your repository content and runs the DriftLinter analysis tool.

## License

This project is licensed under the [MIT License](LICENSE).
