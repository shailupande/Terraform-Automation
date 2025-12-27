Branch selection

- In Jenkins build parameters, pick `BRANCH_CHOICE` from the dropdown (common branches listed).
- To use a custom branch, set `BRANCH_OVERRIDE` to the exact branch name — it will override `BRANCH_CHOICE`.
- Select `ACTION` (plan or apply) and run the job.

Notes

- If you want a dynamic dropdown of repository branches, install and configure the Jenkins "Git Parameter" or "Active Choices" plugin and update the job to use that parameter type.
- The pipeline uses `sh` steps for Terraform; ensure the agent/node is a Linux shell. Replace `sh` with `bat` for Windows agents.
