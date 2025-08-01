# Instruqt CLI

This repository contains the releases of the Instruqt commandline interface.

## GitHub Actions

This repository also provides GitHub Actions for using the Instruqt CLI in CI/CD workflows:

### Setup Action

Installs and caches the Instruqt CLI:

```yaml
- uses: instruqt/cli/setup@v1
```

See [setup/README.md](setup/README.md) for detailed documentation.

### Validate Action

Validates Instruqt lab configurations:

```yaml
- uses: instruqt/cli/validate@v1
  with:
    path: ./path/to/lab
```

See [validate/README.md](validate/README.md) for detailed documentation.

### Example Workflow

See [example-workflow.yml](example-workflow.yml) for a complete example of validating multiple labs in a GitHub Actions workflow.
