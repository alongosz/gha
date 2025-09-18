# Contributing to GitHub Actions Repository

Thank you for your interest in contributing to this GitHub Actions repository! This document provides guidelines for adding new actions and improving existing ones.

## Adding a New Action

### 1. Create Action Directory
Create a new directory under `actions/` with a descriptive kebab-case name:

```bash
mkdir actions/your-action-name
```

### 2. Create Action Definition
Create an `action.yml` file in your action directory. You can use the template from `templates/action-template/action.yml` as a starting point:

```yaml
name: 'Your Action Name'
description: 'Brief description of what this action does'
author: 'Andrew Longosz'

inputs:
  your-input:
    description: 'Description of the input parameter'
    required: false
    default: 'default-value'

outputs:
  your-output:
    description: 'Description of the output'
    value: ${{ steps.main-step.outputs.result }}

runs:
  using: 'composite'
  steps:
    - name: Your main step
      id: main-step
      shell: bash
      run: |
        # Your action logic here
        echo "result=value" >> $GITHUB_OUTPUT
```

### 3. Create Documentation
Create a `README.md` file in your action directory with:
- Description of the action
- Input and output tables
- Usage examples
- Multiple use cases

Use the template from `templates/action-template/README.md` as a starting point.

### 4. Update Main README
Add your action to the "Available Actions" section in the main `README.md` file.

## Action Guidelines

### Naming Conventions
- Use kebab-case for directory names (e.g., `setup-node-cache`)
- Use descriptive names that clearly indicate the action's purpose
- Use Title Case for action names in `action.yml`

### Input/Output Best Practices
- Provide sensible defaults for optional inputs
- Use clear, descriptive names for inputs and outputs
- Document all inputs and outputs with meaningful descriptions
- Use consistent naming patterns (kebab-case for input/output names)

### Shell Scripts
- Always specify `shell: bash` for shell steps
- Use proper error handling with `set -e` if needed
- Quote variables to handle spaces and special characters
- Use `$GITHUB_OUTPUT` for setting outputs

### Documentation
- Include comprehensive examples in README files
- Document all possible use cases
- Keep documentation up-to-date with action changes
- Use consistent formatting and style

## Code Quality

### Action Structure
- Keep actions focused on a single responsibility
- Use existing actions when possible (e.g., `actions/setup-node`)
- Follow the principle of least privilege
- Make actions reusable across different projects

### Error Handling
- Provide meaningful error messages
- Handle edge cases gracefully
- Use appropriate exit codes

### Security
- Never log sensitive information
- Use secrets appropriately
- Validate inputs when necessary

## Testing

While this repository doesn't have automated tests yet, please:
- Test your actions in a separate repository
- Verify all examples in your documentation work
- Test with different input combinations
- Ensure the action works on different operating systems if applicable

## Submitting Changes

1. Create a feature branch for your changes
2. Follow the guidelines above
3. Update documentation
4. Test your changes thoroughly
5. Submit a pull request with a clear description

## Questions?

If you have questions about contributing, please open an issue for discussion.

Thank you for contributing! 🎉