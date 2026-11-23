# marketplace

Public plugin marketplace of sentimony: one place to install Sentimony agent skills as Claude
Code and Codex plugins.

Version: `v0.0.25`

## Plugins

| Plugin | Version | Skills |
| --- | --- | --- |
| [cross-agent](https://github.com/sentimony/cross-agent) | 0.0.14 | `cross-agent` |
| [agentic-workflow](https://github.com/sentimony/agentic-workflow) | 0.0.34 | `resolve-issue`, `resolve-pr`, `resolve-ci`, `resume-task`, `specify`, `plan-craft`, `implement`, `verify`, `cr-request`, `cr-received`, `finalize` |
| [skills](https://github.com/sentimony/skills) | 0.0.116 | `scope-triage`, `doc-preview`, `plan-craft`, `implement`, `subagents-implement`, `worktree-isolation`, `parallel-agents`, `tdd`, `request-review`, `cross-review`, `received-review`, `debug`, `playwright-debug`, `agent-browser-debug`, `verify-gate`, `finalize`, `typescript`, `frontend-craft`, `vitest`, `echarts`, `prose-craft`, `dashfix`, `negafix`, `maintain-agents-md`, `commit-all`, `gh-switch`, `secret-hygiene`, `skill-crafting`, `session-learnings`, `transfer-context` |

Both Claude Code and Codex entries use a `url` source with a release tag `ref`: the
plugin manifests and `skills/` directory live at the root of each source repository. The plugin names are
`agentflow`, `skills`, and `cross-agent`.

A `git-subdir` source with `path: "."` is not used: Claude Code 2.1.322 installs only the
top-level files of the repository from it (no `skills/`).

Installation from these pins was checked on 2026-11-15 in throwaway configs: Claude Code
2.1.325 and Codex 0.169.0 install all three plugins with their skills (cross-agent 1,
skills 30, agentflow 11). Skill invocation inside the hosts and Antigravity remain
unverified; the host validation matrix is tracked in
[agentic-workflow issue 29](https://github.com/sentimony/agentic-workflow/issues/29).

`cross-agent` is a separate experimental plugin. Install it alongside `agentflow`
when using delegation with the workflow owner adapter. Basic delegation has no
workflow dependency. Installation was checked as above; invocation and provider
resume remain unverified, and the remaining evidence is tracked in
[agentic-workflow issue 31](https://github.com/sentimony/agentic-workflow/issues/31).

## Install

Claude Code:

```sh
claude plugin marketplace add sentimony/marketplace
claude plugin install agentflow@sentimony
claude plugin install skills@sentimony
claude plugin install cross-agent@sentimony
```

Codex:

```sh
codex plugin marketplace add sentimony/marketplace
codex plugin add agentflow@sentimony
codex plugin add skills@sentimony
codex plugin add cross-agent@sentimony
```

Antigravity (`agy` installs from the repository URL; the `/tree/<tag>` form pins the release tag):

```sh
agy plugin install https://github.com/sentimony/agentic-workflow/tree/v0.0.34
agy plugin install https://github.com/sentimony/skills/tree/v0.0.116
agy plugin install https://github.com/sentimony/cross-agent/tree/v0.0.14
```

Since `v0.0.23`, `session-learnings` (formerly in `agentflow`) and `transfer-context`
(formerly in `cross-agent`) ship in the `skills` plugin: update all three plugins together so
that neither skill disappears or is installed twice.

Since `v0.0.8`, `agentflow` replaces `aw`. The catalog contains one workflow entry,
`agentflow`. Update your marketplace catalog, then migrate an existing `aw` installation:

1. Claude Code:

   ```sh
   claude plugin uninstall aw@sentimony
   claude plugin install agentflow@sentimony
   ```

2. Codex:

   ```sh
   codex plugin remove aw@sentimony
   codex plugin add agentflow@sentimony
   ```

Since `v0.0.2`, `skills` holds every skill of sentimony/skills: the former `devflow`,
`writing`, `skill-crafting`, and `echarts` plugins are gone, so uninstall them
(`claude plugin uninstall devflow@sentimony` or
`codex plugin remove devflow@sentimony`, and so on) and install `skills`. To pick up a new
release, update the marketplace (`claude plugin marketplace update sentimony`) and reinstall.

## License

MIT
