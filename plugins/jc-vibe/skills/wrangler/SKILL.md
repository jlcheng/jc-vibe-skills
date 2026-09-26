---
name: wrangler
description: Guide John through managing his agent skills and plugins across Claude Code and Codex. Use when he wants to add, change, promote, install, update, remove, or list a skill or plugin, or asks where a skill should live.
---

# Wrangler

John keeps skills in three places and installs them into both Claude Code and Codex with
`jc-plugin`. Help him through whichever step he is on. Speak plainly and offer one step at a time.

## The three places

| Place          | Repo                                                                       | What goes there                                                                          |
| -------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Vibe           | `jlcheng/jc-vibe-skills` (`~/privprjs/jc-vibe-skills`), plugin `jc-vibe`   | Experiments he doesn't care much about. Most new skills start here.                      |
| Published      | `jlcheng/jc-agent-skills` (`~/privprjs/jc-agent-skills`), plugin `jc-code` | Skills he cares enough about to publish, plus other people's skills he copied in to vet. |
| The real world | Someone else's repo, e.g. `mattpocock/skills`                              | Plugins he uses as-is.                                                                   |

When a new skill comes up, ask which place it belongs in. If he isn't sure, suggest vibe; it can be
promoted later. Don't push him to decide more than that.

## The commands

```
jc-plugin list                          # each plugin, with its version in Claude and in Codex
jc-plugin install <source> [plugin]     # source: owner/repo, a Git URL, or a local folder
jc-plugin update <plugin>               # Claude updates in place; Codex removes and re-adds
jc-plugin uninstall <plugin>            # removes it from both
```

Add `--dry-run` to `install`, `update`, or `uninstall` to show the commands without running them.
`list --all` also shows the plugins Codex installs on its own.

After an install or update, sessions already open keep the old version. Tell him to start a new
session in each tool.

## Changing a skill in vibe or published

1. Edit or add the skill folder under `plugins/<plugin>/skills/`.
2. Follow that repo's `CLAUDE.md`. Both require raising the plugin version in
   `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json` together. Without a new version,
   Claude may think nothing changed.
3. Commit and push to `main`. Both tools install from GitHub, so unpushed edits don't reach them.
4. First time: `jc-plugin install jlcheng/<repo> <plugin>`. After that: `jc-plugin update <plugin>`.
5. `jc-plugin list` should show the same new version in both columns.

## Promoting a skill from vibe to published

Move the skill folder from `jc-vibe-skills` to `jc-agent-skills`, remove its `EXPERIMENTS.md` entry,
add a `VETTING.md` entry, and bump both plugins. Push both repos, then `jc-plugin update jc-vibe` and
`jc-plugin update jc-code`.

## Plugins from the real world

`jc-plugin install` needs the repo to list its plugins for both tools:
`.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`. Most repos only have the
Claude one. Check before installing. If it's Claude-only, the choices are:

- Install into Claude alone: `claude plugin marketplace add <source>`, then
  `claude plugin install <plugin>@<marketplace> --scope user`.
- Copy the skills he wants into `jc-agent-skills`. That's his vet-it-myself route, and it reaches
  Codex too.
