---
on:
  schedule: daily on weekdays
  skip-if-match: 'is:issue is:open in:title "Daily Digest -"'

permissions:
  contents: read
  issues: read
  pull-requests: read
  actions: read

tools:
  github:
    mode: gh-proxy
    toolsets: [default]

strict: true
timeout-minutes: 10

safe-outputs:
  create-issue:
    max: 1
    close-older-issues: true
  noop:
---

# daily-digest

## Instructions

Every weekday, review all open issues and pull requests in this repository and
publish a single digest issue.

Use the GitHub tools to gather the current open issues and pull requests.
Group items by label, using an `Unlabeled` section when an item has no labels.

The digest issue must include:
- The total number of open issues
- The total number of open pull requests
- For each item: title, author, URL, and how long it has been open

Title the issue `Daily Digest - <YYYY-MM-DD>`.

Write the body in GitHub-flavored markdown. Start headings at `###`.

If there are no open issues and no open pull requests, do not create an issue.
Call the `noop` safe output instead and explain that there was nothing to report.

Credit humans accurately when summarising activity. If a bot opened or updated an
item on behalf of a person, avoid framing the bot as the primary actor.

## Notes

- Run `gh aw compile` to generate the GitHub Actions workflow
- See https://github.github.com/gh-aw/ for complete configuration options and tools documentation
