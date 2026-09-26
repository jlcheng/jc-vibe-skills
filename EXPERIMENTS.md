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
- **jc-plugin checked (2026-09-26):** John's terminal output confirms that
  `jc-plugin install https://github.com/mattpocock/skills` installed version 1.2.3 in both
  tools, and `jc-plugin uninstall mattpocock-skills` removed it from both. This supersedes
  the earlier claim that `jc-plugin` required both catalogs.
- **Not tested:** Whether its advice holds up across a real promotion from vibe to published.
- **Limitations:** Local testing before pushing is not covered yet. The `jc-misc` plugin it recommends for copied
  skills doesn't exist yet.
- **0.3.0:** The workflow moved into `workflow.md`, written as John's own plan. The skill checks
  other people's repos itself.
- **Ready to promote:** No.

## Wrangler 0.4.0 verification in progress (2026-09-26)

Evidence directory: `/Users/jcheng/Downloads/wrangler-evidence/`, evaluator status in `STATUS.md`.
The original handoff is `/Users/jcheng/Downloads/handoff.txt`.

- Baseline on 0.3.2: actual fresh Claude Code 2.1.283 and Codex 0.157.1 sessions for installation
  advice, inventory, placement, testing advice, and standalone advice. Both tools omitted the
  other harness in testing advice; inventory guidance was incomplete. Raw transcripts retained.
- Harness mechanics: a standalone fixture with a relative JSON resource and Python script loaded
  through project `.claude/skills` and `.agents/skills` links; both produced the exact receipt.
  These fixture results establish standalone mechanics, not final Wrangler acceptance.
- Commands: `claude -p` with JSON event output, `codex exec --json`, `jc-plugin list`, local
  Python fixture script. Documentation and named public repositories are fetched over HTTPS;
  actual harness prompts use the configured model services. No secrets belong in evidence.
- 0.4.0 adds explicit cross-tool behavior testing and removes required jc-misc packaging for
  standalone usage. Existing historical claims above are not proof of 0.4.0 behavior.
- Outstanding: full final-candidate prompt matrix, real source/packaging action cells, state and
  failure variations, held-back paraphrases, cleanup checks, and independent evidence review.
  No claim of completion or promotion readiness. Not ready to promote.

### 0.4.1 decision correction

Independent review of 0.4.0 evidence found that both tools skipped the unresolved placement
question, and Codex offered multi-plugin commands without asking which plugin was intended.
0.4.1 clarifies these two decisions. Final-candidate acceptance remains in progress.

Further 0.4.0 evidence: actual Matt Pocock installation and removal in both tools via both
harnesses, plus harmless skill invocation in fresh Claude and Codex sessions. Claude's Humanizer
action inspected the full GitHub repository, copied complete standalone files into both project
discovery locations, and exercised both actual harnesses. Separate fact-preservation behavior
checks and final-candidate reruns are recorded in the evidence directory. A Claude standalone
test initially hit runner permission denials; it was retained as blocked and retried with a
session-only permission configuration for the authorized temporary workspace.

### 0.4.2 completion of installation checks

Review of 0.4.1 found that installation action sessions stopped at state/content checks for local
and dual-catalog plugins, leaving fresh-session behavior to the evaluator. Inventory also treated
some individually disabled skills as available. 0.4.2 corrects both behaviors and avoids assuming
Wrangler is the candidate in generic testing advice. Final acceptance is still unproven.

Supporting jc-plugin changes are published in privmono at a074bfd. Meaningful failing regression
tests preceded the GitHub-source equivalence fix; 25 tests, clippy and formatting pass. The built
~/bin/jc-plugin succeeds against real tools for shorthand with an existing HTTPS registration.
The earlier Claude-catalog fallback is published at a327a7c, with parent-failure evidence retained.
A transient Claude quota response was rechecked: later fresh sessions succeeded, so it is not
currently classified as a persistent external blocker.

### 0.4.3 discovery and test-run corrections

0.4.2 tests exposed confusion between automatic visibility and callable skills. Current Claude
skill documentation explicitly excludes plugin skills from `skillOverrides`; fresh init command
catalogs and successful explicit invocations confirmed that behavior in 2.1.283. Earlier test
responses subtracting nine same-named override entries from Matt's plugin were incorrect.
No existing overrides were edited. 0.4.3 clarifies the scope and avoids inferred change history.

Two Claude test orchestrations tried the retired Codex `--full-auto` flag before recovering.
The supported `-s workspace-write` example now appears directly in testing.md, with a reminder
to consult current help. Tests must preserve logs/artifacts before cleaning temporary discovery
state. Final 0.4.3 acceptance remains to be run; successful 0.4.2 actions are not presented as
proof of this candidate.
