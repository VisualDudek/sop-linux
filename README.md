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
