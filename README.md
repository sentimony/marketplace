# marketplace

Public plugin marketplace of sentimony: one place to install Sentimony agent skills as Claude
Code and Codex plugins.

## Plugins

| Plugin | Source | Ref | What it holds |
| --- | --- | --- | --- |
| `agentflow` | [sentimony/agentic-workflow](https://github.com/sentimony/agentic-workflow) | `v0.0.18` | Nine workflow skills: resolve-issue, specify, plan-craft, implement, verify, cr-request, cr-received, finalize, session-learnings |
| `skills` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.18` | All 28 skills of sentimony/skills: scope triage, planning, plan execution, TDD, debugging, code review, verification, branch finishing, prose editing, plain hyphens, no negative parallelism, skill crafting, Apache ECharts, frontend, Vitest, TypeScript, agent context, secret hygiene, browser debugging, GitHub accounts, commits |
| `cross-agent` | [sentimony/cross-agent](https://github.com/sentimony/cross-agent) | `v0.0.1` | Experimental standalone delegation and consultation with persistent task and provider session identities |

All entries use `git-subdir` with `path: "."`: the plugin manifests and `skills/`
directory now live at the root of each source repository. The plugin names are
`agentflow`, `skills`, and `cross-agent`.

Native installation and discovery in Claude Code and Codex remain unverified for
these root layouts. The owner accepted this release exception; the host validation
matrix is tracked in [agentic-workflow issue 29](https://github.com/sentimony/agentic-workflow/issues/29).

`cross-agent` is a separate experimental plugin. Install it alongside `agentflow`
when using delegation with the workflow owner adapter. Basic delegation has no
workflow dependency. Native installation, invocation and provider resume
remain unverified; the remaining evidence is tracked in
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
