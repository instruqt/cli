# Setup Instruqt CLI Action

This action installs and caches the Instruqt CLI for use in GitHub Actions workflows.

## Inputs

### `version`

**Optional** The version of Instruqt CLI to install. Default: `latest`.

## Outputs

### `version`

The version of the Instruqt CLI that was installed.

## Example usage

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: instruqt/cli/setup@v1
  - uses: instruqt/cli/validate@v1
    with:
      path: ./path/to/lab
```

## Advanced usage

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: instruqt/cli/setup@v1
    with:
      version: '2287-00a1200'
  - uses: instruqt/cli/validate@v1
    with:
      path: ./lab-1
  - uses: instruqt/cli/validate@v1
    with:
      path: ./lab-2
```

## Platform Support

This action supports:
- Linux (ubuntu runners)
- macOS (macos runners, both Intel and Apple Silicon)
- Windows (windows runners)

The CLI binary is cached to improve performance across workflow runs.