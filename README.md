# marketplace

Public plugin marketplace of sentimony: one place to install Sentimony agent skills as Claude
Code and Codex plugins.

Version: `v0.0.15`

## Plugins

| Plugin | Version | Skills |
| --- | --- | --- |
| [cross-agent](https://github.com/sentimony/cross-agent) | 0.0.7 | `cross-agent`, `transfer-context` |
| [agentic-workflow](https://github.com/sentimony/agentic-workflow) | 0.0.24 | `resolve-issue`, `specify`, `plan-craft`, `implement`, `verify`, `cr-request`, `cr-received`, `finalize`, `session-learnings` |
| [skills](https://github.com/sentimony/skills) | 0.0.103 | `scope-triage`, `doc-preview`, `plan-crafting`, `plan-execution`, `plan-orchestration`, `worktree-isolation`, `parallel-agents`, `tdd`, `review-request`, `cross-review`, `review-resolution`, `debugging`, `web-debug`, `webapp-debugger`, `verification-gate`, `branch-finish`, `typescript`, `frontend-crafting`, `vitest`, `echarts`, `prose-crafting`, `dashfix`, `negafix`, `agent-instructions`, `commit-all`, `gh-switch`, `secret-hygiene`, `skill-crafting` |

Both Claude Code and Codex entries use a `url` source with a release tag `ref`: the
plugin manifests and `skills/` directory live at the root of each source repository. The plugin names are
`agentflow`, `skills`, and `cross-agent`.

A `git-subdir` source with `path: "."` is not used: Claude Code 2.1.322 installs only the
top-level files of the repository from it (no `skills/`).

Installation from these pins was checked on 2026-11-10 in throwaway configs: Claude Code
2.1.322 and Codex 0.167.0 install all three plugins with their skills (cross-agent 2,
skills 28, agentflow 9). Skill invocation inside the hosts and Antigravity remain
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
agy plugin install https://github.com/sentimony/agentic-workflow/tree/v0.0.24
agy plugin install https://github.com/sentimony/skills/tree/v0.0.103
agy plugin install https://github.com/sentimony/cross-agent/tree/v0.0.7
```

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
