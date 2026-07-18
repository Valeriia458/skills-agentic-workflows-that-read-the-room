# GitHub Info

## Mona's editorial angle

Mona's website focuses on practical GitHub guidance backed by official references from:

- docs.github.com
- github.blog
- github.blog/changelog

## Current homepage themes

- GitHub collaboration basics: repositories, branches, pull requests, and merges.
- GitHub Copilot as an AI coding assistant across the IDE, CLI, and GitHub.
- GitHub Actions as the automation layer behind repository workflows.
- Recent GitHub Blog and Changelog stories worth watching.

## Latest GitHub Updates

- This page will be updated daily with notable items from the GitHub Blog and Changelog; check those sources for the newest platform changes.

### How this updater works

- read `notes/mona-notes.md` for editorial context and local notes
- use the GitHub Blog (`https://github.blog/latest/`) for announcements
- use the GitHub Changelog (`https://github.blog/changelog/`) for release notes
- update `site/content/github-info.md` with a concise summary of notable items
- create a pull request for Mona to review using `create-pull-request` with `safe-outputs` enabled

Example (agent pseudo-code):

```
# 1. Read local notes
read_file('notes/mona-notes.md')

# 2. Fetch remote sources (allowed domain: github.blog)
latest = web_fetch('https://github.blog/latest/')
changelog = web_fetch('https://github.blog/changelog/')

# 3. Summarize and update the site file
updated_md = summarize(latest, changelog, local_notes)
edit('site/content/github-info.md', content=updated_md)

# 4. Propose changes via PR (safe outputs)
create_pull_request(title='Update GitHub info', body='Automated update for Mona', safe_outputs=True)
```

The agent should only modify `site/content/github-info.md` and must not merge the PR; Mona will review and merge.

