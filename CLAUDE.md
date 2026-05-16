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
