---
on:
  workflow_dispatch:
  schedule:
    - cron: "0 */6 * * *"

engine: copilot

permissions:
  contents: read
  copilot-requests: write

tools:
  edit:
  web-fetch:

network:
  allowed:
    - github.github.com

safe-outputs:
  create-pull-request:
    max: 1
    allowed-files:
      - index.html

---

# highlights-of-day

Update the Daily Updates section in `index.html` with one new FAQ entry for the current workflow run date.

## Requirements

1. Fetch the GitHub Agentic Workflows FAQ from:
   https://github.github.com/gh-aw/reference/faq/
2. Work in UTC for all date decisions. Determine "today" from the workflow run date in UTC.
3. Use the existing `index.html` structure and styling conventions exactly. Preserve all existing updates.
4. Select exactly one FAQ question that is not already represented in `index.html` (including existing dialogs).
5. If there is no unused FAQ available, make no changes.
6. Find or create the matching Daily Update for today:
   - If a placeholder dialog for today already exists, reuse it.
   - Otherwise, add one new navigation control and one new matching dialog for today.
7. Match existing conventions:
   - ID naming style for trigger/dialog/question/answer
   - date wording style (e.g., "1st of August")
   - dialog header format
   - semantic HTML structure and classes
8. Never duplicate any of the following:
   - date in Daily Updates navigation
   - navigation control
   - dialog
   - FAQ question
9. If today's dialog already contains a real FAQ question and answer, make no changes.
10. Add a concise, accurate FAQ answer based on the official FAQ content.

## Editing constraints

- Modify only `index.html`.
- Make the minimal change needed.
- Keep existing JavaScript dialog behavior intact.
- Do not alter unrelated content, formatting style, or existing entries.

## Output policy

- If an update is needed, emit exactly one `create_pull_request` safe output containing only the `index.html` change.
- If no update is needed, do not emit write outputs.

## Prohibited actions

- Do not compile workflows.
- Do not modify any file other than `index.html`.
