# How I manage my skills and plugins

Written 2026-09-26. AFA. This is my plan, not a finished process. I expect to change it as I use it.

I use Claude Code and Codex, and I want the same skills in both. I install, update, and remove them
with `jc-plugins`, which runs each tool's own plugin commands for me.

## Where my skills live

| Place | Repo | What goes there |
| -- | -- | -- |
| Vibe | `jlcheng/jc-vibe-skills` (`~/privprjs/jc-vibe-skills`), plugin `jc-vibe` | Experiments I choose to keep in vibe. |
| Published | `jlcheng/jc-agent-skills` (`~/privprjs/jc-agent-skills`), plugin `jc-code` | Skills I care enough about to publish. |
| The real world | Someone else's repo, e.g. `mattpocock/skills` | Plugins I use as they are. |

For skills created by me, they likely start as "vibe-coded skills" and live in jc-vibe-skills.
Having said that, I can totally see myself creating a skill in `jc-agent-skills` first.

For skills created by others, I will install them using `jc-plugins` if possible. Otherwise, I'll ask
AI to help me install them in both Codex and Claude Code.

## The commands

```
jc-plugins list                          # each plugin, with its version in Claude and in Codex
jc-plugins install <source> [plugin]     # source: owner/repo, a Git URL, or a local folder
jc-plugins update <plugin>               # Claude updates in place; Codex removes and re-adds
jc-plugins uninstall <plugin>            # removes it from both
```

`--dry-run` shows what `install`, `update`, or `uninstall` would run, without running it.
`list --all` also shows the plugins Codex installs on its own.

The `plugin@marketplace` value printed by `list` is an installed identity, not an installation
source. To add a missing installation, inspect its source and use `install <source> [plugin]`; for
example, `jc-plugins install https://github.com/mattpocock/skills mattpocock-skills`. Use the plugin
name for `update` and `uninstall`.

Sessions that are already open keep the old version. I start a new session to get the new one.

## Adding or changing one of my skills

1. Edit or add the skill folder under `plugins/<plugin>/skills/` in vibe or published.
2. Follow that repo's `CLAUDE.md`.
3. For a GitHub release, commit and push to `main`.
4. First time: `jc-plugins install jlcheng/<repo> <plugin>`. After that: `jc-plugins update <plugin>`.
5. `jc-plugins list` should show the same new version for Claude and Codex.

## Promoting a skill from vibe to published

1. Move the skill folder from `jc-vibe-skills` to `jc-agent-skills`.
2. Remove its entry from `EXPERIMENTS.md` and add one to `VETTING.md`.
3. Raise the version of both plugins, push both repos.
4. `jc-plugins update jc-vibe`, then `jc-plugins update jc-code`.

## Plugins and skills from the real world

Try to use `jc-plugins` -- It should work for skills shipped inside of plugins. Avoid using
`npx skills` -- I don't like how it loses a plugin's namespace.

If installing using `jc-plugins` fails, then fall back to using `npx skills`.

## Inventory and removal

`jc-plugins list` reports each plugin's version and enabled state separately for Claude and Codex. A
dash means missing; `(off)` means installed but disabled. Different versions or an installation in
only one tool are not availability in both. `list --all` includes bundled Codex plugins.

For removal instructions, show `jc-plugins uninstall <plugin>` and the verification command. When
asked to do it, run it, then inspect `jc-plugins list` for both tools. Remove only the requested
plugin; its marketplace registration may remain. For standalone skills, remove the requested copy or
link from the discovery location, preserving the source folder and unrelated skills.
