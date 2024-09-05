# Plugin translation workflows

## Transifex

### Push

This workflow will push the up-to-date locales sources to Transifex.

You can use this workflow using the following Github Actions configuration.

```yaml
name: "Transifex Push"

on:
  push:
    branches:
      - "main"

jobs:
  transifex_push:
    name: "Transifex Push"
    uses: "glpi-project/plugin-translation-workflows/.github/workflows/transifex_push.yml@v1"
    secrets:
      # The Transifex API token used to push sources.
      transifex-token: "${{ secrets.TRANSIFEX_TOKEN }}"

```


### Push / pull

This workflow will fetch the latest translations from Transifex and propose a pull request with the incoming changes.

You can use this workflow using the following Github Actions configuration.
This workflow will require the `contents: "write"` permission to be able to create an update commit and the `pull-requests: "write"` permission to create the pull request.

```yaml
name: "Transifex Push / Pull"

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:

jobs:
  transifex_push_pull:
    permissions:
      contents: "write"
      pull-requests: "write"
    name: "Transifex Push / Pull"
    uses: "glpi-project/plugin-translation-workflows/.github/workflows/transifex_push_pull.yml@v1"
    secrets:
      # The GitHub access token used when the locales update pull request is created.
      # This personal access token (PAT) is required to ensure that subsequent workflows that listen
      # to the pull_request and the push events will be triggered.
      # This PAT requires the `Content: read/write` and the `Pull requests: read/write` permissions.
      github-token: "${{ secrets.LOCALES_SYNC_TOKEN }}"
      # The Transifex API token used to push sources and pull translations.
      transifex-token: "${{ secrets.TRANSIFEX_TOKEN }}"

```
