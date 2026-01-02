# Code Style

## General Formatting

We use an `.editorconfig` file to enforce consistent code style across the project. Visit [editorconfig.org](https://editorconfig.org) for more information.

### Key Guidelines

- Use 2 spaces for indentation in YAML files
- Avoid trailing whitespace
- Ensure files end with a newline

## YAML Formatting

Workflow files should be formatted consistently following GitHub Actions best practices.

- Use lowercase for keys
- Use descriptive names for jobs and steps
- Use proper YAML syntax

## Terraform Formatting

- Use `terraform fmt` to format Terraform files
- Follow the [Terraform Style Guide](https://developer.hashicorp.com/terraform/language/style)

## CloudFormation Formatting

- Use `cfn-lint` for CloudFormation template validation
- Follow AWS CloudFormation best practices

## Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation changes
- `chore:` for maintenance tasks

## Pull Requests

- Create feature branches from `main`
- Use descriptive branch names: `feat/description`, `fix/description`
- Ensure all CI checks pass before requesting review
