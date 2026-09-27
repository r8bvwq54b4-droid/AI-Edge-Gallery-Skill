---
name: github-operator
description: Read and update files in a GitHub repository through the GitHub Contents API.
metadata:
  require-secret: true
  require-secret-description: Enter your GitHub fine-grained personal access token. It is passed securely to the JavaScript skill and is never returned.
---

# GitHub Operator

Use this skill to read or update files in GitHub.

## Instructions

You MUST use the `run_js` tool to perform the GitHub operation.

Call `run_js` with exactly these parameters:
- `script name`: `index.html`
- `data`: a JSON string containing:
  - `action`: String. Must be `read_file` or `upsert_file`.
  - `owner`: String. GitHub repository owner/login.
  - `repo`: String. GitHub repository name.
  - `path`: String. Repository-relative file path.
  - `content`: String. Required only for `upsert_file`.
  - `message`: String. Optional commit message for `upsert_file`.

Example data for reading:
`{"action":"read_file","owner":"r8bvwq54b4-droid","repo":"AI-Operating-Company","path":"README.md"}`

Example data for updating:
`{"action":"upsert_file","owner":"r8bvwq54b4-droid","repo":"AI-Operating-Company","path":"tasks/example.md","content":"# Example\n","message":"Update example task"}`

## Authentication

The JavaScript skill receives the GitHub token as its second argument. Never put the token in the prompt or return it in output.

The token should have Contents read/write permission for the target repository.

## Behavior

- For `read_file`, return the decoded UTF-8 file content.
- For `upsert_file`, create or update the requested file.
- Never expose the GitHub token.
