# I3 Roadmap

## Core Fundamentals

### Installation and initial session

* Understand how to install i3 via your distro’s package manager.
* Recognise what session files (e.g., `i3.desktop`) exist and how your display manager picks up i3.
* On first login with i3, learn how to choose your modifier key (`$mod`, usually Super or Alt).

### Basic concepts of i3

* Understand that i3 is a *tiling window manager*: windows are arranged in non-overlapping containers.
* Know what a **workspace** is (virtual desktop), how to switch between them, and move windows to them.
* Get familiar with the default keybindings: e.g., `$mod+Enter` to open a terminal, `$mod+Number` to switch workspace.

### Container layouts & navigation

* Learn how windows split vertically/horizontally and how focus moves between them (e.g., `$mod+j/k/h/l`).
* Understand container modes: default (equal split), stacking, tabbed.
* Practice moving windows, resizing, toggling floating mode for when tiling isn’t ideal.

---

## Configuration and Usage Fluency

### Config file and keybindings

* Locate and edit your config: typically `~/.config/i3/config`.
* Set your `$mod` if you want (Super/Windows key is common) and define custom keybindings for your favourite apps.
* Map your terminal emulator.

### Workspaces and application assignment

* Name workspaces meaningfully (e.g., “1:Dev”, “2:Web”, “3:Chat”) and switch between them quickly.
* Assign certain applications to always open in specific workspaces via config rules (`assign [class="..."] 2:Web`).

### Status bar and system integration

* Use `i3status`, `i3blocks`, or alternatives to show system info (CPU, memory, network) in the bar.
* Integrate locking (`i3lock`), screen brightness, suspend/hybernate, etc.
* Consider launching `rofi` or `dmenu` for app launching (`$mod+d`).

### Aesthetic and workflow refinement

* Tweak colours, fonts, window borders to your taste; customize the look.
* Use compositors (`picom`, etc.) for effects (optional).
* Eliminate mouse dependency: aim to do almost everything with the keyboard.

---

## Advanced Features and Efficiency

### Multi-monitor setups

* Understand output handling, mapping workspaces to monitors, dealing with monitor connect/disconnect events.
* Configure in your config file `workspace X output __` etc.

### IPC / scripting / automation

* i3 supports IPC (JSON-based) and you can script behavior (window movements, layouts) programmatically.
* Create automation for your workflows: e.g., open dev environment across multiple workspaces with one keybinding.

### Layouts and advanced window management

* Use split orientation changes mid-workflow, switch between layouts (stacked/tabbed/tiled) dynamically.
* Mark windows, jump to them, and use more advanced focus rules.

### Integration with your stack

* If you use `nvim` and `tmux` for example, map these to workspaces and keybindings so your environment flows.
* For example: workspace “Dev” opens `alacritty` (or your terminal) with `tmux`, split to editor, logs, REPL.
* Launch `nvim` in full keyboard mode; i3 should complement that (no distractions).

### Maintenance and best practices

* Keep your config modular: split into includes, use comments, version-control your config (e.g., Git).
* Backup your config and document your keybindings for yourself.
* Review performance: i3 is light, but monitor for issues like screen tearing, missing shortcuts etc.

---

## Expert Level / Customization for Power Users

### Fully customised bar and desktop “rice”

* Replace `i3bar` with `polybar` or highly customised bar for status, icons, animations.
* Custom themes, icons, fonts, transparent terminals, neat visuals; purely aesthetic but satisfying.
* Setup application launcher skins, window gaps (via forks like `i3-gaps`), animations.

### Deep scripting and external tools

* Write scripts that manage window layout based on project: project-specific workspace setup, automated startup.
* Use i3’s IPC socket for integration with notification daemons, status scripts.
* Investigate WM event hooks, workspace naming conventions, conditional configs.

### Wayland transition / alternate WMs

* Although you’re on X11 via Debian now, explore the possibility of moving to Sway (Wayland-compatible) which uses many of the same config features.
* Understand the pros/cons of tiling WMs vs full desktop environments in context of performance, multi-monitor, GPU usage.

---
