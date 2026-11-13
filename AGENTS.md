# Project rules

These rules apply throughout this repository.

## Public repository and security

- Treat all repository content, commits, pull requests, and CI output as public. Never publish secrets, credentials, tokens, private keys, personal data, or other sensitive information.
- Use GitHub Actions secrets or an appropriate external secrets manager for sensitive values. Do not put sensitive values in Terraform configuration, state committed to Git, logs, or examples.
- If sensitive information is exposed, stop and report it; removing it from the latest commit alone does not remove it from history.

## Infrastructure and access

- Manage all infrastructure with Terraform, deployed through GitHub Actions. Make infrastructure changes in code and use the GitHub Actions workflow to apply them; do not make direct, out-of-band changes to infrastructure.
- GitHub and AWS access may be used to inspect the repository, workflows, and resources, and to trigger the appropriate GitHub Actions workflows when needed. Respect the available permissions and any required approvals.
- Verify existing configuration and resource state before making assumptions. Never expose sensitive values in output.

## Verification and pull requests

- Run the relevant tests and checks for each change. Report any checks that could not be run or that fail.
- All tests and required checks must pass before a pull request is merged. Never bypass, disable, or weaken checks to obtain a green result.

## Code and changes

- Keep code minimal, clean, and readable. Implement only what is needed; avoid speculative edge cases, unnecessary abstractions, dependencies, and comments that restate the code.
- Follow existing project conventions, keep changes focused, and avoid unrelated refactoring.
