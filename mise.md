<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [mise](#mise)
  - [Overview and Purpose](#overview-and-purpose)
  - [Core Features](#core-features)
    - [Dev Tool Version Management](#dev-tool-version-management)
    - [Environment Variable Management](#environment-variable-management)
    - [Task Runner](#task-runner)
  - [Performance and Technical Advantages](#performance-and-technical-advantages)
  - [Comparison with Other Tools](#comparison-with-other-tools)
  - [Adoption and Community Reception](#adoption-and-community-reception)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# mise  

## Overview and Purpose  

Mise, short for *mise-en-place* (pronounced "meez"), is a modern, **Rust-based
development environment tool** designed to unify and simplify how developers
manage their toolchains, environments, and workflows. Inspired by the French
culinary term meaning "everything in its place," Mise aims to prepare a
developer’s environment automatically before coding begins.

Originally known as *rtx*, it was rebranded to Mise to reflect its broader scope
beyond just runtime management. Created by Jared Forsyth (also known as jdx), it
acts as a **"front-end to your dev environment"**, handling multiple aspects of
local development from a single configuration file—typically `mise.toml`.

## Core Features  

### Dev Tool Version Management  

Mise serves as a **polyglot version manager**, capable of managing multiple
language runtimes and CLI tools such as Node.js, Python, Ruby, Go, Terraform,
and hundreds more. It supports both **project-specific** and **global** tool
versions.

It reads configuration files like `.tool-versions` (compatible with asdf),
`.node-version`, or its native `mise.toml`, allowing seamless migration from
existing tools.

```toml
[tools]
node = "20"
python = "3.11"
ruby = "3.2"
```

When you enter a project directory, Mise **automatically switches** to the
correct versions, eliminating "works on my machine" issues.

### Environment Variable Management

Beyond tools, Mise manages **project-specific environment variables**, replacing
tools like direnv. Variables can be defined directly in `mise.toml` or loaded
from `.env` files.

```toml
[env]
DATABASE_URL = "postgres://localhost/myapp_dev"
API_KEY = { value = "secret", redact = true }
```

These variables are **automatically loaded and unloaded** as you navigate
between projects, keeping your shell clean and secure.

### Task Runner

Mise includes a built-in **task runner** similar to `make` or npm scripts, but
with better integration. Tasks are defined in the `[tasks]` section of
`mise.toml` and have full access to managed tools and environment variables.

```toml
[tasks.serve]
run = "npm run dev"

[tasks.test]
run = "npm test"
```

You can run them with `mise run serve`. Tasks support **dependencies** and *
*composition**, enabling complex workflows.

## Performance and Technical Advantages

Built in **Rust**, Mise is **significantly faster** than shell-based tools like
asdf, nvm, or rbenv. It minimizes shell startup overhead and avoids the latency
caused by sourcing multiple shell scripts.

Its **single compiled binary** ensures consistent behavior across
platforms—macOS, Linux, and Windows (via WSL). It modifies the `PATH`
environment variable directly, pointing to **real binaries** rather than shims,
improving reliability.

Mise also supports **plugin backends** (like asdf, npm, cargo) while maintaining
performance through efficient internal handling.

## Comparison with Other Tools

| Tool      | Scope                                   | Performance            | Configuration       | Key Difference                        |
|-----------|-----------------------------------------|------------------------|---------------------|---------------------------------------|
| asdf      | Polyglot version manager                | Slower (shell scripts) | `.tool-versions`    | Mise is faster, adds env vars & tasks |
| nvm/pyenv | Language-specific                       | Moderate               | Dotfiles (`.nvmrc`) | Mise unifies all in one tool          |
| Nix       | Full system/environment reproducibility | Heavy                  | Nix language        | Mise is lighter, developer-focused    |
| direnv    | Env var loading                         | Fast                   | `.envrc`            | Mise integrates this natively         |

Mise is often seen as a **spiritual successor to asdf**, offering better speed,
richer configuration (TOML), and broader functionality.

## Adoption and Community Reception

Mise has gained rapid traction among developers managing **multi-language
projects** or working in teams where environment consistency is critical. Its *
*developer ergonomics**, speed, and unified interface have made it a favorite in
the DevOps and full-stack communities.

It’s actively maintained on GitHub, with regular updates and a growing plugin
ecosystem. Many developers report switching from asdf, rvm, or nodenv due to
Mise's simplicity and reliability.

While not yet as widespread as some legacy tools, its **adoption is growing**,
especially in CI/CD pipelines and modern monorepo setups.
