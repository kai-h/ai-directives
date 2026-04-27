# ai-directives

Personal AI tool configuration, synced across machines via this repo.

## Files

- `CLAUDE.md` — working memory loaded by Claude Code and Cowork
- `STYLE.md` — writing style guide referenced from CLAUDE.md

## Setup on a new Mac

```bash
git clone git@github.com:kai-h/ai-directives.git ~/Code/ai-directives
mkdir -p ~/.claude
ln -s ~/Code/ai-directives/CLAUDE.md ~/.claude/CLAUDE.md
ln -s ~/Code/ai-directives/STYLE.md ~/.claude/STYLE.md
```

## Workflow

`git pull` at session start, edit files, then `git commit && git push` when done.
