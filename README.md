# Setup

1. On Settings > Actions, update Workflow permissions to read/write, and check `Allow GitHub Actions to create and approve pull requests`


# Notes

## A workflow cannot trigger another one

See [Automatic token authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#using-the-github_token-in-a-workflow).

> When you use the repository's GITHUB_TOKEN to perform tasks, events triggered by the GITHUB_TOKEN, with the exception of workflow_dispatch and repository_dispatch, will not create a new workflow run. This prevents you from accidentally creating recursive workflow runs. For example, if a workflow run pushes code using the repository's GITHUB_TOKEN, a new workflow will not run even when the repository contains a workflow configured to run when push events occur.

A workaround of this would be to [set up a deploy key](https://medium.com/prompt/trigger-another-github-workflow-without-using-a-personal-access-token-f594c21373ef)

1. Generate an Ed25519 key `ssh-keygen -t ed25519 -f id_ed25519 -N "" -q -C ""`
2. Add the public key to Settings > Deploy keys  with Allow write access selected
3. Add the private key to Settings > Secrets & Variables > Secrets

You want to use this key in the first workflow, so that the default Github token can run the second one.

```yml
- name: Code checkout
  uses: actions/checkout@v3
  with:
    ssh-key: ${{ secrets.RELEASE_KEY }}
```
