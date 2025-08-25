# Code Quality Workflow Template

Reusable GitHub Actions workflows for Java/Maven projects.

## Usage

In your repo's `.github/workflows/code-quality.yml`:

```yaml
name: Code Quality

on:
  push:
    branches: [ 'feature/**' ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    uses: WITT-GCP-PLATFORM/log-code-quality-workflow-template/.github/workflows/build.yml@main

  spotless:
    needs: build
    uses: WITT-GCP-PLATFORM/log-code-quality-workflow-template/.github/workflows/spotless.yml@main

  checkstyle:
    needs: spotless
    uses: WITT-GCP-PLATFORM/log-code-quality-workflow-template/.github/workflows/checkstyle.yml@main

  pmd:
    needs: checkstyle
    uses: WITT-GCP-PLATFORM/log-code-quality-workflow-template/.github/workflows/pmd.yml@main

  tests:
    needs: pmd
    uses: WITT-GCP-PLATFORM/log-code-quality-workflow-template/.github/workflows/tests.yml@main
```

## Project Configuration

Your repo should include:
- `pom.xml` (with plugins for Spotless, Checkstyle, PMD, JaCoCo)
- `.editorconfig`
- `checkstyle.xml`

See [the template repo docs](./) for example configs.

## Updating

To use updates, bump the ref (`@main`, `@main`, etc.) in your workflow file.
