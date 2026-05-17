<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [DevPod](#devpod)
- [Key Features and Advantages](#key-features-and-advantages)
  - [Open-Source & No Vendor Lock-In](#open-source--no-vendor-lock-in)
  - [Cost Efficiency](#cost-efficiency)
  - [Cross-IDE Support](#cross-ide-support)
  - [Infrastructure Flexibility](#infrastructure-flexibility)
  - [Client-Only Architecture](#client-only-architecture)
- [How DevPod Works](#how-devpod-works)
- [Use Cases and Adoption](#use-cases-and-adoption)
  - [Rapid Onboarding](#rapid-onboarding)
  - [Secure Remote Development](#secure-remote-development)
  - [Dev-Environments-as-Code](#dev-environments-as-code)
  - [Hybrid Development Workflows](#hybrid-development-workflows)
- [Getting Started with DevPod](#getting-started-with-devpod)
  - [Installation](#installation)
  - [Create a Workspace](#create-a-workspace)
  - [Supported Providers](#supported-providers)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## DevPod

DevPod is an **open-source, client-only tool** designed to create 
**reproducible, containerized development environments** using the DevContainer
standard (`devcontainer.json`). It allows developers to define their entire
development environment as code, ensuring consistency across teams and
eliminating the traditional "works on my machine" problem.

Unlike managed services such as GitHub Codespaces or JetBrains Spaces, DevPod
gives full control over where environments are hosted—whether on **local
machines, remote servers, Kubernetes clusters**, or any public cloud (e.g., AWS,
GCP, Azure).

## Key Features and Advantages

### Open-Source & No Vendor Lock-In

DevPod is **100% open-source** and unopinionated, meaning you're not tied to a
specific cloud provider or IDE. You can switch providers or infrastructure with
a single command.

### Cost Efficiency

DevPod is typically **5–10 times cheaper** than hosted alternatives because it
uses bare virtual machines and supports **automatic shutdown of inactive
environments**.

### Cross-IDE Support

It natively supports VS Code and the full JetBrains suite (IntelliJ, PyCharm,
etc.), while other IDEs can connect via SSH.

### Infrastructure Flexibility

You can run DevPod workspaces on:

- Local Docker (e.g., Docker Desktop, OrbStack)
- Remote machines via SSH
- Kubernetes clusters
- Cloud VMs (AWS, GCP, Azure)

### Client-Only Architecture

No server backend is required—DevPod runs entirely on your local machine,
reducing operational overhead.

## How DevPod Works

DevPod uses a **provider model** to launch development environments. A *
*provider** defines where the containerized workspace runs (e.g., local Docker,
GCP, Kubernetes). Once configured, DevPod spins up a container based on the
`devcontainer.json` file in your project, which specifies:

- Base image
- Required tools, libraries, and runtimes
- IDE settings
- Prebuild configurations

The developer connects to this environment from their local IDE using remote
development extensions (e.g., VS Code Remote - Containers), creating a seamless
coding experience regardless of where the environment is hosted.

Each **workspace** is isolated, ephemeral, and reproducible—ensuring that every
team member works in an identical setup.

## Use Cases and Adoption

### Rapid Onboarding

Teams at companies like ThoughtSpot and Uber use DevPod to **reduce onboarding
time from days to minutes**, especially for complex monorepos requiring multiple
services (databases, message brokers, etc.).

### Secure Remote Development

Organizations use DevPod to enforce **secure, standardized environments**
running on company-controlled infrastructure, avoiding sensitive code on
personal laptops.

### Dev-Environments-as-Code

By treating development environments as infrastructure-as-code, SREs and
platform engineers ensure **consistency, version control, and automation**,
aligning dev environments with production.

### Hybrid Development Workflows

Developers can **switch seamlessly between local and cloud-powered environments
**, using lightweight laptops for editing while offloading heavy builds and
tests to powerful remote machines.

## Getting Started with DevPod

### Installation

DevPod can be installed via CLI or desktop app:

```bash
brew install devpod  # macOS
# or download from https://devpod.sh
```

### Create a Workspace

```bash
devpod up --ide=intellij https://github.com/example/project
```

This command:

1. Clones the repo
2. Reads `devcontainer.json`
3. Spins up a container on your chosen provider
4. Connects your local IDE

### Supported Providers

- Docker (local)
- SSH
- Kubernetes
- AWS EC2
- Google Cloud
- Azure VM
