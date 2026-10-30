# AGENTS.md

## Layout

- `.claude-plugin/marketplace.json` - Claude Code marketplace `sentimony`.
- `.agents/plugins/marketplace.json` - Codex marketplace `sentimony`.
- `.github/workflows/ci.yml` - validation: both files parse, list the same plugins with the
  same `source`, and every `ref` exists as a tag in its source repository.

## Plugins

Every entry is a `git-subdir` source pinned to a release tag of its source repository;
the current entries and refs are in the marketplace files and the `README.md` plugin table.

## Rules

- The marketplace holds no plugin code: an entry only points at a tag of its source.
- Both marketplace files carry the same entries in the same order with an identical `source`
  object `{"source": "git-subdir", "url", "path", "ref"}`. Claude Code entries also carry
  `description`, `category`, and `keywords` from the source plugin; Codex entries carry
  `policy` and `category`.
- After a release tag in a source repository, bump the `ref` of its entries in both files and
  the `README.md` plugin table with a patch release of this repository.
  A `ref` always names an existing tag, never a branch.
- Before merging, install the changed plugins from the branch in a throwaway config:
  `CLAUDE_CONFIG_DIR=<tmp> claude plugin marketplace add <checkout>` and
  `claude plugin install <plugin>@sentimony`; `CODEX_HOME=<tmp> codex plugin marketplace add
  <checkout>` and `codex plugin add <plugin>@sentimony`.
  Copy `~/.codex/auth.json` into the Codex `<tmp>`. A `ref` may name a pushed branch for this
  check only. List Codex plugins with `codex plugin list -m sentimony`: the bare command also
  prints the remote catalog (~1.6 MB).
- Tags: annotated `v0.0.x`, patch bumps only, on the squash commit in `main`; the message lists
  every entry and its `ref`. A published tag is never moved or recreated.
- Branches: `YYMMDDHHMM-dev-session`, squash-merged into `main` via PR; the branch is deleted
  after merge. `main` accepts no direct pushes.
- License: MIT, Ihor Orlovskyi.
- English only, plain hyphen.
