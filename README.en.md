# ReleaseZip

Create a zip archive of the current repository, generate a SHA256 file, and upload both as workflow artifacts.

Simplified Chinese version: [README.md](./README.md)

## Usage

```yaml
name: Package

on:
  workflow_dispatch:

jobs:
  package:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - name: Checkout
        uses: actions/checkout@v6

      - name: Run ReleaseZip
        uses: BlazeSnow/ReleaseZip@v1
        with:
          artifact_name: my-repo-v1.0.0
          retention_days: 7
```

## Inputs

| Parameter        | Description                                           | Required | Default    |
| ---------------- | ----------------------------------------------------- | -------- | ---------- |
| `artifact_name`  | Base name for output files and uploaded artifact.     | No       | `repo-zip` |
| `retention_days` | Artifact retention days, integer in the range `1-90`. | No       | `7`        |

## Outputs

| Parameter     | Description                                   |
| ------------- | --------------------------------------------- |
| `zip_path`    | Absolute path of the generated zip file.      |
| `sha256_path` | Absolute path of the generated checksum file. |
