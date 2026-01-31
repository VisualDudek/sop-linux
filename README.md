<!-- markjkdownlint-disable MD013 -->
# SOP-linux TOC
<!-- mtoc-start -->

* [Terminal](#terminal)
* [Text Editor](#text-editor)
  * [Neovim Keymap](#neovim-keymap)
* [Package Managers](#package-managers)
  * [Homebrew Applications](#homebrew-applications)
* [Git & GitHub](#git--github)
* [CLI AI Agents](#cli-ai-agents)
* [Shell Configuration USE ZSH-omz](#shell-configuration-use-zsh-omz)
  * [fzf Integration with Zsh](#fzf-integration-with-zsh)
* [Yazi File Manager](#yazi-file-manager)
* [Backup, use Borg](#backup-use-borg)
  * [tips with `systemctl` unit files](#tips-with-systemctl-unit-files)
  * [tips with `journalctl`](#tips-with-journalctl)
* [Tips](#tips)
  * [Find which package provides a file](#find-which-package-provides-a-file)
  * [List installed packages](#list-installed-packages)

<!-- mtoc-end -->
Standard Operation Procedure framework for Linux.

## Terminal

The preferred terminal emulator is **Ghostty**.

To set Ghostty as the default terminal:

```sh
gsettings set org.gnome.desktop.default-applications.terminal exec 'ghostty'
gsettings set org.gnome.desktop.default-applications.terminal exec-arg ''
```

## Text Editor

The recommended text editor is **Neovim**.

Install Neovim via Homebrew:

```sh
brew install neovim
```

### Neovim Keymap

* search current buffer lines `<leader>sb`

## Package Managers

The main package managers used in this documentation are:

* **apt** - Advanced Package Tool (Debian/Ubuntu)
* **brew** - Homebrew package manager
* **snap** - Snap package manager (cross-distribution)

### Homebrew Applications

* **bat** - A cat clone with syntax highlighting
* **copilot** - GitHub Copilot CLI
* **fzf** - Command-line fuzzy finder
* **gh** - GitHub CLI
* **yazi** - Blazing fast terminal file manager
* ripgrep - alias `rg`
* **zoxide** - alias `z`

## Git & GitHub

* zsh alias `gd = git diff`
* zsh alias push `gp = git push`
* zsh alias pull `gl = git pull`
* git diff for specific file, working tree vs last commit `git diff file1 ...`

## CLI AI Agents

The recommended CLI AI agent is **Claude Code**.
Claude Code is Anthropic's official CLI tool that provides an interactive AI assistant for software engineering tasks, code analysis, and development workflows directly in your terminal.

## Shell Configuration USE ZSH-omz

Navigation using `zoxide`:
`z foo<SPACE><TAB> # show interactive completion`

Based on `robyrussel` custom prompt adding number of jobs in background if any

```sh
# Define the jobs indicator: shows only if jobs > 0
# %j is the number of jobs, %1(j.X.Y) is a conditional: if jobs >= 1, show X, else Y.
# %(1j.true.false): This is a Zsh ternary expression. It checks if there is at least 1 job (j).
PROMPT_JOBS='%(1j.%{$fg[yellow]%}⚙ %j %{$reset_color%}. )'

PROMPT="%(?:%{$fg_bold[green]%}%1{➜%} :%{$fg_bold[red]%}%1{➜%} )"
PROMPT+="${PROMPT_JOBS}"
PROMPT+="%{$fg[cyan]%}%c%{$reset_color%}"
PROMPT+=' $(git_prompt_info)'

ZSH_THEME_GIT_PROMPT_PREFIX="%{$fg_bold[blue]%}git:(%{$fg[red]%}"
ZSH_THEME_GIT_PROMPT_SUFFIX="%{$reset_color%} "
ZSH_THEME_GIT_PROMPT_DIRTY="%{$fg[blue]%}) %{$fg[yellow]%}%1{✗%}"
ZSH_THEME_GIT_PROMPT_CLEAN="%{$fg[blue]%})"
```

### fzf Integration with Zsh

**fzf** provides fuzzy finding capabilities for command history, file navigation, and more.

After installing fzf via Homebrew, enable zsh integration by adding to `~/.zshrc`:

```sh
# Enable fzf key bindings and fuzzy completion
source <(fzf --zsh)
```

**Key bindings:**

* `Ctrl+R` - Search command history
* `Ctrl+T` - Search files and directories
* `Alt+C` - Change directory using fuzzy search

## Yazi File Manager

`t` open a new tab
`[ / ]` navigate between tabs
`z` jump to a file/dir via fzf
`Z` jump to dir via zoxide
`gh` go home
`gc` go config dir
`<leader>sB` grep open buffers

## Backup, use Borg

Use Borg. Automate backups with systemd timers and borg docs bash script `dobackup.sh`.
`*.service` and `*.timer` files are in the `~/.config/systemd/user/` folder.

check example cnf files [check here](./borg-cnf/)

usage:

```sh
borg info
borg list
```

### tips with `systemctl` unit files

To manage user-level systemd services and timers, use the `--user` flag with `systemctl`. For example:

```sh
systemctl --user list-timers
systemctl --user status mybackup.timer

# Reload user systemd units after making changes
systemctl --user daemon-reload
```

### tips with `journalctl`

By default, `journalctl` shows logs in **pager** mode (by default `less`). To view logs without pagination, use the `--no-pager` option.

Example usage:

```sh
# tail-like behavior to follow logs in real-time
journalctl -f 

# jump to the end of the logs
journalctl -e
```

There are **journal fields** that can help filter logs for specific command name or PID.

```sh
journalctl _COMM=borg
```

## Tips

### Find which package provides a file

To find which apt package is responsible for a given file:

```sh
dpkg -S "$(command -v gh)"
```

**Why `command -v` over `which`?**

* `command -v` is a POSIX-standard shell builtin, making it faster and more portable
* `which` is an external program that may not be installed or may behave differently across systems
* `command -v` respects shell aliases and functions, providing more accurate results

### List installed packages

To list all installed packages:

```sh
dpkg -l
```

This displays all installed packages with their status, version, and description.
