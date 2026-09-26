# Experiments

This is the record for skills in `jc-vibe`. 
For each skill, record:

- What it does and where it came from.
- What commands it runs and what it sends over the network.
- What has and has not been tested.
- Known limitations, failure modes, and the date it was last checked.
- Whether it is ready to promote to `jc-agent-skills`.

## wrangler

- **What it does:** Guides John through his skill workflow: which of his three places a skill
  belongs in (vibe, published, someone else's repo), and the `jc-plugin` commands to install,
  update, remove, and list plugins in Claude Code and Codex. Written by John and Claude on
  2026-09-26.
- **Invocation:** By name only (`/jc-vibe:wrangler`, `$jc-vibe:wrangler`); neither tool starts it on its own.
- **Commands and network:** The skill itself runs nothing. It suggests `jc-plugin`, `claude plugin`,
  `codex plugin`, and `git` commands, which fetch from GitHub when run.
- **Tested:** Installed through `jc-plugin` into both tools; a fresh session in each loaded it
  (2026-09-26).
- **Compatibility checked (2026-09-26):** Codex CLI 0.157.1 installed
  `mattpocock-skills@mattpocock` 1.2.3 from its Claude catalog and manifest. Individual skills
  were not executed.
- **Not tested:** Whether its advice holds up across a real promotion from vibe to published.
- **Limitations:** Describes `jc-plugin` as of 2026-09-26, whose preflight requires both catalogs even though Codex accepts Claude packaging.
  Local testing before pushing is not covered yet. The `jc-misc` plugin it recommends for copied
  skills doesn't exist yet.
- **0.3.0:** The workflow moved into `workflow.md`, written as John's own plan. The skill checks
  other people's repos itself.
- **Ready to promote:** No.
