# ReleaseZip

Package the current repository into a zip file, generate a SHA256 checksum file, and upload both as workflow artifacts.

Simplified Chinese version: [README.md](./README.md)

## Usage

```yaml
name: Package

on:
  workflow_dispatch:
    inputs:
      tag:
        description: 'Release tag'
        required: true
        default: 'v1.0.0'

jobs:
  package:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v6
        with:
          lfs: true

      - name: Run ReleaseZip
        uses: BlazeSnow/ReleaseZip@v1
        with:
          artifact_name: ${{ github.event.repository.name }}-${{ inputs.tag }}
          retention_days: 7
```

## Artifacts

`artifact_name`_bundle.zip

## Inputs

| Parameter        | Description                                            | Required | Default    |
| ---------------- | ------------------------------------------------------ | -------- | ---------- |
| `artifact_name`  | Base name for output files and uploaded artifact.      | No       | `repo-zip` |
| `retention_days` | Number of days to retain the artifact, integer `1-90`. | No       | `7`        |

## Outputs

| Parameter     | Description                                   |
| ------------- | --------------------------------------------- |
| `zip_path`    | Absolute path of the generated zip file.      |
| `sha256_path` | Absolute path of the generated checksum file. |

## Changelog

<https://github.com/BlazeSnow/ReleaseZip/blob/main/CHANGELOG.md>
