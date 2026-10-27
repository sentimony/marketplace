# marketplace

Public plugin marketplace of sentimony: one place to install Sentimony agent skills as Claude
Code and Codex plugins.

## Plugins

| Plugin | Source | Ref | What it holds |
| --- | --- | --- | --- |
| `aw` | [sentimony/agentic-workflow](https://github.com/sentimony/agentic-workflow) | `v0.0.8` | Agentic workflow for one change from request to merge: specify, plan-craft, implement, verify, cr-request, cr-received, finalize, session-learnings, cross-cr |
| `devflow` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.14` | Development workflow: scope triage, planning, plan execution, TDD, debugging, code review, verification, branch finishing |
| `writing` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.14` | Prose editing, plain hyphens, no negative parallelism |
| `skill-crafting` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.14` | Creating, evaluating, and tuning agent skills |
| `echarts` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.14` | Apache ECharts charts |
| `skills` | [sentimony/skills](https://github.com/sentimony/skills) | `v1.58.14` | Frontend, Vitest, TypeScript, agent context, secret hygiene, browser debugging, GitHub accounts, commits |

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

Install `devflow`, `writing`, `skill-crafting`, and `echarts` the same way. To pick up a new
release, update the marketplace (`claude plugin marketplace update sentimony`) and reinstall.

## License

MIT
