# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## GitHub Repository

Remote: https://github.com/fmwichmann/KnowledgeBase

## Autonomous Commit & Push Workflow

After every meaningful change (new file, edit, deletion), Claude Code commits and pushes automatically so the full history is on GitHub and any state can be restored.

**Rules:**
- Commit after every change — do not batch unrelated changes into one commit
- Always push immediately after committing (`git push origin main`)
- Write concise commit messages that describe what changed and why
- Never use `--no-verify` or force-push to main

**Standard sequence after a change:**
```
git add <changed-files>
git commit -m "short description"
git push origin main
```

**To revert a specific commit:**
```
git revert <commit-hash>
git push origin main
```

**To view history:**
```
git log --oneline
```
