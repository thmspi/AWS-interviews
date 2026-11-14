# AWS-interviews
A private, voice-based simulator for AWS Solutions Architect interviews in France.

See [SPEC.md](SPEC.md) for the v1 product and technical specification.

## CI and Terraform foundation

Pull requests run Terraform format, validation, Checkov, and GitHub Actions syntax checks without AWS access. The application Terraform root is `infra/`, with separate `dev` and `prod` state keys. Application resources and their deployment workflows will be added with the application code.

The S3 state bucket and GitHub OIDC provider were created manually. Separate `dev` and `prod` IAM roles trust only their matching GitHub environments. Each role can access only its own state key and lock file. The `dev` environment allows `develop` and feature branches without approval; `prod` allows only `main` and requires a reviewer. Repository variables `TF_STATE_BUCKET`, `AWS_DEV_ROLE_ARN`, and `AWS_PROD_ROLE_ARN` identify the shared bucket and the roles. No long-term AWS credential is stored in GitHub.

The `infra/backend/` files contain the environment-specific state key, encryption, and locking settings. Supply `TF_STATE_BUCKET` and region `eu-west-3` when initializing each environment. Application resource permissions must be added to the matching role as those resources are defined. No AWS apply is part of the current CI checks.

The **OIDC state smoke** workflow runs on the local runner after any repository branch push. It uses the dev role outside `main` and the prod role on `main`, verifies the assumed role, and reads the state bucket location without changing AWS resources. The credential-free Terraform checks run for every pull request, regardless of its target branch.
