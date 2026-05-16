## Justfile

Justfile is a modern command runner designed to simplify and streamline task
automation in software development. It serves as a user-friendly alternative to
traditional tools like Makefile, offering a cleaner syntax, better
cross-platform support, and enhanced developer experience.

Justfiles define tasks—called *recipes*—in a simple, readable format. These
recipes can run shell commands, scripts, or even integrate with other languages
like Python. The `just` command-line tool executes these recipes, making it easy
to standardize project workflows such as building, testing, deploying, or
running common scripts.

### Key Features of Justfile

1. **Clean, Readable Syntax**  
   Justfiles use space-based indentation (no tabs required), eliminating a major
   source of errors in Makefiles. Recipes are defined clearly and can include
   documentation comments.

   ```just
   # Build the project
   build:
       ./mvnw clean install

   # Run tests
   test:
       ./mvnw test
   ```

2. **Cross-Platform Compatibility**  
   Unlike Makefiles, which assume POSIX compliance and often fail on Windows,
   Just works natively across Linux, macOS, and Windows without additional
   tooling.

3. **Built-in Parameter Support**  
   Justfiles support arguments and default values directly:

   ```just
   deploy(env="staging"):
       echo "Deploying to {{env}}"
       kubectl apply -f deployment-{{env}}.yaml
   ```

   Run with: `just deploy production`

4. **Task Dependencies & Chaining**  
   Recipes can depend on others, enabling logical workflow sequencing:

   ```just
   release: build test deploy
   ```

5. **Environment and Variable Management**  
   Supports `.env` files, typed parameters, and built-in functions (e.g.,
   `os()`, `arch()`, `uuid4()`), improving consistency across environments.

6. **Improved Error Reporting**  
   Provides descriptive error messages with line numbers and context, reducing
   debugging time.

### Why Developers Prefer Just to Make

- **Easier Onboarding**: New contributors can run `just --list` to discover
  available tasks.
- **No Phantom Dependencies**: Just is not tied to file timestamps, avoiding
  unexpected rebuilds.
- **No `.PHONY` Targets Needed**: All recipes are treated as commands by
  default.
- **Shell Independence**: Works with bash, zsh, PowerShell, etc., without
  changes.
- **Modern DevOps Integration**: Ideal for CI/CD pipelines, with structured
  output and logging.

### Use Cases

- Automating build, test, and deployment scripts
- Standardizing developer environments
- Replacing ad-hoc shell scripts or complex Makefiles
- Managing infrastructure-as-code workflows (e.g., Terraform, Kubernetes)
- Running database migrations or seeding data

### Getting Started

Install `just` via package managers (e.g., `brew install just`,
`cargo install just`) or download from [just.systems](https://just.systems).

Create a `justfile` in your project root:

```just
# Default task
default: build

build:
    @echo "Building..."
    ./build.sh

test:
    @echo "Testing..."
    ./test.sh
```

Run with `just` (runs default) or `just test`.
