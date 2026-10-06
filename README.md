# 🛠️ Gitflux v6.0.0 — GitHub CLI Assistant

> A powerful, bilingual GitHub CLI assistant built for Termux — and any Linux environment.

## 🤔 Why Gitflux?

Gitflux combines 35+ Git and GitHub operations into a single, easy-to-remember CLI.
No more typing long Git commands or switching between `git` and `gh`.

Just run `gitflux deploy "fix: login bug"` and you're done. Humanity really looked at hundreds of Git commands and decided, "this is fine." Incredible species.

### Highlights

- 🚀 **One-command deploy** — stage, commit, push, and sync in a single step.
- 💾 **Backup all your repos** — store local copies without opening a browser.
- ⏪ **Undo anything** — uncommit, restore files, or reset entirely.
- 🔄 **Daemon mode** — auto-sync your repo every N seconds.
- 📊 **Stats** — see your commit history, lines of code, and top languages.
- 🧩 **Full GitHub API support** — manage gists, issues, PRs, releases, and actions.
- 🌐 **Bilingual** — English by default, Indonesian with `GITFLUX_LANG=id`.
- 🔒 **Input validation** — dangerous characters are blocked on all commands.

## 📦 Supported Platforms

| Platform | Status |
| --- | --- |
| Termux (Android) | ✅ Full Support |
| Linux (Ubuntu, Debian, Arch, Fedora) | ✅ Full Support |
| macOS | ✅ Full Support |
| Windows (Git Bash / MSYS2 / Cygwin) | ⚠️ Partial |

## ⚡ Quick Install

One command, and you're ready to go:

```bash
curl -sL https://raw.githubusercontent.com/Ziferd/Gitflux/main/Gitflux.sh -o $PREFIX/bin/gitflux && chmod +x $PREFIX/bin/gitflux
```

Then install the dependencies:

```bash
gitflux setup
```

🎉 Done. Type `gitflux help` to see all available commands.

> **Note:** On Linux/macOS without `$PREFIX`, replace `$PREFIX/bin` with `/usr/local/bin` and use `sudo`.

## 📋 Features Overview

### Core Git

- `deploy`
- `push`
- `pull`
- `sync`
- `status`
- `log`
- `diff`
- `stash`
- `tag`
- `remote`
- `init`

### Branch & Merge

- `branch` — create / switch / delete / rename
- `merge`
- `fetch`

### Rewrite History

- `reset` — soft / hard
- `reflog`
- `squash`
- `rebase`
- `cherry-pick`
- `bisect`

### GitHub API

- `repo` — create
- `clone`
- `gist`
- `issue`
- `pr`
- `release`
- `actions`

### Automation

- `backup` — all repos
- `stats`
- `daemon` — auto-sync
- `webhook`

### Setup & Config

- `setup`
- `config` — Git settings
- `undo`
- `keygen`
- `help`

## 📖 Command Reference

### Core Git

#### `gitflux deploy "message" [branch]`

Stage all files, commit, pull with `--rebase`, then push.

**Example:**

```bash
gitflux deploy "fix: login error"
```

#### `gitflux push [branch]`

Push the current branch to the remote.

**Example:**

```bash
gitflux push feature/login
```

#### `gitflux pull [branch]`

Pull the latest changes from the remote.

**Example:**

```bash
gitflux pull main
```

#### `gitflux sync [branch]`

Pull, then commit any local changes and push.

#### `gitflux status`

Show working tree status, current branch, and remote URL.

#### `gitflux log`

Show the last 20 commits as a graph.

#### `gitflux diff [target]`

Show changes between commits.

**Example:**

```bash
gitflux diff HEAD~2
```

#### `gitflux stash list|save|pop|drop`

Temporarily stash changes.

**Example:**

```bash
gitflux stash save "WIP: refactor"
```

#### `gitflux tag list|create|push|delete`

Manage tags.

**Example:**

```bash
gitflux tag create v1.2.0
```

#### `gitflux remote show|add|set|delete`

Manage remote URLs.

**Example:**

```bash
gitflux remote add upstream git@github.com:other/repo.git
```

#### `gitflux init [project]`

Create a new Git repo with README and `.gitignore` from scratch.

**Example:**

```bash
gitflux init my-awesome-project
```

### Branch & Merge

#### `gitflux branch list`

List all local and remote branches.

#### `gitflux branch create <name>`

Create and switch to a new branch.

**Example:**

```bash
gitflux branch create feat/oauth
```

#### `gitflux branch switch <name>`

Switch to an existing branch.

#### `gitflux branch delete <name>`

Delete a branch.

#### `gitflux branch rename <old> <new>`

Rename a branch.

#### `gitflux merge <branch>`

Merge a branch into the current branch.

#### `gitflux fetch`

Fetch all remote metadata.

### Rewrite History

#### `gitflux reset soft|hard [target]`

Reset `HEAD` to a specific commit. Hard reset requires confirmation.

#### `gitflux reflog`

Show the last 20 `HEAD` reference logs. Great for recovering lost commits.

