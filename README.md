# Plugin translation workflows

## Transifex

### Push

This workflow will update and push the translation file (`<plugin.pot>`) using the Transifex CLI.

* Install the necessary dependencies for extracting translations.
* Generate a `<plugin>.pot` file.
* Pushes the `<plugin>.pot` file update to Transifex.

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
      based_branch: "main"

```


### Push / pull

This workflow will update translations using Transifex CLI.

* Install the necessary dependencies for extracting translations.
* Generate a `<plugin>.pot` file for translations.
* `Push` updates to Transifex and `pull` translation files from Transifex.
* Compile translation files to binary version (`.mo`)
* Create `Pull Request` if necessary.

You can use this workflow using the following Github Actions configuration.
This workflow will require the `contents: "write"` permission to be able to create an update commit.


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
      tx_token: "${{ secrets.TRANSLATE_TOKEN }}"
      based_branch: "main"

```
