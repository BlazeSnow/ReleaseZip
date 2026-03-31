# ReleaseZip

Create a zip archive of the current repository, generate a SHA256 file, and upload both as workflow artifacts.

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

- `artifact_name`: Base name for output files and uploaded artifact. Default: `repo-zip`.
- `retention_days`: Artifact retention days, integer in `1-90`. Default: `7`.

## Outputs

- `zip_path`: Absolute path of generated zip file.
- `sha256_path`: Absolute path of generated checksum file.

## Notes

- This action expects `zip` and `sha256sum` to be available on the runner (available on `ubuntu-latest`).
- Pin to a tag or commit SHA (for example `@v1` or `@<commit-sha>`) for stable builds.
