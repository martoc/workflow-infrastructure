# Usage

## Overview

This repository provides reusable GitHub Actions workflows for infrastructure projects.
It simplifies the CI/CD workflow by automating validation and release processes using
containerised tools.

## Available Workflows

-   [Terraform](#terraform)
-   [CloudFormation](#cloudformation)

## Terraform

The `terraform.yml` workflow is a callable workflow for Terraform-based infrastructure projects.

### Workflow Details

#### Init

Initialises the Terraform environment:

-   **Container**: `martoc/terraform-tools:1.1.0`
-   **Runner**: `ubuntu-24.04`
-   **Command**: `make init`

#### Validate

Runs Terraform validation using a containerised environment:

-   **Container**: `martoc/terraform-tools:1.1.0`
-   **Runner**: `ubuntu-24.04`
-   **Command**: `make validate`

#### Release

After successful validation, the workflow handles tagging and releasing:

-   Uses [martoc/action-tag](https://github.com/martoc/action-tag) for semantic versioning
-   Uses [martoc/action-release](https://github.com/martoc/action-release) for GitHub releases
-   Releases are only created on pushes to the main branch (not on pull requests)

### Example

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

### Requirements

Your repository must include:

1.  A `Makefile` with `init` and `validate` targets
2.  Valid Terraform configuration files

### Example Makefile

```makefile
.PHONY: init validate

init:
	terraform init -backend=false

validate:
	terraform validate
	terraform fmt -check
```

## CloudFormation

The `cloudformation.yml` workflow is a callable workflow for CloudFormation-based infrastructure projects.

### Workflow Details

#### Init

Initialises the CloudFormation environment:

-   **Container**: `martoc/cloudformation-tools:0.2.89`
-   **Runner**: `ubuntu-24.04`
-   **Command**: `make init`

#### Validate

Runs CloudFormation validation using a containerised environment:

-   **Container**: `martoc/cloudformation-tools:0.2.89`
-   **Runner**: `ubuntu-24.04`
-   **Command**: `make validate`

#### Release

After successful validation, the workflow handles tagging and releasing:

-   Uses [martoc/action-tag](https://github.com/martoc/action-tag) for semantic versioning
-   Uses [martoc/action-release](https://github.com/martoc/action-release) for GitHub releases
-   Releases are only created on pushes to the main branch (not on pull requests)

### Example

```yaml
name: CloudFormation

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  cloudformation:
    permissions:
      contents: write
    uses: martoc/workflow-infrastructure/.github/workflows/cloudformation.yml@v0
    secrets: inherit
```

### Requirements

Your repository must include:

1.  A `Makefile` with `init` and `validate` targets
2.  Valid CloudFormation template files

### Example Makefile

```makefile
.PHONY: init validate

init:
	@echo "Initialising CloudFormation environment"

validate:
	cfn-lint **/*.yaml
	aws cloudformation validate-template --template-body file://template.yaml
```
