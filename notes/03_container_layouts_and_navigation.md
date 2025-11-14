# Container layouts and navigation

## Vertical and horizontal splits

i3’s spatial composition engine operates through explicit split directives that determine how new windows integrate into the container tree.

* **Vertical split** (`$mod+v`):
  Injects the next window into a container arranged along the vertical axis, producing left/right partitions.
* **Horizontal split** (`$mod+h`):
  Inserts the next window along the horizontal axis, producing top/bottom partitions.

Focus traversal uses a directional navigation model:

* `$mod+j`; move focus left
* `$mod+k`; move focus down
* `$mod+l`; move focus up
* `$mod+semicolon`; move focus right

This model ensures deterministic navigation independent of pixel geometry, reinforcing cognitive consistency across sessions.

---

## Container layout modes

i3 provides three principal layout schemas, each optimized for different workload patterns:

1. **Default (splith/splitv)**

   * Windows share space proportionally, following the current split orientation.
   * Ideal for analytical workflows requiring simultaneous visibility (e.g., logs + editor + terminal matrix).

2. **Stacking mode** (`$mod+s`)

   * Surfaces collapse into a vertical list with only the active window visible.
   * Maximizes screen space for content-dense applications while preserving quick access to secondary tasks.

3. **Tabbed mode** (`$mod+w`)

   * Windows appear as tabs across the top of the container.
   * Well-suited for multi-step processes requiring frequent context switches without spatial fragmentation.

Layout cycling (`$mod+e`) provides rapid reconfiguration during exploratory work.

---

## Window mobility, resizing, and floating mode

Operational agility in i3 depends on mastering container manipulation.

**Move windows**

* `$mod+Shift+h/j/k/l`; relocate the focused container directionally.
  This rewires the tree structure, enabling deliberate architecture of workspace topology.

**Resize containers**

* `$mod+r` enters resize mode; directional keys adjust container dimensions.
  This mode provides precise resource reallocation across competing windows, aligning with task priority.

**Toggle floating mode** (`$mod+Shift+Space`)

* Converts a tiled container into a floating surface with manual positioning.
* Use cases include transient utilities (dialogs, communication apps, reference material) that do not fit into the tiling schema.
* `$mod+Left/Right/Up/Down` can move floating windows; mouse dragging is also enabled.

Floating is a tactical override mechanism; used sparingly when tiling geometry becomes counterproductive.

---
