Used together with [action-terraform](https://github.com/Pararius/action-terraform) for auto-approving (and merging) of pull request created by Dependabot

Example usage:

```yaml
  terraform:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Terraform
        uses: Pararius/action-terraform@0.0.29
        with:
          terraform_directory: ./terraform
          terraform_do_apply: false
          terraform_parallelism: 3

  auto-approve:
    runs-on: ubuntu-latest
    needs: [terraform]
    if: github.actor == 'dependabot[bot]'
    steps:
      - uses: Pararius/action-terraform-automerge@dev
        with:
          github-token: <github-token-here>
          terraform-directory: 'terraform/'
          merge: true
```
