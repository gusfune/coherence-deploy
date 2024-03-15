# action-coherence-deploy

This action setup [Coherence](https://app.withcoherence.com) CLI and allows automatic deploy of an enviroment.

## Input

```yaml
inputs:
  arch:
    description: |
      defines the architecture of the runner
      default is: linux-amd64
      accepts: darwin-arm64 | linux-386 | linux-amd64 | linux-arm64
    default: linux-amd64
  branch:
    description: |
      name of the branch to deploy
      default is the current branch the runner is in
    default: main
  commit_sha:
    description: |
      SHA value of the commit if you want to manually set which to deploy
      default to the current reference on Github
    required: false
  environment_id:
    description: |
      id of Coherence environment
    required: true
  token:
    description: |
      your Coherence COCLI_REFRESH_TOKEN, can be generated using `cocli auth login`
      or following this example: https://github.com/coherenceplatform/cocli/blob/main/examples/auth.sh
    required: true
```

### Usage

```yaml
name: Pull Request
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy
        uses: gusfune/coherence-deploy@0.2.0
        with:
          arch: linux-amd64
          commit_sha: ${{ github.sha }}
          environment_id: 12345
          token: ${{ secrets.COCLI_REFRESH_TOKEN }}
```