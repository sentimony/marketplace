# AGENTS.md

## Layout

- `.claude-plugin/marketplace.json` - Claude Code marketplace `sentimony`.
- `.agents/plugins/marketplace.json` - Codex marketplace `sentimony`.
- `.github/workflows/ci.yml` - validation: both files parse, list the same plugins with the
  same `source`, every `ref` exists as a tag in its source repository, and each Claude Code
  `version` equals its `ref` without `v`.

## Plugins

Every entry is a `git-subdir` source pinned to a release tag of its source repository:

| Plugin | Repository | Path | Ref |
| --- | --- | --- | --- |
| `agentflow` | `sentimony/agentic-workflow` | `.` | `v0.0.22` |
| `skills` | `sentimony/skills` | `.` | `v0.0.101` |
| `cross-agent` | `sentimony/cross-agent` | `.` | `v0.0.5` |

## Rules

- The marketplace holds no plugin code: an entry only points at a tag of its source.
- Both marketplace files carry the same entries in the same order with the same `url` and
  `ref`. Claude Code uses `{"source": "git-subdir", "url", "path": ".", "ref"}`; Codex does not
  list `git-subdir` entries with `path: "."` (Codex 0.166.0), so its entries use
  `{"source": "url", "url", "ref"}`: the plugins live at the repository root. Claude Code entries also carry
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
