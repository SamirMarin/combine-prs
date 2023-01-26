# combine-prs ➡️📦⬅️

GitHub Action to combine multiple PRs into a single one

## About 💡

GitHub uses this Action to combine multiple dependabot PRs into a single one. Rather than having to deploy each PR individually, we can run this Action on a `cron` or `workflow_dispatch` to combine all the PRs into a single one to make dependency management just a little bit easier.

This Action is customizable so you can use it for your own purposes and it doesn't have to be specific to dependabot PRs.

## Inputs 📝

| Name | Description | Default | Required |
| ---- | ----------- | ------- | -------- |
| `github_token` | GitHub token to use for authentication within this Action | `${{ github.token }}` | `true` |
| `branch_prefix` | Prefix for the branch name to use for the combined PR | `dependabot` | `true` |
| `ci_required` | Whether or not CI should be passing to combine the PR - can be `"true"` or `"false"`  | `"true"` | `true` |
| `ignore_label` | The label to ignore when combining PRs | `"nocombine"` | `true` |

## Outputs 📤

| Name | Description |
| ---- | ----------- |
| `pr_url` | The pull request URL if a PR was created |
| `pr_number` | The pull request number if a PR was created |

## Usage 💻

Here is a brief example of how to use this Action in a workflow:

```yaml
name: Combine PRs

on:
  schedule:
    - cron: '0 1 * * 3' # Wednesday at 01:00
  workflow_dispatch: # allows you to manually trigger the workflow

jobs:
  combine-prs:
    runs-on: ubuntu-latest

    steps:
      - name: combine-prs
        id: combine-prs
        uses: github/combine-prs@vX.X.X # where X.X.X is the latest version
```
