[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# workflow-infrastructure

Reusable GitHub Actions workflows for infrastructure projects. Provides standardised validation and release processes for Terraform and CloudFormation using containerised tools.

## Features

- Terraform validation workflow with containerised tools
- CloudFormation validation workflow with cfn-lint
- Automatic semantic versioning with `action-tag`
- GitHub release creation with `action-release`
- Make-based initialisation and validation

## Quick Start

### Terraform Workflow

```yaml
name: Terraform

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  terraform:
    permissions:
      contents: write
    uses: martoc/workflow-infrastructure/.github/workflows/terraform.yml@v0
    secrets: inherit
```

### CloudFormation Workflow

```yaml
name: CloudFormation

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  cloudformation:
    permissions:
      contents: write
    uses: martoc/workflow-infrastructure/.github/workflows/cloudformation.yml@v0
    secrets: inherit
```

## Prerequisites

Your repository must have a `Makefile` with `init` and `validate` targets:

```makefile
.PHONY: init validate

init:
	terraform init -backend=false

validate:
	terraform validate
	terraform fmt -check
```

## Documentation

- [Usage Guide](./docs/USAGE.md) - Detailed usage instructions and examples
- [Code Style](./docs/CODESTYLE.md) - Code style guidelines for contributors

## Available Workflows

| Workflow | Description |
|----------|-------------|
| `terraform.yml` | Terraform validation and release workflow |
| `cloudformation.yml` | CloudFormation validation and release workflow |

## Licence

This project is licenced under the MIT Licence - see the [LICENCE](LICENSE) file for details.
