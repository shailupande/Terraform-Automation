Branch selection

- In Jenkins build parameters, pick `BRANCH_CHOICE` from the dropdown (common branches listed).
- To use a custom branch, set `BRANCH_OVERRIDE` to the exact branch name — it will override `BRANCH_CHOICE`.
- Select `ACTION` (plan or apply) and run the job.

Notes

- If you want a dynamic dropdown of repository branches, install and configure the Jenkins "Git Parameter" or "Active Choices" plugin and update the job to use that parameter type.
- The pipeline uses `sh` steps for Terraform; ensure the agent/node is a Linux shell. Replace `sh` with `bat` for Windows agents.

Key pair notes

- To have Terraform create a key pair for the instance, set the `public_key` variable (either via `-var 'public_key="..."'` or in `terraform.tfvars`) to your public key material (the contents of `id_rsa.pub`). Terraform will create a key pair with the name from `key_name`.
- If you already have a key pair in AWS, leave `public_key` empty and ensure `key_name` matches an existing key-pair name in the region.

Example to run with a public key file:
```bash
terraform apply -var="public_key=$(cat ~/.ssh/id_rsa.pub)" -var="key_name=my-key-name"
```
