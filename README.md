[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

# node-pr-labeler

GitHub Action applying labels to [nodejs/node pull requests](https://github.com/nodejs/node/pulls) based off of files have been changed.

_Previously part of the [nodejs-github-bot](https://github.com/nodejs/github-bot). Extracted to make it easier for Node.js collaborators to maintain the label rules themselves._

## Usage

Two parts are needed to make use of this Action:

1. GitHub Action Workflow triggered by pull requests opened in the target repository
2. A `.yml` configuration file declaring the rules for filepath -> labels

### 1. GitHub Action Workflow

```yml
name: Label PRs

on:
  pull_request_target:
    types: [opened]

jobs:
  label:
    runs-on: ubuntu-latest

    steps:
      - uses: step-security/node-pr-labeler@v1
        with:
          configuration-path: .github/pr-labels.yml
```

> **Security note:** Do not add a `actions/checkout` step or execute any code from the pull request in this workflow. `pull_request_target` runs with write access and access to secrets; checking out or running PR code in this context would allow attackers to exfiltrate secrets or gain write access to the repository.

### 2. `.yml` configuration with filepath -> label rules

[`.github/pr-labels.yml`](.github/pr-labels.yml) acts as an example and used in the test suite of this GitHub Action.

This configuration file is part of the using repository, allowing its collaborators to maintain the labelling rules, close to the source code they relate to.

## License

[MIT](https://opensource.org/licenses/MIT)
