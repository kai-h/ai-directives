# ai-directives

Personal AI tool configuration, synced across machines via this repo.

## Files

- `CLAUDE.md` — working memory loaded by Claude Code and Cowork
- `STYLE.md` — writing style guide referenced from CLAUDE.md via `@~/.claude/STYLE.md` import

## Setup on a new Mac

```bash
# Clone the repo
mkdir -p ~/Code
git clone git@github.com:kai-h/ai-directives.git ~/Code/ai-directives

# Symlink the files into ~/.claude so Claude Code reads them
mkdir -p ~/.claude
ln -s ~/Code/ai-directives/CLAUDE.md ~/.claude/CLAUDE.md
ln -s ~/Code/ai-directives/STYLE.md ~/.claude/STYLE.md

# Verify
ls -la ~/.claude/CLAUDE.md ~/.claude/STYLE.md
```

If `~/.claude/` already contains `CLAUDE.md` or `STYLE.md` as plain files (not symlinks), back them up first:

```bash
mv ~/.claude/CLAUDE.md ~/.claude/CLAUDE.md.bak 2>/dev/null
mv ~/.claude/STYLE.md ~/.claude/STYLE.md.bak 2>/dev/null
```

## Daily workflow

### Pull before you edit

At the start of any session where you might edit on the other Mac, pull the latest:

```bash
cd ~/Code/ai-directives
git pull
```

### Commit after you edit

Git tracks changes in two phases: first you stage which changes to include in the next commit (`git add`), then you commit them (`git commit`). Without staging, `git commit` has nothing to act on.

For modifying files that are already tracked in the repo (the most common case):

```bash
git commit -am "describe the change" && git push
```

The `-a` flag auto-stages all tracked files that have been modified. The `-m` flag provides the commit message inline so git doesn't drop you into an editor.

For adding brand new files (e.g. a new directive file, a `memory/` subdirectory):

```bash
git add -A && git commit -m "describe the change" && git push
```

`-A` stages everything: new files, modifications, and deletions.

### Useful one-liners

```bash
# See what's changed since the last commit
git status

# See exactly what's changed in a file
git diff CLAUDE.md

# See the commit history for a file
git log --oneline CLAUDE.md

# Undo uncommitted changes to a file
git restore CLAUDE.md

# Pull in changes from the other Mac that you haven't yet seen
git pull
```

## Convention for commit messages

Short, present-tense, imperative voice. Examples:

- `Add rule about en-dashes vs em-dashes`
- `Reorder CLAUDE.md sections; style guide now at end`
- `Document Guardz/SentinelOne/Check Point security stack`
- `Add memory directory for client-specific notes`

Avoid bare commits like `update` or `changes`. Future-you will want to know what you did without opening the diff.

## Authentication

Clones use SSH (`git@github.com:kai-h/ai-directives.git`), which requires a GitHub SSH key registered on each Mac. To set up on a new Mac:

```bash
ssh-keygen -t ed25519 -C "kai@automatica.com.au"
cat ~/.ssh/id_ed25519.pub  # copy the output
```

Then add the public key to github.com under Settings → SSH and GPG keys.

If you'd rather use HTTPS with a Personal Access Token cached in macOS Keychain, swap the clone URL to `https://github.com/kai-h/ai-directives.git`.
