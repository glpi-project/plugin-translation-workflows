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
      tx_token: "${{ secrets.TRANSLATE_TOKEN }}"
    with:
      branch: "main"

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

jobs:
  transifex_push_pull:
    permissions:
      contents: "write"
      pull-requests: "write"
    name: "Transifex Push / Pull"
    uses: "glpi-project/plugin-translation-workflows/.github/workflows/transifex_push_pull.yml@v1"
    secrets:
      tx_token: "${{ secrets.TRANSIFEX_TOKEN }}"
    with:
      branch: "main"

```
