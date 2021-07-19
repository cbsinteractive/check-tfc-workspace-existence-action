# Check TFC Workspace Existence

This action is used to determine if a Terraform Cloud workspace exists.

## Inputs

The action expects the following inputs:

| Variable             | Required | Description                                                                 |
| -------------------- | -------- | --------------------------------------------------------------------------- |
| `tfcToken`           | Yes      | A Terraform Cloud API token with access to manage the workspace             |
| `orgName`            | Yes      | The name of the Terraform Cloud organization in which the workspace resides |
| `workspaceName`      | Yes      | The name of the Terraform Cloud workspace to manage                         |

## Outputs

The action generates no outputs.

## Example Usage

```yaml
- name: Check for existing workspace
  id: check-workspace
  continue-on-error: true # Will error if the workspace already exists
  uses: cbsinteractive/check-tfc-workspace-existence@v1
  with:
    tfcToken: ${{ secrets.tfc_token }}
    orgName: ${{ secrets.tfc_organization }}
    workspaceName: some-workspace-name

- name: Create new workspace
  if: steps.check-workspace.outcome == 'failure'
  run: echo Creating new workspace...
```

This example assumes several variables stored as GitHub [encrypted secrets][].

[encrypted secrets]: https://docs.github.com/en/actions/reference/encrypted-secrets
