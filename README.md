# dotconfig

Personal `~/.config` managed with git. Allowlist-based `.gitignore` — everything is ignored by default, only explicitly included dirs are tracked.

## What's tracked

| Directory | Description |
|-----------|-------------|
| `fish/` + `omf/` | Fish shell + Oh My Fish |
| `ghostty/` | Ghostty terminal |
| `nvim/` | Neovim (submodule) |
| `gh/` | GitHub CLI |
| `opencode/` | OpenCode plugins & skills |

## Setup

```bash
git clone --recurse-submodules <repo-url> ~/.config
```

If already cloned without submodules:

```bash
git submodule update --init --recursive
```

## Tracking a new directory

Add two lines to `.gitignore`:

```gitignore
!newdir/
!newdir/**
```

Then `git add newdir/` and commit.
