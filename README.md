# Write File Action

This action writes a file.

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
uses: DamianReeves/write-file-action
with:
  path: ${{ env.home}}/.bashrc
  contents: |
    Hello World!
  write-mode: append
```
