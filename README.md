# Github Actions for Backstage TechDocs

This repository contains several GitHub actions designed to support publishing
[Backstage TechDocs]. Read the [Backstage documentation] for recommendations on
how to setup the cloud storage provider.

[Backstage TechDocs]: https://backstage.io/docs/features/techdocs/techdocs-overview
[Backstage documentation]: https://backstage.io/docs/features/techdocs/architecture#recommended-deployment

## Actions related to publishing

The setup, generate, and publish actions are intended to be used within a
workflow to publish techdocs to a cloud storage provider. These are split into
separate actions to allow additional dependencies to be installed and processing
steps to be performed as-needed.

Example usage:

``` yaml
# .github/workflows/publish-techdocs.yml

name: Publish TechDocs to the S3 Bucket for Backstage

on:
  push:
    branches: [main]
    paths:
      - "docs/**"
      - "mkdocs.yml"

jobs:
  publish-techdocs:
    runs-on: ubuntu-latest
    name: Publish Techdocs to S3
    steps:
      - uses: actions/checkout@v3
      - uses: ezcater/techdocs-actions/setup@main
      - uses: ezcater/techdocs-actions/generate@main
      - uses: ezcater/techdocs-actions/publish@main
        with:
          aws-bucket-name: ${{ secrets.EDIT_ME }}
          aws-region: ${{ secrets.EDIT_ME }}
          aws-access-key-id: ${{ secrets.EDIT_ME }}
          aws-secret-access-key: ${{ secrets.EDIT_ME }}
          entity-kind: "edit_me"
          entity-name: "edit_me"
```
