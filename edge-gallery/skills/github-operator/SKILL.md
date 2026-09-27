---
name: github-operator
description: Read and update files in a GitHub repository through the GitHub Contents API.
metadata:
  require-secret: true
  require-secret-description: Enter a GitHub fine-grained personal access token with Contents read/write permission for the target repository. The token is passed securely to the skill as GITHUB_TOKEN.
---

# GitHub Operator

Use this skill when the user wants an on-device AI workflow to read or update files in GitHub.

## Inputs

Provide JSON with:
Call the `run_js` tool with script name `index.html` and pass the following as its data JSON string:
- `action`: `read_file` or `upsert_file`
- `owner`: GitHub owner/login
- `repo`: repository name
- `path`: repository-relative file path
- `content`: required for `upsert_file`
- `message`: optional commit message for `upsert_file`

## Authentication

The JavaScript implementation requires a GitHub fine-grained personal access token supplied through the Agent Skills secret mechanism. Give the secret the name `GITHUB_TOKEN`.

The token must have only the minimum repository Contents permission needed for the target repository.

## Behavior

- Never expose the GitHub token in output.
- Validate owner, repo, and path before making requests.
- `read_file` returns decoded UTF-8 file content.
- `upsert_file` creates or updates a file and returns the commit information.
- When updating an existing file, first obtain its current blob SHA.
- Return machine-readable JSON.

## Example

Read:
```json
{"action":"read_file","owner":"r8bvwq54b4-droid","repo":"AI-Operating-Company","path":"README.md"}
```

Update:
```json
{"action":"upsert_file","owner":"r8bvwq54b4-droid","repo":"AI-Operating-Company","path":"tasks/example.md","content":"# Example\n","message":"Update example task"}
```
