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
| `jc-vibe` | Experimental skills awaiting validation or promotion to `jc-agent-skills`. Skills: `wrangler` (plugin and standalone installation with source and intent checks, inventory, placement, and testing the intended skill in both tools). |

## Layout

```
.claude-plugin/marketplace.json      # Claude marketplace: jc-vibe-skills
.agents/plugins/marketplace.json     # Codex marketplace: jc-vibe-skills
plugins/jc-vibe/
├── .claude-plugin/plugin.json       # plugin: jc-vibe, version 0.4.10
├── .codex-plugin/plugin.json        # same plugin, for Codex, version 0.4.10
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

### 0.4.10 — 2026-09-26

Keep installation questions read-only, resolve multi-plugin choices before giving install commands, and leave an unnamed draft’s identity and home undecided.

### 0.4.9 — 2026-09-26

Use the installed plugin’s actual namespace when testing skills, so a duplicate short name or a different source folder does not mislead stale-copy diagnosis.

### 0.4.8 — 2026-09-26

Ask for unresolved ownership before selecting a home, distinguish install sources from installed identities, and keep test evidence in unique directories.

### 0.4.7 — 2026-09-26

Preserve the chosen skill home and installation scope; distinguish plugin absence from missing standalone skills and retain complete standalone folders.

### 0.4.6 — 2026-09-26

Apply source-file preflight to installation actions as well as advice, and execute explicit installation requests even when the plugin is already listed.

### 0.4.5 — 2026-09-26

Verify referenced files directly before diagnosing missing skill resources from an incomplete inventory.

### 0.4.4 — 2026-09-26

Wrangler distinguishes an installation source from the installed plugin identity and checks complete manifests and referenced skill paths before giving install instructions.

### 0.4.3 — 2026-09-26

- Distinguish explicit-only skills from disabled skills, and apply Claude overrides only to
  the skill kinds they actually control. Ground inventory in full discovery and avoid guessing
  configuration history.
- Use current Codex permission flags for tests and retain evidence before cleaning scratch state.

### 0.4.2 — 2026-09-26

- Finish installation actions with harmless skill loading and behavior checks in both tools.
- Account for individual disabled skills in inventory, and keep generic testing advice scoped
  to the user's candidate rather than assuming Wrangler itself is being tested.

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
