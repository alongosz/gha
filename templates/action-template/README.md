# Action Name

Brief description of what this action does.

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `example-input` | Description of the input parameter | No | `default-value` |

## Outputs

| Name | Description |
|------|-------------|
| `example-output` | Description of the output |

## Usage

```yaml
- name: Use this action
  uses: alongosz/gha/actions/action-name@main
  with:
    example-input: 'value'
```

## Examples

### Basic usage
```yaml
- uses: alongosz/gha/actions/action-name@main
```

### With custom input
```yaml
- uses: alongosz/gha/actions/action-name@main
  with:
    example-input: 'custom-value'
```