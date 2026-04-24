# AI-universal-workflow

Universal GitHub Actions workflow template that you can import into any project and edit with your own commands.

## Workflow Included

- `.github/workflows/universal-project-workflow.yml`
  - Supports both reusable (`workflow_call`) and manual (`workflow_dispatch`) usage.
  - Optional Node.js and Python setup.
  - Configurable install, lint, test, build commands.
  - Optional build artifact upload.
  - Input validation to fail fast when required commands are missing.

## How to Use in Another Repository

Create a workflow file in your target repository (for example `.github/workflows/ci.yml`) and call this reusable workflow:

```yaml
name: Project CI

on:
  push:
    branches: [main]
  pull_request:

jobs:
  ci:
    uses: Sanvith6/AI-universal-workflow/.github/workflows/universal-project-workflow.yml@main
    with:
      runs_on: ubuntu-latest
      working_directory: .
      node_version: "20"
      install_command: npm ci
      run_lint: true
      lint_command: npm run lint
      run_test: true
      test_command: npm test
      run_build: true
      build_command: npm run build
      artifact_path: dist
      artifact_name: app-build
```

Then edit the `with:` values for your own project stack and commands.
