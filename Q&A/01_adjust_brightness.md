# Adjust Brightness in I3

## Overview

The i3 window‑manager does *not* include built‑in brightness control. You must rely on an external utility that manipulates the display back‑light or output brightness, and then bind key‑presses in your i3 configuration file to call that utility. Two widely used utilities are:

* `brightnessctl`; controls actual back‑light devices via sysfs; regarded as reliable.
* `xbacklight` (or related variants); adjusts output brightness via XRandR; works in some environments but may only *simulate* brightness (i.e., changes pixel values rather than the back‑light) and may not function on all hardware.

This tutorial will provide steps using brightnessctl (preferred) and also outline alternatives and caveats.

---

## Install the brightness‑control utility

Open a terminal and run:

```bash
sudo apt install brightnessctl
```

(If you use a different distribution, replace `apt` with your package‑manager, e.g., `dnf`, `pacman`, etc.)

Once installed, verify it works by running:

```bash
brightnessctl s +10%
brightnessctl s 10%-
```

The first command *increases* brightness by 10 %; the second *decreases* brightness by 10 %. This method sets the back‑light device rather than only adjusting pixel output.

**Note**: On some systems brightnessctl may require root privileges to access the back‑light device. You may need to configure appropriate permissions (e.g., udev rules or group membership) so that your normal user can adjust brightness without `sudo`.

---

## Locate your i3 configuration file

Typically the file is located at:

```
~/.config/i3/config
```

Open it in your preferred text editor (e.g., `nano`, `vim`, `gedit`) with appropriate permissions.

```bash
nvim ~/.config/i3/config
```

---

## Add key‑bindings for brightness control

Inside the i3 config file, add lines similar to the following **after** any existing key‑bindings section, for example:

```text
# Brightness control
bindsym XF86MonBrightnessUp  exec --no-startup-id brightnessctl set +10%
bindsym XF86MonBrightnessDown exec --no-startup-id brightnessctl set 10%-
```

Explanation:

* `bindsym` instructs i3 to bind a key‑symbol to a command.
* `XF86MonBrightnessUp` and `XF86MonBrightnessDown` correspond to the special brightness keys on many keyboards.
* `exec --no-startup-id` ensures i3 executes the command without creating a new startup item.
* `brightnessctl set +10%` increases by 10 %.
* `brightnessctl set 10%-` decreases by 10 %.

If your keyboard does *not* have dedicated brightness keys (or they are not recognised), you may bind alternate keys, for example:

```text
bindsym $mod+F6 exec --no-startup-id brightnessctl set +10%
bindsym $mod+F5 exec --no-startup-id brightnessctl set 10%-
```

Here `$mod` is your i3 modifier key (often the Windows key or Alt).

---

## Reload the i3 configuration

After saving the config file, instruct i3 to reload its configuration. Usually the key‑binding is:

```
$mod+Shift+r
```

This causes i3 to re‑read the config file and apply changes.

---

## Test the key‑bindings

Press the configured keys (e.g., brightness up and down) to verify that brightness changes. Confirm visually, and optionally run `brightnessctl g` to display the current brightness value.

If *nothing happens*, check the following:

* Are the key‑symbols `XF86MonBrightnessUp`/`Down` correctly recognised by X? Use `xev` to monitor key‑press events.
* Does brightnessctl succeed when run manually in a terminal (without sudo)? If it fails due to permissions, you must fix device permissions.
* Is your system using back‑light devices visible under `/sys/class/backlight/`? If none, utility may not have a target.

---

## Alternative method using xbacklight or light

If brightnessctl does not work on your hardware, you may fallback to other utilities. For example:

**Using xbacklight**:

```text
bindsym XF86MonBrightnessUp   exec xbacklight -inc 10
bindsym XF86MonBrightnessDown exec xbacklight -dec 10
```

**Caveat**: On many modern laptops, xbacklight will return an error like `No outputs have backlight property` because the display back‑light is not controlled via RandR but via ACPI.

**Using light** (another utility) example:

```text
bindsym XF86MonBrightnessUp   exec light -A 5
bindsym XF86MonBrightnessDown exec light -U 5
```

Where `-A` means add and `-U` means subtract percentage.
Note: The ‘light’ utility may be archived and not actively maintained.

---

## Permission and device‑access considerations

Because the back‑light device resides under `/sys/class/backlight/…`, you may run into permission errors when invoking brightnessctl without root.
Possible resolutions:

* Add your user to a group (e.g., `video`) that has permissions to write to the back‑light device.
* Add a udev rule to allow write access to the device for that group.
* Grant `brightnessctl` set‑uid or similar (less recommended for security).

---

## Troubleshooting; common issues

* **Keys not detected**: Use `xev` or `showkey` to verify that the brightness keys produce `XF86MonBrightnessUp`/`Down`. If they don’t, you must use the actual key‑symbol or map hardware keys via your desktop/user environment.
* **Brightness changes but looks like a filter**: If you used `xrandr --brightness …` rather than back‑light control, the effect may simply be dimming the image (not the back‑light) and colours may degrade.
* **Minimum brightness still too high**: On some laptops the lowest back‑light value is still quite bright. Some users set `--min-value` parameters or step down further.
* **Multiple displays/back‑light devices**: If you have multiple back‑light interfaces, you may need to specify the correct device. brightnessctl supports `--device=…`.

---
