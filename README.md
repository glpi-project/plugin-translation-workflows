# Plugin translation workflows

This workflow will update translations using Transifex CLI.

You can use this workflow using the following Github Actions configuration.
This workflow will require the `contents: "write"` permission to be able to create an update commit.

* Install the necessary dependencies for extracting translations.
* Generate a `.pot` file for translations.
* `Push` updates to Transifex and `pull` translation files from Transifex.
* Create `Pull Request` if necessary.


```yaml
name: "Translate"

on:
  push:
    branches:
      - "main"
  schedule:
    - cron: "0 0 * * *"

jobs:
  refresh-translations:
    permissions:
      contents: "write"
      pull-requests: "write"
    name: "Push / Pull translations"
    uses: "glpi-project/plugin-translation-workflows/.github/workflows/translation.yml@v1"
    secrets:
      tx_token: "${{ secrets.TRANSLATE_TOKEN }}"
      based_branch: "master"
```
