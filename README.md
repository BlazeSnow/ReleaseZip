# ReleaseZip

将当前仓库打包为 zip，生成 SHA256 校验文件，并把两者上传为工作流产物（artifact）。

English version: [README.en.md](./README.en.md)

## 用法

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

      - name: 运行 ReleaseZip
        uses: BlazeSnow/ReleaseZip@v1
        with:
          artifact_name: my-repo-v1.0.0
          retention_days: 7
```

## 输入参数

- `artifact_name`：输出文件名和上传 artifact 的基础名称。默认值：`repo-zip`。
- `retention_days`：artifact 保留天数，取值范围为 `1-90` 的整数。默认值：`7`。

## 输出参数

- `zip_path`：生成的 zip 文件绝对路径。
- `sha256_path`：生成的校验文件绝对路径。

## 说明

- 该 Action 依赖 Runner 环境中的 `zip` 与 `sha256sum`（`ubuntu-latest` 默认可用）。
- 为了获得稳定构建，建议固定到 tag 或 commit SHA（例如 `@v1` 或 `@<commit-sha>`）。
