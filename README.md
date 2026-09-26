# jc-vibe-skills

A Claude Code and Codex plugin marketplace for experimental agent skills. Skills here are intentionally published before they are fully tested. Read [EXPERIMENTS.md](EXPERIMENTS.md) before installing or relying on one.

## Install

Into both Claude Code and Codex:

```
jc-plugin install jlcheng/jc-vibe-skills jc-vibe
```

## Plugins

| Plugin | Purpose |
| -- | -- |
| `jc-vibe` | Experimental skills awaiting validation or promotion to `jc-agent-skills`. Skills: `wrangler`. |

## Layout

```
.claude-plugin/marketplace.json      # Claude marketplace: jc-vibe-skills
.agents/plugins/marketplace.json     # Codex marketplace: jc-vibe-skills
plugins/jc-vibe/
├── .claude-plugin/plugin.json       # plugin: jc-vibe, version 0.2.1
├── .codex-plugin/plugin.json        # same plugin, for Codex, version 0.2.1
└── skills/
    └── wrangler/                    # manage skills and plugins with jc-plugin
        ├── SKILL.md
        └── agents/openai.yaml       # Codex: explicit invocation only
EXPERIMENTS.md                       # readiness and limitations for each skill
```

## Promotion

Once an experimental skill is tested and reviewed, move it to `jc-agent-skills`. Do not imply that a skill here is safe for production use.

## Change Log

### 0.2.1 — 2026-09-26

- `wrangler` now runs only when invoked by name, in both Claude Code and Codex.

### 0.2.0 — 2026-09-26

- Codex support: added a Codex marketplace and plugin manifest.
- New skill `wrangler`: guides adding, promoting, installing, updating, and removing skills and
  plugins across Claude Code and Codex with `jc-plugin`.

### 0.1.0 — 2026-09-07

- First release: marketplace and empty `jc-vibe` plugin scaffold for experimental skills.
