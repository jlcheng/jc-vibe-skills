# jc-vibe-skills

A Claude Code plugin marketplace for experimental agent skills. Skills here are intentionally published before they are fully tested. Read [EXPERIMENTS.md](EXPERIMENTS.md) before installing or relying on one.

## Install

```
/plugin marketplace add jcheng/jc-vibe-skills
/plugin install jc-vibe@jc-vibe-skills
```

While developing locally:

```
/plugin marketplace add ~/privprjs/jc-vibe-skills
```

## Plugins

| Plugin | Purpose |
| -- | -- |
| `jc-vibe` | Experimental skills awaiting validation or promotion to `jc-agent-skills`. |

## Layout

```
.claude-plugin/marketplace.json      # marketplace: jc-vibe-skills
plugins/jc-vibe/
└── .claude-plugin/plugin.json       # plugin: jc-vibe, version 0.1.0
EXPERIMENTS.md                       # readiness and limitations for each skill
```

## Promotion

Once an experimental skill is tested and reviewed, move it to `jc-agent-skills`. Do not imply that a skill here is safe for production use.

## Change Log

### 0.1.0 — 2026-09-07

- First release: marketplace and empty `jc-vibe` plugin scaffold for experimental skills.
