# 🚀 GitHub Actions: Job Execution and Coordination

This repository demonstrates how to manage job dependencies and execution order in GitHub Actions.

## ⚡ Parallel Execution (Default)
By default, all jobs run simultaneously on separate runners.

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Linting..."
  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Testing..."
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Scanning..."
```

## ⛓️ Sequential Execution (With Dependencies)
Use the `needs` keyword to force jobs to wait for previous ones to finish.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  test:
    needs: build # Waits for build to complete
    runs-on: ubuntu-latest

  deploy:
    needs: [build, test] # Waits for both jobs
    runs-on: ubuntu-latest
```
