# AGENTS.md

## Layout

- `.claude-plugin/marketplace.json` - Claude Code marketplace `sentimony`.
- `.agents/plugins/marketplace.json` - Codex marketplace `sentimony`.
- `.github/workflows/ci.yml` - validation: both files parse, list the same plugins with the
  same `source`, every `ref` exists as a tag in its source repository, and each Claude Code
  `version` equals its `ref` without `v`.
- `.github/workflows/auto-reviewer.yaml` - Auto Reviewer caller of
  `sentimony/github-workflows` `auto-reviewer-shared.yaml@v0.0.5`; it waits for the `validate` job
  of `CI` and reviews the PR as yngwald.

## Plugins

Every entry is a `url` source pinned to a release tag of its source repository:

| Plugin | Repository | Path | Ref |
| --- | --- | --- | --- |
| `agentflow` | `sentimony/agentic-workflow` | `.` | `v0.0.24` |
| `skills` | `sentimony/skills` | `.` | `v0.0.103` |
| `cross-agent` | `sentimony/cross-agent` | `.` | `v0.0.7` |

## Rules

- The marketplace holds no plugin code: an entry only points at a tag of its source.
- Both marketplace files carry the same entries in the same order with the same `url` and
  `ref`. Both files use `{"source": "url", "url", "ref"}` without `path`: the plugins live at the
  repository root. A `git-subdir` source with `path: "."` is not used: Codex 0.166.0 does not list
  such entries, and Claude Code 2.1.322 installs only the top-level files of the repository from
  it (no `skills/`). Claude Code entries also carry
  `description`, `category`, and `keywords` from the source plugin, and `version`, equal to `ref`
  without `v` (bump it together with `ref`); Codex entries carry
  `policy` and `category`.
- After a release tag in a source repository, bump the `ref` of its entries in both files,
  the Claude Code `version`, the table above, the `README.md` plugin table, and the tags in the
  README Antigravity `agy plugin install` commands with a patch release of this repository.
  A `ref` always names an existing tag, never a branch.
- Before merging, install the changed plugins from the branch in a throwaway config:
  `CLAUDE_CONFIG_DIR=<tmp> claude plugin marketplace add <checkout>` and
  `claude plugin install <plugin>@sentimony`; `CODEX_HOME=<tmp> codex plugin marketplace add
  <checkout>` and `codex plugin add <plugin>@sentimony`.
- Tags: annotated `v0.0.x`, patch bumps only, on the squash commit in `main`; the message lists
  every entry and its `ref`. A published tag is never moved or recreated.
- Branches: `YYMMDDHHMM-dev-session`, squash-merged into `main` via PR; the branch is deleted
  after merge. `main` accepts no direct pushes.
- License: MIT, Ihor Orlovskyi.
- English only, plain hyphen.
