---
name: Update GitHub Info
on:
  schedule:
    - cron: '0 9 * * *' # daily at 09:00 UTC
  workflow_dispatch: {}
permissions:
  contents: write
imports:
  aw:
    - version: 1
tools:
  github:
    repos:
      - '.'
    access: write
  web_fetch:
    allowed_domains:
      - github.blog
  create-pull-request:
    safe_outputs: true
network:
  allowed:
    - https://github.blog
---

## Description

Agentic workflow: read notes and GitHub Blog pages, update site/content/github-info.md, and open a PR for Mona to review.

## Prompt

You are an assistant run by this agentic workflow. Perform these steps:

- Read the repository file `notes/mona-notes.md` and extract any updates or items relevant to GitHub platform changes.
- Fetch and scrape content from the following URLs: https://github.blog/latest/ and https://github.blog/changelog/ (only the allowed domain `github.blog`).
- Combine and summarize relevant items from the notes and fetched pages into an updated markdown content suitable for `site/content/github-info.md`.
- Use the `edit` tool to update only `site/content/github-info.md` in a new branch. Do not write directly to `main`.
- Use the `create-pull-request` tool (safe outputs enabled) to open a pull request targeting `main`. The PR should include a concise title, a summary of changes, and reference this workflow run.
- Leave the PR as a proposal for Mona to review; do not merge.

Rules and constraints:

- Only modify `site/content/github-info.md` in this repository.
- The workflow has edit access via the `edit` tool configuration and may use `web_fetch` only for `github.blog` domains.
- Use `create-pull-request` with safe outputs so changes are proposed via a PR and not pushed directly to `main`.
 - Do not compile this workflow file automatically; do not run `gh aw compile` from this agent.

## Usage

Run on schedule (daily) or on demand via `workflow_dispatch`.
