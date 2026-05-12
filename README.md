# ebydash

A LazyGit-inspired terminal dashboard for developers. Shows git status, file changes, branches, VPN, system stats, Spotify, and Claude usage — all in one place.

## Preview

```
┌─[1] STATUS──────────────────────┐  ┌─[0] DIFF────────────────────────────────┐
│ myproject → feature/auth        │  │ --- a/src/auth.py                       │
│ origin/feature/auth  ↑2         │  │ +++ b/src/auth.py                       │
│                                 │  │ @@ -12,6 +12,8 @@                       │
├─[2] FILES───────────────────────┤  │ + def login(user, pwd):                 │
│ M  src/auth.py                  │  │ +     return check(user, pwd)           │
│ ?? tests/test_auth.py           │  ├─[5] SYSTEM──────────────────────────────┤
├─[3] BRANCHES────────────────────┤  │ CPU  ████████░░░░░░░░░░  42.3%          │
│ * feature/auth                  │  │ RAM  ███████████░░░░░░░░  61.0%         │
│ 2d  main              ✓         │  ├─[6] SPOTIFY─────────────────────────────┤
│ 5d  fix/login         ↓         │  │ ▶ Playing  Blinding Lights              │
├─[4] VPN─────────────────────────┤  │   The Weeknd                            │
│ ● Connected                     │  ├─[7] CLAUDE──────────────────────────────┤
│   Config: work-vpn              │  │ Claude Usage — Today                    │
└─────────────────────────────────┘  │   myproject    42.1k tok                │
                                     └─────────────────────────────────────────┘
```

## Requirements

- Python 3.9+
- [`textual`](https://github.com/Textualize/textual) — TUI framework
- [`psutil`](https://github.com/giampaolo/psutil) — for CPU/memory stats
- `git` — for git panes
- `playerctl` — optional, for Spotify controls
- `openvpn3` — optional, for VPN pane

## Installation

**1. Install dependencies**

```bash
pip install --user textual psutil
```

**2. Download the script**

```bash
curl -Lo ~/.local/bin/ebydash https://raw.githubusercontent.com/menporulporiayalan/ebydash/main/ebydash
chmod +x ~/.local/bin/ebydash
```

Make sure `~/.local/bin` is in your `PATH`:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

**3. Run it**

```bash
cd /your/git/project
ebydash
```

## Keybindings

| Key | Action |
|-----|--------|
| `q` | Quit |
| `r` | Force refresh |
| `1`–`7`, `0` | Jump to pane |
| **Branches pane** | |
| `↑` / `↓` | Move cursor |
| `Enter` | Checkout branch |
| `n` | New branch |
| `p` | Pull current branch |
| `P` | Push current branch |
| `m` | Pull main/master |
| **Files pane** | |
| `↑` / `↓` | Move cursor (updates diff preview) |
| `Space` | Stage / unstage file |
| `a` | Stage all files |
| `c` | Commit staged files |
| **VPN pane** | |
| `c` | Connect VPN |
| `d` | Disconnect VPN |
| **Spotify pane** | |
| `p` | Play / pause |
| `n` | Next track |
| `b` | Previous track |

## Panes

| # | Pane | Description |
|---|------|-------------|
| 1 | Status | Repo name, current branch, upstream sync |
| 2 | Files | Working tree changes with stage/unstage/commit |
| 3 | Branches | All local branches sorted by recency |
| 4 | VPN | OpenVPN3 session status |
| 5 | System | CPU and memory usage |
| 6 | Spotify | Now playing with playback controls |
| 7 | Claude | Today's token usage across projects |
| 0 | Diff | Live diff preview for selected file |

## Notes

- Run from inside any git repository directory
- VPN pane requires `openvpn3` CLI
- Spotify pane requires `playerctl`
- Claude pane reads `~/.claude/projects/` session logs
