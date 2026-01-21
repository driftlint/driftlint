# DriftLinter - GitHub Action

**DriftLinter** is a powerful tool designed to detect API drift by comparing your Flask application routes against your OpenAPI 3.0 specification. It ensures your documentation stays in sync with your codebase.

This repository is a wrapper for the DriftLinter Docker image, allowing it to be easily integrated into your GitHub Actions workflows.

## Features

- 🔍 **Drift Detection**: Identifies missing, undocumented, or mismatched endpoints.
- 🤖 **AI-Powered Suggestions**: Automatically generates OpenAPI YAML for undocumented routes.
- ⚡ **Zero Setup**: Runs via Docker, no need to install Python dependencies in your runner.

## Quick Start

Add the `driftlinter` action to your workflow file (e.g., `.github/workflows/drift-check.yml`).

```yaml
name: API Drift Check

on: [push, pull_request]

jobs:
  driftlint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run DriftLinter
        uses: driftlint/driftlint@v1
        with:
          openai-api-key: ${{ secrets.OPENAI_API_KEY }} # Optional: For auto-suggestions
          spec-path: 'docs/openapi.yaml'
          app-file: 'app/main.py'
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `openai-api-key` | OpenAI API Key for AI suggestions. | Optional |
| `spec-path` | Path to your OpenAPI YAML file. | `openapi.yaml` |
| `app-file` | Path to your Flask application entry point. | `app.py` |

## How it Works

This action uses a pre-built Docker image hosted on GitHub Container Registry. It mounts your repository content and runs the DriftLinter analysis tool.

## License

This project is licensed under the [MIT License](LICENSE).
