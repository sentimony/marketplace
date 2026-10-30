# Contributing

This repository is the `sentimony` plugin marketplace for Claude Code and Codex. It holds two
marketplace files and no plugin code; plugins live in their source repositories.

## Branches and pull requests

- Work on a branch named `YYMMDDHHMM-dev-session` (date and time it was created), never on
  `main`: `main` rejects direct pushes.
- Open a pull request into `main`. The only merge method is squash merge; the branch is deleted
  after the merge.
- Keep the pull request title under 72 characters and describe the whole branch: it becomes
  the squash commit title.

## Bumping a plugin

1. Release the plugin in its source repository and wait for the tag.
2. Set the `ref` of its entry to that tag in both `.claude-plugin/marketplace.json` and
   `.agents/plugins/marketplace.json`, and in the `README.md` plugin table.
3. Install it from the branch in a throwaway config (commands in `AGENTS.md`).
4. Merge the pull request after CI is green, then tag the squash commit.

## Releases

Tags are annotated `v0.0.x`, bumped by patch only, placed on the squash commit in `main`. The
tag message lists every entry and its `ref`. A published tag is never moved, deleted, or
recreated: a defect is fixed by the next patch release.

## Checks

CI (`.github/workflows/ci.yml`) parses both marketplace files, compares their entries, and
checks with `git ls-remote` that every `ref` is a tag of its repository.
