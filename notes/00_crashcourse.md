# I3 Crashcourse

## Installing i3 on Debian

Open a terminal and run:

```bash
sudo apt update
sudo apt install i3 i3status i3lock dmenu
```

Explanation of packages:

* `i3`: the tiling window manager itself.
* `i3status`: shows a status bar (time, CPU, network, etc.).
* `i3lock`: screen locker.
* `dmenu`: a minimal application launcher (keyboard-driven).

After installation:

1. Log out of GNOME.
2. At the login screen, select **i3** as your session.
3. Log in; i3 will start in a default layout. The first time, it will ask:

   * Do you want a **default config**? (Choose yes)
   * Which **modifier key** to use? (`Mod1` = Alt, `Mod4` = Super/Windows key; Super is common)

---

## Initial Configuration

i3’s config file is usually at:

```
~/.config/i3/config
```

If it doesn’t exist, running i3 once will create a template.

**Key things to configure early:**

* **Mod key** (your main shortcut key; usually `Mod4`/Super).
* **Terminal emulator** (you can keep your favorite, like `alacritty` or `gnome-terminal`). Example:

```text
bindsym $mod+Return exec alacritty
```

* **Window splitting**: horizontal or vertical by default.
* **Workspace names**: optional, but helps organize multiple projects:

```text
set $ws1 "1: Dev"
set $ws2 "2: Web"
workspace $ws1 output HDMI-1
workspace $ws2 output eDP-1
```

---

## Crash Course: i3 Concepts

i3 is different from GNOME; think **“keyboard-controlled rectangles”** instead of floating windows.

### **Basic Controls (assuming Mod = Super)**

| Action                          | Shortcut                                                      |
| ------------------------------- | ------------------------------------------------------------- |
| Open terminal                   | `Mod+Enter`                                                   |
| Open dmenu (app launcher)       | `Mod+d`                                                       |
| Split vertical                  | `Mod+v`                                                       |
| Split horizontal                | `Mod+h`                                                       |
| Move focus to next window       | `Mod+j` (down), `Mod+k` (up), `Mod+h` (left), `Mod+l` (right) |
| Move window to another position | `Mod+Shift+<direction>`                                       |
| Switch workspace                | `Mod+1`, `Mod+2`, …                                           |
| Move window to workspace        | `Mod+Shift+<workspace number>`                                |
| Close window                    | `Mod+Shift+q`                                                 |
| Resize window                   | `Mod+r` (enters resize mode, then arrow keys)                 |
| Reload config                   | `Mod+Shift+c`                                                 |
| Lock screen                     | `Mod+Shift+x` (if bound)                                      |

---

### Tiling Concepts

* i3 divides your screen into a **tree of containers**.
* Each container can split **vertically or horizontally**.
* Windows “tile” automatically; no overlapping unless you want floating mode (`Mod+Shift+Space` toggles floating).

---

### Workflow Tips for Keyboard-Focused Users

* **Use tmux inside your terminal** for nested window management. i3 + tmux is insane productivity.
* **Learn dmenu or rofi** to launch apps instead of clicking icons.
* **Use workspaces per project** (Dev, Web, Media) and move windows around with keyboard shortcuts.
* **Configure i3status** to show useful info (battery, CPU, network) on your bar.

---

### Optional Extras

* Install `alacritty` or `kitty` if you want blazing fast, keyboard-centric terminals.
* Install `rofi` for a prettier app launcher:

```bash
sudo apt install rofi
```

Bind it in your config:

```text
bindsym $mod+d exec rofi -show run
```

* Consider `polybar` if you want a more customizable status bar.

---
