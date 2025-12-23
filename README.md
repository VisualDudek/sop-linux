# sop-linux
Standard Operation Procedure framework for Linux.

## Terminal
The preferred terminal emulator is **Ghostty**.

To set Ghostty as the default terminal:
```sh
gsettings set org.gnome.desktop.default-applications.terminal exec 'ghostty'
gsettings set org.gnome.desktop.default-applications.terminal exec-arg ''
```

## Package Managers
The main package managers used in this documentation are:
- **apt** - Advanced Package Tool (Debian/Ubuntu)
- **brew** - Homebrew package manager
- **snap** - Snap package manager (cross-distribution)

### Homebrew Applications
- **bat** - A cat clone with syntax highlighting
- **copilot** - GitHub Copilot CLI
- **gh** - GitHub CLI
- **yazi** - Blazing fast terminal file manager

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
