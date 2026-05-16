# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## GitHub Repository

Remote: https://github.com/fmwichmann/KnowledgeBase

## Autonomous Commit Workflow

After every meaningful change (new file, edit, deletion), Claude Code commits automatically. Push requires manual approval by the user.

**Rules:**
- Commit after every change — do not batch unrelated changes into one commit
- Do not push automatically — ask the user before pushing
- Write concise commit messages that describe what changed and why
- Never use `--no-verify` or force-push to main

**Standard sequence after a change:**
```
git add <changed-files>
git commit -m "short description"
# Push only after user approval
```

**To revert a specific commit:**
```
git revert <commit-hash>
```

**To view history:**
```
git log --oneline
```

## Decision Workflow

When the user makes a design decision, Claude Code derives and documents it in two steps:

**1. Create an ADR** in `decisions/ADR-NNN.md`:
- Use the next available ID (check existing files)
- Sections: Kontext, Alternativen, Entscheidung, Konsequenzen
- List all considered alternatives, not just the chosen one
- Link to related REQs and ADRs in the frontmatter

**2. Create or update a REQ** in `requirements/REQ-NNN.md`:
- One requirement per decision outcome that imposes a system constraint
- Use SOPHIST MASTeR style: muss / soll / kann
- Link back to the ADR that justifies it

**Rules:**
- Always present alternatives before documenting a decision — never jump straight to the ADR
- If a decision touches an existing REQ, update its `links:` frontmatter to include the new ADR
- Check bidirectional links: ADR → REQ and REQ → ADR must both reference each other
- After creating ADR + REQ, run a brief consistency check: are all ADRs covered by at least one REQ?
