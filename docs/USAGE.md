# Usage

## Overview

This repository provides a reusable GitHub Actions workflow for Terraform-based infrastructure projects.
It simplifies the CI/CD workflow by automating Terraform validation and release processes using
containerized tools.

## Workflow Details

The `terraform.yml` workflow is a callable workflow that provides two jobs:

### Validate

Runs Terraform validation using a containerized environment:

-   **Container**: `martoc/terraform-tools:1.1.0`
-   **Runner**: `ubuntu-24.04`
-   **Command**: `make validate`

Your repository must include a `Makefile` with a `validate` target that runs the appropriate Terraform validation commands.

### Release

After successful validation, the workflow handles tagging and releasing:

-   Uses [martoc/action-tag](https://github.com/martoc/action-tag) for semantic versioning
-   Uses [martoc/action-release](https://github.com/martoc/action-release) for GitHub releases
-   Releases are only created on pushes to the main branch (not on pull requests)

## Example

Here is an example of how to use this workflow in your repository:

```yaml
name: Terraform

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  terraform:
    permissions:
      contents: write
    uses: martoc/workflow-infrastructure/.github/workflows/terraform.yml@v0
    secrets: inherit
```

## Requirements

Your repository must include:

1.  A `Makefile` with a `validate` target
2.  Valid Terraform configuration files

## Example Makefile

```makefile
.PHONY: validate

validate:
	terraform init -backend=false
	terraform validate
	terraform fmt -check
```
