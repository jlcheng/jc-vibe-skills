---
name: wrangler
description: Walk through adding, promoting, installing, updating, and removing skills and plugins in Claude Code and Codex.
disable-model-invocation: true
---

# Wrangler

[workflow.md](workflow.md) is John's own write-up of how he plans to manage skills and plugins
across Claude Code and Codex. Read it first, then help him through whichever step he is on. Speak
plainly and offer one step at a time.

- When a new skill comes up, ask which place it belongs in. If he isn't sure, suggest vibe. Don't
  push him to decide more than that.
- When he names someone else's repo, look at it yourself before advising: which catalogs it ships,
  which plugins they list, or whether it has only skill folders. Then say which case in the
  write-up it falls under.
- Check current state with `jc-plugin list` rather than assuming what is installed.
- If what you find contradicts the write-up, tell him, so he can update it.
