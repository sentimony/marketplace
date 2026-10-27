# marketplace

Public plugin marketplace of sentimony: one place to install Sentimony agent skills as Claude
Code and Codex plugins.

## Plugins

| Plugin | Source | Ref | What it holds |
| --- | --- | --- | --- |
| `aw` | [sentimony/agentic-workflow](https://github.com/sentimony/agentic-workflow) | `v0.0.9` | Agentic workflow for one change from request to merge: specify, plan-craft, implement, verify, cr-request, cr-received, finalize, session-learnings, cross-cr |
| `skills` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.16` | All 28 skills of sentimony/skills: scope triage, planning, plan execution, TDD, debugging, code review, verification, branch finishing, prose editing, plain hyphens, no negative parallelism, skill crafting, Apache ECharts, frontend, Vitest, TypeScript, agent context, secret hygiene, browser debugging, GitHub accounts, commits |

## Install

Claude Code:

```sh
claude plugin marketplace add sentimony/marketplace
claude plugin install aw@sentimony
claude plugin install skills@sentimony
```

Codex:

```sh
codex plugin marketplace add sentimony/marketplace
codex plugin add aw@sentimony
codex plugin add skills@sentimony
```

Since `v0.0.2`, `skills` holds every skill of sentimony/skills: the former `devflow`,
`writing`, `skill-crafting`, and `echarts` plugins are gone, so uninstall them
(`claude plugin uninstall devflow@sentimony` or
`codex plugin remove devflow@sentimony`, and so on) and install `skills`. To pick up a new
release, update the marketplace (`claude plugin marketplace update sentimony`) and reinstall.

## License

MIT
