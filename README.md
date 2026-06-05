# Test Mod for Factorio Mod Uploader Action

This repository contains a test mod for the `factorio-mod-uploader-action`. The purpose of this mod is to demonstrate and test the functionality of the GitHub Action used for uploading Factorio mods.

## Usage

1. Clone or use this repository as a template
2. Make any necessary modifications to the mod
3. Push to `main` or create a GitHub release to trigger the automated upload

## Features

- **Automated Validation**: Validates `info.json` before packaging
- **Smart Compression**: Creates zip with `.factorioignore` support
- **Auto Version Sync**: Automatically updates `mod_info.yml` version from GitHub release tag (v2.0.5+)
- **Seamless Upload**: Pushes directly to Factorio Mod Portal

## Workflow

The automated pipeline is defined in `.github/workflows/publish.yml`:

```yaml
name: Publish Factorio Mod

on:
  push:
    branches:
      - main
  release:
    types: [published]

jobs:
  publish-mod:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Validate Mod
        uses: TheBrutalX/factorio-mod-uploader-action@v2
        with:
          action: validate
      
      - name: Create zip
        uses: TheBrutalX/factorio-mod-uploader-action@v2
        with:
          action: compress
          auto-update-version: 'true'
      
      - name: Upload Mod
        uses: TheBrutalX/factorio-mod-uploader-action@v2
        with:
          action: upload
          factorio-api-key: ${{ secrets.FACTORIO_API_KEY }}
```

> **Note**: Requires `FACTORIO_API_KEY` secret to be configured in repository settings. Generate your API key at [factorio.com/profile](https://factorio.com/profile).

## Action Details

Learn more about each action step:
- [Available Actions](https://github.com/TheBrutalX/Factorio-mod-uploader-action/wiki/Avaible-Actions)
- [Workflow Detail](https://github.com/TheBrutalX/Factorio-mod-uploader-action/wiki/WorkFlow-detail)
- [.factorioignore Syntax](https://github.com/TheBrutalX/Factorio-mod-uploader-action/wiki/.factorioignore)

## License

This project is licensed under the MIT License.

## Contributing

Feel free to open issues or submit pull requests if you find any bugs or have suggestions for improvements.