#### `gitflux squash [count]`

Squash the last N commits into one. Validates that N doesn't exceed the total number of commits.

#### `gitflux rebase [branch]`

Rebase the current branch onto another branch.

#### `gitflux cherry-pick <commit>`

Apply a specific commit to the current branch.

#### `gitflux bisect start|good|bad|reset`

Binary search for a buggy commit. Tiny archaeological dig through your own mistakes. A timeless Git tradition.

### GitHub API

#### `gitflux repo <name> [public|private]`

Create a new GitHub repo and clone it locally.

#### `gitflux clone <user/repo>`

Clone a GitHub repo.

#### `gitflux gist list|create|edit|delete`

Manage GitHub Gists.

#### `gitflux issue list|create|close|view`

Manage Issues.

#### `gitflux pr list|create|merge|checkout|review`

Manage Pull Requests.

#### `gitflux release list|create|delete`

Manage Releases.

#### `gitflux actions list|watch|trigger`

Manage GitHub Actions workflows.

### Automation

#### `gitflux backup [folder]`

Back up all your GitHub repos locally. Runs in parallel for speed. Default folder: `~/gitflux-backups`.

#### `gitflux stats`

Show contribution stats: top committers, total lines of code, and dominant languages.

#### `gitflux daemon [seconds]`

Auto-sync the repo every N seconds in the background. Uses a PID-based lockfile to prevent duplicate instances. Default: 600 seconds.

#### `gitflux webhook`

Send a test ping to your `WEBHOOK_URL`.

### Setup & Config

#### `gitflux setup`

Auto-detect the package manager and install all dependencies (`git`, `gh`, `jq`, `curl`, `openssh`). Also runs `gh auth login` if not authenticated.

#### `gitflux config show|set|remote`

View or modify Git config settings.

**Examples:**

```bash
gitflux config set user.email you@example.com
gitflux config remote https://github.com/you/repo.git
```

#### `gitflux undo commit|file|hard`

Undo changes safely.

- `commit` — soft reset, keeps files staged.
- `file <name>` — restore a single file.
- `hard` — discard all changes (requires confirmation).

#### `gitflux keygen [email]`

Generate a new ED25519 SSH key for GitHub. Saves to `~/.ssh/id_ed25519_gitflux` and prints the public key.

#### `gitflux help`

Show the full command reference in your terminal.

## 🌐 Language / Bahasa

Gitflux speaks English by default.

To switch to Indonesian, set the environment variable:

```bash
export GITFLUX_LANG=id
```

Add that line to your `~/.bashrc` to make it permanent. Because typing the same export command forever is apparently how humans build character.

## ⚙️ Configuration

| Variable | Description | Default |
| --- | --- | --- |
| `GITFLUX_LANG` | Language (`en` or `id`) | `en` |
| `WEBHOOK_URL` | Webhook URL for notifications (Slack, Discord, etc.) | — |
| `GITHUB_USER` | Your GitHub username (speeds up clone) | — |

## 🆚 Comparison with `gh` CLI

| Feature | Gitflux | `gh` CLI |
| --- | --- | --- |
| One-command deploy | ✅ | ❌ |
| Backup all repos | ✅ | ❌ |
| Undo (commit / file / hard) | ✅ | ❌ |
| Squash, Rebase, Cherry-pick, Bisect, Reflog | ✅ | ❌ |
| Auto-sync (daemon) | ✅ | ❌ |
| Contribution stats | ✅ | ❌ |
| SSH key generator | ✅ | ❌ |
| Bilingual (EN / ID) | ✅ | ❌ |
| Input validation & sanitization | ✅ | ❌ |
| Gist / Issue / PR / Release / Actions | ✅ | ✅ |
| Repo create / Clone | ✅ | ✅ |

> **Total:** 35+ features — more powerful than `gh` CLI while staying lightweight.

## 🛠️ Troubleshooting

### `command not found` after install

Make sure `$PREFIX/bin` is in your `PATH`. Run `hash -r` or restart Termux.

### `gh: command not found`

Run:

```bash
gitflux setup
```

### `Not a Git repository`

You're not inside a Git repo. Navigate to one, or run:

```bash
gitflux init
```

### Deploy fails with merge conflicts

Gitflux won't force-push. Resolve conflicts manually, then run `deploy` again. Because Git believes suffering builds wisdom.

### `Karakter berbahaya terdeteksi` / `Dangerous character detected`

Your input contains characters like `;`, `&`, `|`, or `$` (except in commit messages). Clean the input and try again.

### Daemon won't start

A previous daemon may still be running. Check with:

```bash
cat /tmp/gitflux.lock
```

If necessary, delete the lockfile manually:

```bash
rm /tmp/gitflux.lock
```

## 🤝 Contributing

Pull requests are welcome!

If you have an idea for a new feature or found a bug, open an issue on GitHub.

## 📄 License

MIT © 2026 Ziferd

## 🧑‍💻 Developer

**Ziferd**  
GitHub: `@Ziferd`

> “Good tools make good developers. Build them, share them, improve them.”
