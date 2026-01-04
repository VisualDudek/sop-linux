# sop-linux
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

## Package Managers
The main package managers used in this documentation are:
- **apt** - Advanced Package Tool (Debian/Ubuntu)
- **brew** - Homebrew package manager
- **snap** - Snap package manager (cross-distribution)

### Homebrew Applications
- **bat** - A cat clone with syntax highlighting
- **copilot** - GitHub Copilot CLI
- **fzf** - Command-line fuzzy finder
- **gh** - GitHub CLI
- **yazi** - Blazing fast terminal file manager

## CLI AI Agents
The recommended CLI AI agent is **Claude Code**.

Claude Code is Anthropic's official CLI tool that provides an interactive AI assistant for software engineering tasks, code analysis, and development workflows directly in your terminal.

## Shell Configuration

### fzf Integration with Zsh
**fzf** provides fuzzy finding capabilities for command history, file navigation, and more.

After installing fzf via Homebrew, enable zsh integration by adding to `~/.zshrc`:
```sh
# Enable fzf key bindings and fuzzy completion
source <(fzf --zsh)
```

**Key bindings:**
- `Ctrl+R` - Search command history
- `Ctrl+T` - Search files and directories
- `Alt+C` - Change directory using fuzzy search

## Backup
Use Borg. Automate backups with systemd timers and borg docs bash script `dobackup.sh`.
`*.service` and `*.timer` files are in the `~/.config/systemd/user/` folder.

check example cnf files [here](./borg-cnf/)

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

## Tips

### Find which package provides a file
To find which apt package is responsible for a given file:
```sh
dpkg -S "$(command -v gh)"
```

**Why `command -v` over `which`?**
- `command -v` is a POSIX-standard shell builtin, making it faster and more portable
- `which` is an external program that may not be installed or may behave differently across systems
- `command -v` respects shell aliases and functions, providing more accurate results

### List installed packages
To list all installed packages:
```sh
dpkg -l
```
This displays all installed packages with their status, version, and description.
