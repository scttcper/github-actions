# github-actions
Reusable Workflow based on https://github.com/node-modules/github-actions by 
fengmk2


## Usage

This workflow will be triggered when the CI workflow completes successfully on the `master` branch.

```yaml
.github/workflows/release.yml
name: Release
on:
  workflow_run:
    workflows: ['CI']
    branches: [master]
    types: [completed]

permissions:
  contents: write
  deployments: write
  issues: write
  pull-requests: write
  id-token: write

jobs:
  release:
    name: NPM Release
    if: ${{ github.event.workflow_run.conclusion == 'success' }}
    uses: scttcper/github-actions/.github/workflows/npm-release.yml@main
    secrets:
      GIT_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```