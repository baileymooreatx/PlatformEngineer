## GitHub Actions

GitHub Actions is a powerful **CI/CD and automation platform** built directly
into GitHub, allowing you to automate your software development workflows such
as building, testing, and deploying code. It uses **YAML files** stored in your
repository (in the `.github/workflows` directory) to define workflows that run
based on events like `push`, `pull_request`, or a scheduled time.

You can automate repetitive tasks—like running tests, assigning issue labels, or
deploying to the cloud—without leaving GitHub. Workflows run on **virtual
machines (runners)** provided by GitHub for Linux, Windows, or macOS.

## Key Concepts

Understanding the core components of GitHub Actions is essential for building
effective workflows.

1. **Workflows**
    - Automated processes that run one or more jobs.
    - Defined in `.yml` files inside `.github/workflows`.
    - Triggered by **events** (e.g., `push`, `pull_request`, `issues`, or
      `schedule`).

2. **Events**
    - Specific activities in a repository that trigger a workflow.
    - Common events: `push`, `pull_request`, `release`, `issues`,
      `workflow_dispatch` (manual trigger).

3. **Jobs**
    - A set of steps that execute on the same **runner** (virtual machine).
    - Jobs run **in parallel** by default but can be set to run sequentially
      using `needs`.

4. **Steps**
    - Individual tasks within a job.
    - Can run shell commands (`run`) or use prebuilt actions (`uses`) from the
      GitHub Marketplace.

5. **Runners**
    - Virtual machines that execute your jobs.
    - GitHub provides **hosted runners** (`ubuntu-latest`, `windows-latest`,
      `macos-latest`), or you can use **self-hosted runners**.

6. **Actions**
    - Reusable units of code that perform specific tasks.
    - Can be **community-built** (from Marketplace) or **custom-built** (
      JavaScript, Docker, or composite).

7. **GitHub Marketplace**
    - A public directory of prebuilt actions you can use in your workflows.
    - Examples: `actions/checkout@v4`, `actions/setup-node@v4`,
      `aws-actions/configure-aws-credentials`.

## Step-by-Step Guide to Creating Your First Workflow

### Prerequisites

- A GitHub account.
- Basic knowledge of Git and repositories.
- Familiarity with YAML syntax (optional but helpful).

### Step-by-step instructions

1. **Navigate to your GitHub repository**
    - Go to the repo where you want to add automation.

2. **Create the workflows directory**
    - In your repo, create a folder named `.github/workflows` at the root level.

3. **Create a new workflow file**
    - Inside `.github/workflows`, create a file like `hello-world.yml`.

4. **Define the workflow in YAML**
    - Paste the following code:

```yaml
name: Hello World Workflow
on: [ push ]
jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Print greeting
        run: echo "Hello, GitHub Actions!"
```

5. **Commit the file**
    - Save and commit the file directly on GitHub or via your IDE.

6. **Trigger the workflow**
    - Push a change to the repository to trigger the `push` event.

7. **View the workflow run**
    - Go to the **Actions** tab in your repo.
    - Click on the workflow to see logs and step-by-step output.

You’ll see “Hello, GitHub Actions!” printed in the logs—your first successful
run!

## Best Practices and Tips

- **Use descriptive names** for workflows and jobs (e.g., `build-and-test.yml`).
- **Specify event types** to avoid unnecessary runs:
  ```yaml
  on:
    pull_request:
      types: [opened, reopened]
      branches: [main]
  ```
- **Use environment variables and secrets** for sensitive data:
  ```yaml
  env:
    API_KEY: ${{ secrets.API_KEY }}
  ```
- **Reuse actions** from the Marketplace to save time.
- **Test workflows** on a branch before merging to `main`.
- **Enable concurrency** to prevent multiple runs from queuing:
  ```yaml
  concurrency: ci-${{ github.ref }}
  ```
- **Use caching** to speed up jobs (e.g., for Node.js `node_modules`).

## Further Learning Resources

- [Complete GitHub Actions Course - From BEGINNER to PRO](https://www.youtube.com/watch?v=Xwpi0ITkL3U)
- [GitHub Docs: Understanding GitHub Actions](https://docs.github.com/articles/getting-started-with-github-actions)
- [freeCodeCamp: Learn GitHub Actions Step-by-Step](https://www.freecodecamp.org/news/learn-to-use-github-actions-step-by-step-guide/)
- [Microsoft Learn: Introduction to GitHub Actions](https://learn.microsoft.com/en-us/training/modules/introduction-to-github-actions/)
- [GitHub Blog: Getting Started with GitHub Actions](https://github.blog/developer-skills/github/github-for-beginners-getting-started-with-github-actions/)
