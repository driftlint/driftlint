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

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `config` | Path to your driftlinter yaml configuration. | `.driftlinter.yml` |

## How it Works

This action uses a pre-built Docker image hosted on GitHub Container Registry. It mounts your repository content and runs the DriftLinter analysis tool.

## License

This project is licensed under the [MIT License](LICENSE).
