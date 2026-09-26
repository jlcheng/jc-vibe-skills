# How I manage my skills and plugins

Written 2026-09-26. This is my plan, not a finished process. I expect to change it as I use it.

I use Claude Code and Codex, and I want the same skills in both. I install, update, and remove
them with `jc-plugin`, which runs each tool's own plugin commands for me.

## Where my skills live

| Place          | Repo                                                                       | What goes there                                                  |
| -------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Vibe           | `jlcheng/jc-vibe-skills` (`~/privprjs/jc-vibe-skills`), plugin `jc-vibe`   | Experiments I don't care much about. Most new skills start here. |
| Published      | `jlcheng/jc-agent-skills` (`~/privprjs/jc-agent-skills`), plugin `jc-code` | Skills I care enough about to publish.                           |
| The real world | Someone else's repo, e.g. `mattpocock/skills`                              | Plugins I use as they are.                                       |

I don't have a rule for vibe versus published. I decide each time. If I'm not sure, it goes in
vibe; I can promote it later.

## The commands

```
jc-plugin list                          # each plugin, with its version in Claude and in Codex
jc-plugin install <source> [plugin]     # source: owner/repo, a Git URL, or a local folder
jc-plugin update <plugin>               # Claude updates in place; Codex removes and re-adds
jc-plugin uninstall <plugin>            # removes it from both
```

`--dry-run` shows what `install`, `update`, or `uninstall` would run, without running it.
`list --all` also shows the plugins Codex installs on its own.

Sessions that are already open keep the old version. I start a new session to get the new one.

## Adding or changing one of my skills

1. Edit or add the skill folder under `plugins/<plugin>/skills/` in vibe or published.
2. Follow that repo's `CLAUDE.md`. Both repos make me raise the plugin version in the Claude and
   Codex manifests together. Without a new version, Claude may think nothing changed.
3. Commit and push to `main`. Both tools install from GitHub, so unpushed edits don't reach them.
4. First time: `jc-plugin install jlcheng/<repo> <plugin>`. After that: `jc-plugin update <plugin>`.
5. `jc-plugin list` should show the same new version for Claude and Codex.

## Promoting a skill from vibe to published

1. Move the skill folder from `jc-vibe-skills` to `jc-agent-skills`.
2. Remove its entry from `EXPERIMENTS.md` and add one to `VETTING.md`.
3. Raise the version of both plugins, push both repos.
4. `jc-plugin update jc-vibe`, then `jc-plugin update jc-code`.

Its name changes, from `/jc-vibe:<skill>` to `/jc-code:<skill>`. That's fine.

## Plugins and skills from the real world

Before installing, look at what the repo has. It depends on which catalogs it ships:

- **Both a Claude and a Codex catalog** (`.claude-plugin/marketplace.json` and
  `.agents/plugins/marketplace.json`): `jc-plugin install <owner/repo> [plugin]`.
- **Only a Claude catalog.** This is most repos. `jc-plugin` can't install these into both tools
  yet. Either install into Claude alone (`claude plugin marketplace add <source>`, then
  `claude plugin install <plugin>@<marketplace> --scope user`), or treat it like the next case.
- **No plugin catalog at all**, just skill folders. Vet the skills I want, then copy them into
  `jc-agent-skills` under a plugin named `jc-misc`. They show up as `/jc-misc:<skill>` in both
  tools. `jc-misc` doesn't exist yet; the first skill I copy in creates it.
