# Write File Action

This action writes a file.

Thanks to the provided [typings](action-types.yml), it is possible to use this action in a type-safe way using
https://github.com/typesafegithub/github-workflows-kt which allows writing workflow files using a type-safe Kotlin DSL.

## Inputs

### `path`

**Required** The path to the file to write.

### `contents`

**Required** The contents of the file.

### `write-mode`

**Optional** The mode of writing to use: `overwrite`, `append`, or `preserve`.

Modes:

- `overwrite` - overwrite the file if it exists
- `append` - if the file exists, it will be appended to
- `preserve` - if the file already exists the contents will not be written to

**Default** `append`

## Outputs

### `size`

Returns the file size.

## Example usage

```yaml
uses: DamianReeves/write-file-action@master
with:
  path: ${{ env.home}}/.bashrc
  contents: |
    Hello World!
  write-mode: append
```

## Example usage with checkout, commit and push
```yaml
name: Overwrite some file

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Overwrite file
        uses: "DamianReeves/write-file-action@master"
        with:
          path: path/to/file.js
          write-mode: overwrite
          contents: |
            console.log('some contents')
            
      - name: Commit & Push
        uses: Andro999b/push@v1.3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: main
          force: true
          message: 'Overwritten by Github Actions - ${date}'
```
