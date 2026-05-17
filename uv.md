<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [uv](#uv)
- [Key Features](#key-features)
  - [Blazing Fast Performance](#blazing-fast-performance)
  - [All-in-One Tool](#all-in-one-tool)
  - [Comprehensive Project Management](#comprehensive-project-management)
  - [Advanced Capabilities](#advanced-capabilities)
- [Installation](#installation)
- [Basic Usage](#basic-usage)
- [Comparison with Other Tools](#comparison-with-other-tools)
- [Getting Started Resources](#getting-started-resources)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## uv

Uv is a modern, high-performance Python package and project manager developed by
Astral, the team behind Ruff, a popular Python linter. Written in Rust, `uv` is
designed to unify and replace multiple traditional Python tools—including `pip`,
`pip-tools`, `virtualenv`, `pyenv`, `pipx`, and parts of `poetry`—into a single,
fast, and reliable command-line interface.

It aims to solve long-standing issues in Python development such as slow
dependency resolution, complex environment management, and fragmented tooling.

## Key Features

### Blazing Fast Performance

`uv` is **10–100x faster** than `pip`, especially in cold and warm cache
scenarios. This speed comes from:

- **Rust implementation** for low-level performance
- **Parallel downloads** and dependency resolution
- **Aggressive caching** with a global module cache
- **Copy-on-Write (CoW)** and hardlinks to reduce disk usage

For example, virtual environment creation is up to **80x faster** than
`python -m venv`.

### All-in-One Tool

`uv` consolidates functionality from multiple tools:

| Functionality             | Replaces                    |
|---------------------------|-----------------------------|
| Package installation      | `pip`                       |
| Dependency locking        | `pip-tools` (`pip-compile`) |
| Virtual environments      | `virtualenv`, `venv`        |
| Python version management | `pyenv`                     |
| CLI tool execution        | `pipx`                      |
| Project scaffolding       | `poetry init`-like features |

This reduces toolchain complexity and configuration overhead.

### Comprehensive Project Management

`uv` supports modern Python workflows:

- `uv init`: Scaffold new projects with `pyproject.toml`, `.git`, and `.venv`
- `uv add package`: Add dependencies (like `npm install`)
- `uv run script.py`: Run scripts in isolated environments (no manual
  activation)
- `uv lock` / `uv sync`: Generate and apply lockfiles (`uv.lock`) for
  reproducibility
- `uv python install 3.11`: Install and manage multiple Python versions
- `uvx black`: Run CLI tools in ephemeral environments (like `npx`)

### Advanced Capabilities

- **Platform-independent resolution**: Resolve dependencies for different Python
  versions or platforms
- **Dependency overrides**: Fix version conflicts by overriding transitive
  dependencies
- **Universal lockfiles**: `uv.lock` ensures consistent environments across OSes
- **Script-level dependencies**: Manage deps for standalone scripts using PEP
  723-style metadata
- **Ephemeral tool execution**: Use `uvx` to run tools like `ruff` or `black`
  without installing them globally

## Installation

The recommended method uses the standalone installer (doesn't require Python):

```bash
# Linux/macOS
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Alternatively, install via `pip` or `pipx`:

```bash
pip install uv
```

## Basic Usage

```bash
# Initialize a new project
uv init myproject
cd myproject

# Add dependencies
uv add requests pandas

# Run a script in the project environment
uv run main.py

# Install and use a specific Python version
uv python install 3.11
uv python pin 3.11

# Run a CLI tool temporarily
uvx black --check .
```

## Comparison with Other Tools

| Feature                   | `uv`                  | `pip` + `venv`               | `poetry`                     | `conda`           |
|---------------------------|-----------------------|------------------------------|------------------------------|-------------------|
| Speed                     | 10–100x faster        | Baseline                     | Faster than pip              | Slower            |
| Language                  | Rust                  | Python                       | Python                       | Python            |
| Virtual env management    | Built-in              | Manual                       | Built-in                     | Built-in          |
| Python version management | Built-in              | No                           | Partial                      | Built-in          |
| Lockfile                  | `uv.lock` (universal) | `requirements.txt` (no lock) | `poetry.lock` (per platform) | `environment.yml` |
| Non-Python packages       | No                    | No                           | No                           | Yes               |
| CLI tool execution        | `uvx`                 | No                           | `poetry run`                 | `conda run`       |

## Getting Started Resources

- [Official `uv` Documentation](https://docs.astral.sh/uv/)
- [Migrating from `pip` or `poetry`](https://docs.astral.sh/uv/migration/)
- [GitHub Repository](https://github.com/astral-sh/uv)
