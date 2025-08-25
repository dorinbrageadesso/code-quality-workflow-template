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
    uses: org/code-quality-workflow-template/.github/workflows/build.yml@v1

  spotless:
    needs: build
    uses: org/code-quality-workflow-template/.github/workflows/spotless.yml@v1

  checkstyle:
    needs: spotless
    uses: org/code-quality-workflow-template/.github/workflows/checkstyle.yml@v1

  pmd:
    needs: checkstyle
    uses: org/code-quality-workflow-template/.github/workflows/pmd.yml@v1

  tests:
    needs: pmd
    uses: org/code-quality-workflow-template/.github/workflows/tests.yml@v1
```

## Project Configuration

Your repo should include:
- `pom.xml` (with plugins for Spotless, Checkstyle, PMD, JaCoCo)
- `.editorconfig`
- `checkstyle.xml`

See [the template repo docs](./) for example configs.

## Updating

To use updates, bump the ref (`@v1`, `@main`, etc.) in your workflow file.
