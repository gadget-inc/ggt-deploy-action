# GGT Deploy Github Action

This Github Action is used to deploy a repository to a gadget project's production by adding a step to your workflow.

```yaml
- name: Deploy to production
uses: gadget-inc/ggt-deploy-action@v1
with:
    app: 'gadget-project'
    environment: 'development'
    token: ${{ secrets.GGT_TOKEN }}
```

`token` is a generated CLI token from your gadget project. We recommend storing it as
[GitHub Encrypted Secrets.](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

`environment` is the environment you want to push the current repository to and deploy from.

`app` is the name of the gadget project who's production will be deployed to.

optionally, you can specify `allow-issues` to allow the deployment to continue even if there are issues on the gadget project.

```yaml
- name: Deploy to production
uses: gadget-inc/ggt-deploy-action@v1
with:
    app: 'gadget-project'
    environment: 'development'
    token: ${{ secrets.GGT_TOKEN }}
    allow-issues: 'true'
```

# Full Github Action Example

```yaml
name: cd

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Deploy to production
        uses: gadget-inc/ggt-deploy-action@v1
        with:
          app: 'gadget-app'
          environment: 'development'
          token: ${{ secrets.GGT_TOKEN }}
```
