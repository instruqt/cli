# Validate Instruqt Lab Action

This action validates Instruqt lab configurations using the `instruqt lab validate` command.

## Prerequisites

This action requires the Instruqt CLI to be installed. Use the `instruqt/cli/setup` action first.

## Inputs

### `path`

**Required** Path to the lab directory or HCL file to validate.

### `fail-on-error`

**Optional** Whether to fail the action on validation errors. Default: `true`.

## Outputs

### `status`

The validation status: `success` or `failed`.

### `output`

The full output from the `instruqt lab validate` command.

## Example usage

### Basic validation

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: instruqt/cli/setup@v1
  - uses: instruqt/cli/validate@v1
    with:
      path: ./lab
```

### Validate multiple labs

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: instruqt/cli/setup@v1
  - uses: instruqt/cli/validate@v1
    with:
      path: ./lab-1
  - uses: instruqt/cli/validate@v1
    with:
      path: ./lab-2
```

### Matrix validation

```yaml
strategy:
  matrix:
    lab: [./lab-1, ./lab-2, ./lab-3]
steps:
  - uses: actions/checkout@v4
  - uses: instruqt/cli/setup@v1
  - uses: instruqt/cli/validate@v1
    with:
      path: ${{ matrix.lab }}
```

### Continue on validation errors

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: instruqt/cli/setup@v1
  - uses: instruqt/cli/validate@v1
    with:
      path: ./lab
      fail-on-error: false
  - name: Check validation result
    if: steps.validate.outputs.status == 'failed'
    run: echo "Validation failed but continuing..."
```

## Example Output

### Successful validation

```
==> Validating lab...
    [SUCCESS] Lab is valid
```

### Failed validation

```
==> Validating lab...
    [ERROR] Error:
      Missing required field "description" in task resource "first_task"
    
     /path/to/lab/tasks.hcl:5,1-15
          5 | resource "task" "first_task" {
    
    
    Lab is not valid
```

## Features

- **Clean output**: Preserves the native `instruqt lab validate` formatting
- **Job summaries**: Creates collapsible summaries in the GitHub Actions UI
- **Flexible error handling**: Option to continue on validation failures
- **Grouped output**: Uses GitHub Actions groups for better readability