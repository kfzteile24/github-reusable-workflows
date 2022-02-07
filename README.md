# GitHub reusable workflows

Collection of reusable GitHub workflows for Terraform child/root modules.

## Usage

Save one of the following examples in the `.github/workflows` directory of your repository.

**Validate Commits:**

```yaml
---
name: Commits

on:
  pull_request:

jobs:
  commits:
    uses: dhoppeIT/github-reusable-workflows/.github/workflows/commits.yaml@main
```

**Generate Readme:**

```yaml
---
name: Readme

on:
  pull_request:

jobs:
  readme:
    uses: dhoppeIT/github-reusable-workflows/.github/workflows/docs.yaml@main
    with:
      output-file: README.md
      git-commit-message: "docs: Generate README.md"
      git-push: true
```

**Validate Terraform (child module):**

```yaml
---
name: Terraform

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  terraform:
    uses: dhoppeIT/github-reusable-workflows/.github/workflows/terraform.yaml@main
```

**Validate Terraform (root module):**


```yaml
---
name: Terraform

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  terraform:
    uses: dhoppeIT/github-reusable-workflows/.github/workflows/terraform_cloud.yaml@main
    secrets:
      cli_config_credentials_token: ${{ secrets.TF_API_TOKEN }}
      github-token: ${{ secrets.GITHUB_TOKEN }}
```

**Create Release:**


```yaml
---
name: Release

on:
  push:
    branches:
      - main

jobs:
  release:
    if: ${{ github.repository_owner == 'dhoppeIT' }}
    uses: dhoppeIT/github-reusable-workflows/.github/workflows/release.yaml@main
    with:
      release-type: terraform-module
      bump-minor-pre-major: true
      pull-request-title-pattern: "chore${scope}: Release${component} ${version}"
```

## Authors

Created and maintained by [Dennis Hoppe](https://github.com/dhoppeIT/).

## License

Apache 2 licensed. See [LICENSE](https://github.com/dhoppeIT/github-reusable-workflows/blob/main/LICENSE) for full details.
