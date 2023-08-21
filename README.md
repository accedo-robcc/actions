# Setup

1. On Settings > Actions, update Workflow permissions to read/write, and check `Allow GitHub Actions to create and approve pull requests`


# Notes

## A workflow cannot trigger another one

See [Automatic token authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#using-the-github_token-in-a-workflow).

> When you use the repository's GITHUB_TOKEN to perform tasks, events triggered by the GITHUB_TOKEN, with the exception of workflow_dispatch and repository_dispatch, will not create a new workflow run. This prevents you from accidentally creating recursive workflow runs. For example, if a workflow run pushes code using the repository's GITHUB_TOKEN, a new workflow will not run even when the repository contains a workflow configured to run when push events occur.
