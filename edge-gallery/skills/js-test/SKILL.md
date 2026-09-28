---
name: js-test
description: Test JavaScript Agent Skill execution.
---

# JavaScript Test

## Instructions

Call the `run_js` tool with exactly these parameters:
- script name: `index.html`
- data: A JSON string with the following field:
  - message: String. Optional test message.

If the tool returns a result, report it exactly to the user.