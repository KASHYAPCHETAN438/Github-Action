# GitHub Actions Keywords Notes

## 1. `name`

### Theory

* Defines the name of the workflow.
* Displayed in the GitHub Actions tab.
* Helps identify the workflow easily.

### Example

```yaml
name: Java CI Pipeline
```

### Key Points

* Workflow-level keyword.
* Optional but recommended.
* Improves readability.

---

## 2. `run-name`

### Theory

* Defines a custom name for each workflow execution.
* Makes workflow runs easier to identify.
* Can use GitHub expressions.

### Example

```yaml
run-name: Build by ${{ github.actor }}
```

### Key Points

* Supports expressions.
* Useful for tracking executions.
* Displayed in workflow run history.

---

## 3. `on`

### Theory

* Defines the event that triggers the workflow.
* Workflow starts only when the specified event occurs.
* Supports single or multiple triggers.

### Example

```yaml
on: push
```

### Key Points

* Trigger keyword.
* Required for automation.
* Supports multiple events.

---

## 4. `push`

### Theory

* Triggers workflow when code is pushed.
* Commonly used for Continuous Integration (CI).
* Executes after a commit is pushed.

### Example

```yaml
on:
  push:
```

### Key Points

* Most commonly used trigger.
* Useful for CI pipelines.
* Supports branch and path filters.

---

## 5. `pull_request`

### Theory

* Triggers workflow when a pull request is created or updated.
* Used to validate code before merging.
* Helps maintain code quality.

### Example

```yaml
on:
  pull_request:
```

### Key Points

* Common in team projects.
* Used for code review validation.
* Supports branch filters.

---

## 6. `branches`

### Theory

* Restricts workflow execution to specific branches.
* Prevents workflows from running on every branch.
* Used with push and pull_request events.

### Example

```yaml
on:
  push:
    branches:
      - main
```

### Key Points

* Branch filtering.
* Saves execution time.
* Supports wildcard patterns.

---

## 7. `paths`

### Theory

* Runs workflow only when specific files or folders change.
* Avoids unnecessary workflow executions.
* Useful for large repositories.

### Example

```yaml
on:
  push:
    paths:
      - 'src/**'
```

### Key Points

* File-based filtering.
* Improves efficiency.
* Supports wildcard matching.

---

## 8. `schedule`

### Theory

* Executes workflows automatically at scheduled times.
* Uses cron expressions.
* Suitable for recurring tasks.

### Example

```yaml
on:
  schedule:
    - cron: '0 9 * * *'
```

### Key Points

* Time-based execution.
* Uses UTC time.
* Ideal for reports and backups.

---

## 9. `env`

### Theory

* Stores environment variables.
* Variables can be reused throughout the workflow.
* Reduces duplicate values.

### Example

```yaml
env:
  JAVA_VERSION: 17
```

### Key Points

* Global variable storage.
* Avoids hardcoding.
* Improves maintainability.

---

## 10. `permissions`

### Theory

* Controls access rights of the GITHUB_TOKEN.
* Defines what the workflow can access.
* Improves workflow security.

### Example

```yaml
permissions:
  contents: read
```

### Key Points

* Security feature.
* Supports read/write access.
* Follow least privilege principle.

---

## 11. `jobs`

### Theory

* Defines the main tasks of the workflow.
* A workflow can contain multiple jobs.
* Jobs run independently.

### Example

```yaml
jobs:
  build:
```

### Key Points

* Core workflow component.
* Multiple jobs supported.
* Parallel execution by default.

---

## 12. `needs`

### Theory

* Creates dependencies between jobs.
* Ensures jobs run in a specific sequence.
* Useful in CI/CD pipelines.

### Example

```yaml
test:
  needs: build
```

### Key Points

* Sequential execution.
* Job dependency management.
* Prevents premature execution.

---

## 13. `if`

### Theory

* Executes jobs or steps only when a condition is true.
* Supports GitHub expressions.
* Enables dynamic workflows.

### Example

```yaml
if: github.ref == 'refs/heads/main'
```

### Key Points

* Conditional execution.
* Supports logical operators.
* Reduces unnecessary runs.

---

## 14. `runs-on`

### Theory

* Specifies the runner environment.
* Determines where the workflow executes.
* Can use Linux, Windows, or macOS.

### Example

```yaml
runs-on: ubuntu-latest
```

### Key Points

* Runner selection.
* Required for every job.
* Supports self-hosted runners.

---

## 15. `steps`

### Theory

* Represents individual tasks inside a job.
* Jobs consist of one or more steps.
* Executed sequentially.

### Example

```yaml
steps:
```

### Key Points

* Smallest execution unit.
* Sequential execution.
* Contains `uses` and `run`.

---

## 16. `uses`

### Theory

* References a reusable GitHub Action.
* Allows using pre-built functionality.
* Reduces development effort.

### Example

```yaml
- uses: actions/checkout@v4
```

### Key Points

* Reusable component.
* Marketplace integration.
* Saves time.

---

## 17. `run`

### Theory

* Executes shell commands directly on the runner.
* Used for build, test, and deployment tasks.
* Supports multiple shells.

### Example

```yaml
- run: mvn clean install
```

### Key Points

* Executes commands.
* Supports Bash, CMD, and PowerShell.
* Commonly used in CI/CD.

---

# Complete Workflow Example

```yaml
name: Java CI Pipeline

run-name: Build by ${{ github.actor }}

on:
  push:
    branches:
      - main
    paths:
      - 'src/**'

env:
  JAVA_VERSION: 17

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - run: java --version

      - run: mvn clean install
```

# GitHub Actions Hierarchy

```text
Workflow
│
├── name
├── run-name
├── on
│   ├── push
│   ├── pull_request
│   ├── branches
│   ├── paths
│   └── schedule
│
├── env
├── permissions
│
└── jobs
     │
     ├── needs
     ├── if
     ├── runs-on
     │
     └── steps
          ├── uses
          └── run
```

# Quick Interview Revision

| Keyword        | Purpose                 |
| -------------- | ----------------------- |
| `name`         | Workflow Name           |
| `run-name`     | Workflow Run Name       |
| `on`           | Workflow Trigger        |
| `push`         | Trigger on Push         |
| `pull_request` | Trigger on Pull Request |
| `branches`     | Branch Filter           |
| `paths`        | File Filter             |
| `schedule`     | Time-Based Trigger      |
| `env`          | Environment Variables   |
| `permissions`  | Access Control          |
| `jobs`         | Main Tasks              |
| `needs`        | Job Dependency          |
| `if`           | Conditional Execution   |
| `runs-on`      | Runner Environment      |
| `steps`        | Individual Tasks        |
| `uses`         | Reusable Action         |
| `run`          | Execute Commands        |

```
```
