# Installation and initial session; i3

This document describes, in concise procedural form, the steps required to install the i3 tiling window manager, how display managers discover i3 session files, and how to select / change the i3 modifier key (`$mod`) during the first session and thereafter.

---

## Summary of concepts

* **Installation**: i3 is ordinarily installed from a distribution package; package names and package manager commands vary by distribution.
* **Session files**: Display managers (GDM, SDDM, LightDM, etc.) enumerate session `.desktop` files (commonly under `/usr/share/xsessions/`) to populate the session chooser; an `i3.desktop` file is created by the package to allow “i3” to appear in the login UI.
* **Modifier key (`$mod`)**: i3 uses a configurable modifier named `$mod`. The i3 first-run wizard prompts to choose between common options (Alt = `Mod1`, Super/Win = `Mod4`); the choice is written to the user config (usually `~/.config/i3/config`). You may edit the config later to change the mapping.

---

## Installing i3

Use your distribution’s package manager to install the i3 package. The following examples are canonical; adapt to your distro and to whether you want the core package, the `i3-gaps` fork, or helper packages (e.g., `i3status`, `i3lock`, `i3-wm`).

Debian / Ubuntu (APT):

```bash
sudo apt update
sudo apt install i3      # or i3-wm, or i3-gaps if available in your repo
# optional helpers:
sudo apt install i3status i3lock suckless-tools
```

Arch Linux / Manjaro (pacman):

```bash
sudo pacman -Syu
sudo pacman -S i3-wm i3status    # or i3-gaps from community/AUR if preferred
```

Fedora (DNF):

```bash
sudo dnf install i3
```

openSUSE (Zypper):

```bash
sudo zypper refresh
sudo zypper install i3
```

Notes:

* Package names vary (e.g., `i3`, `i3-wm`, `i3-gaps`). Consult your distribution repository if the name differs.

---

## How display managers detect i3 (session `.desktop` files)

1. **Location**
   Display managers list available X sessions by reading `.desktop` files in locations such as:

   * `/usr/share/xsessions/` (system-wide)
   * `/usr/local/share/xsessions/` (less common)
     A typical i3 package installs `/usr/share/xsessions/i3.desktop`. If that file is absent the display manager will not show “i3” in the session chooser.

2. **Typical `i3.desktop` contents** (minimal example)

   ```ini
   [Desktop Entry]
   Name=i3
   Comment=Dynamic tiling window manager
   Exec=i3
   TryExec=i3
   Type=Application
   DesktopNames=i3
   Keywords=tiling;wm;windowmanager;
   ```

   * `Exec` identifies the command run when the session is selected.
   * `TryExec` ensures the session is only offered if the binary exists.
     If your display manager’s session menu does not include i3, check for the presence and contents of the `.desktop` file in `/usr/share/xsessions/`. Reinstalling the distribution package will normally restore a missing file.

3. **Using an alternate startup command**
   You may create additional session entries that pass options or a specific config:

   ```ini
   Exec=i3 -c /home/username/.config/i3/custom-config
   ```

   This is useful for maintaining multiple session variants.

---

## First login with i3; the configuration wizard and selecting `$mod`

1. **First launch behavior**
   On the first login into an i3 session (i.e., when no user config exists at `~/.config/i3/config`), i3 runs an interactive configuration wizard. The wizard offers to generate a configuration file and prompts specifically to choose the modifier key (`Alt` / `Super` etc.). This generated file becomes the default writable user configuration.

2. **Choosing `$mod` during the wizard**

   * The wizard explicitly asks whether to use the `Mod1` (Alt) or `Mod4` (Super/Windows) key as the `$mod` key.
   * Choosing `Mod4` (Super) is common because it reduces collisions with application shortcuts; choosing `Mod1` (Alt) follows the upstream default in some installers.

3. **Result in the config file**
   The user config will contain a line similar to:

   ```text
   set $mod Mod4
   ```

   or

   ```text
   set $mod Mod1
   ```

   followed by keybindings that invoke `$mod`. The config is typically saved at:

   ```
   ~/.config/i3/config
   ```

   (or `~/.i3/config` on some installations / historical setups).

---

## Changing the modifier after first login

1. **Edit the config**
   Open `~/.config/i3/config` and change the `set $mod ...` line to the desired modifier symbol:

   ```text
   set $mod Mod4      # Super / Windows key
   # or
   set $mod Mod1      # Alt
   ```

   i3 recognizes X modifier names such as `Mod1` (Alt), `Mod4` (Super), or explicit keysyms like `Mod4`.

2. **Reload / restart i3**

   * Default generated configs include a keybinding to reload the configuration and to restart i3. Common defaults:
     * Reload config: `$mod+Shift+c`
     * Restart i3 in place: `$mod+Shift+r`
       Use those keybindings to apply the edited configuration; alternatively, log out and log in again. If you changed the `$mod` binding itself, use the alternative key (or restart session) to avoid being locked out.

3. **If the new `$mod` appears to be ignored**

   * Ensure the syntax in the config is correct and not being superseded by another config file.
   * Check whether a global remapping (XKB, desktop environment shortcuts) causes conflicts; some desktop environments or global key-mapping utilities may intercept the Super/Alt keys. Debug with `xev` / `xmodmap -pm`.

---

## Practical troubleshooting checklist

* **i3 does not appear in the session list**: verify `/usr/share/xsessions/i3.desktop` exists and contains a valid `Exec` and `TryExec`. Reinstall the package if necessary.
* **Wizard did not run / no config file created**: run `i3-config-wizard` manually, or copy a template to `~/.config/i3/config`.
* **Keybindings do nothing after changing `$mod`**: ensure you reloaded the config (or restarted i3) and that no other program intercepts the chosen modifier. Use `xmodmap -pm` and `xev` to inspect modifier mappings.

---
