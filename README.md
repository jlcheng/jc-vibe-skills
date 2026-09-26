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
| `jc-vibe` | Experimental skills awaiting validation or promotion to `jc-agent-skills`. Skills: `wrangler` (plugin and standalone installation, inventory, placement, and testing in both tools). |

## Layout

```
.claude-plugin/marketplace.json      # Claude marketplace: jc-vibe-skills
.agents/plugins/marketplace.json     # Codex marketplace: jc-vibe-skills
plugins/jc-vibe/
├── .claude-plugin/plugin.json       # plugin: jc-vibe, version 0.4.1
├── .codex-plugin/plugin.json        # same plugin, for Codex, version 0.4.1
└── skills/
    └── wrangler/                    # manage skills and plugins with jc-plugin
        ├── SKILL.md
        ├── workflow.md              # John's write-up of the workflow wrangler follows
        ├── testing.md               # standalone and plugin behavior testing in both tools
        └── agents/openai.yaml       # Codex: explicit invocation only
EXPERIMENTS.md                       # readiness and limitations for each skill
```

## Promotion

Once an experimental skill is tested and reviewed, move it to `jc-agent-skills`. Do not imply that a skill here is safe for production use.

## Change Log

### 0.4.1 — 2026-09-26

- Ask for an unresolved skill home or plugin selection before choosing one. Independent
  behavior review found that both tools sometimes treated a placement question as a vibe choice.

### 0.4.0 — 2026-09-26

- Add standalone skill testing in both tools without plugin packaging or publication.
- Distinguish plugin state from individual skills, instructional requests from actions, and
  temporary testing from long-term placement. Document fresh-session behavior verification.
- Behavioral validation is in progress; see EXPERIMENTS.md for the exact current limits.

### 0.3.2 — 2026-09-26

- Correct `wrangler` to use `jc-plugin` for Claude-only catalogs too, based on John's
  successful installation and removal of Matt Pocock's plugin in both tools.

### 0.3.1 — 2026-09-26

- Teach `wrangler` that Codex accepts Claude catalogs and plugin manifests, and distinguish
  that support from the current `jc-plugin` preflight limitation.

### 0.3.0 — 2026-09-26

- `wrangler` now reads John's write-up of his workflow (`workflow.md`), checks someone else's repo
  itself before advising, and covers skills that come with no plugin catalog: vet them, then copy
  them into a new `jc-misc` plugin in `jc-agent-skills`.

### 0.2.1 — 2026-09-26

- `wrangler` now runs only when invoked by name, in both Claude Code and Codex.

### 0.2.0 — 2026-09-26

- Codex support: added a Codex marketplace and plugin manifest.
- New skill `wrangler`: guides adding, promoting, installing, updating, and removing skills and
  plugins across Claude Code and Codex with `jc-plugin`.

### 0.1.0 — 2026-09-07

- First release: marketplace and empty `jc-vibe` plugin scaffold for experimental skills.
