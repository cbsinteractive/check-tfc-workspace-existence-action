# Terraform Cloud Workspace Action

This action is used to set up a Terraform Cloud workspace.

## Inputs

The action expects the following inputs:

| Variable             | Required | Description                                                                 |
| -------------------- | -------- | --------------------------------------------------------------------------- |
| `action`             | Yes      | A verb describing the function to be performed                              |
| `tfcToken`           | Yes      | A Terraform Cloud API token with access to manage the workspace             |
| `orgName`            | Yes      | The name of the Terraform Cloud organization in which the workspace resides |
| `workspaceName`      | Yes      | The name of the Terraform Cloud workspace to manage                         |
| `workspaceVariables` | No       | A JSON array containing a set of variables to be created in the workspace   |

## Outputs

The action generates no outputs.

## Example Usage

Create a TFC workspace and populate it with some variables:

```yaml
- uses: cbsinteractive/tfc-workspace-action@v1
  with:
    action: create
    tfcToken: ${{ secrets.tfc_token }}
    orgName: ${{ secrets.tfc_organization }}
    workspaceName: some-workspace-name
    workspaceVariables: >
      [
        {
          "key": "FOO",
          "category": "env",
          "sensitive": true,
          "value": "${{ secrets.foo }}"
        },
        {
          "key": "BAR",
          "category": "env",
          "value": "no big secret"
        },
        {
          "key": "baz",
          "category": "terraform",
          "sensitive": true,
          "value": "${{ secrets.baz }}"
        }
      ]
```

This example assumes several variables stored as GitHub [encrypted secrets][].

[encrypted secrets]: https://docs.github.com/en/actions/reference/encrypted-secrets
