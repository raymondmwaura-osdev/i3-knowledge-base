# Basic concepts of i3; foundational architecture and operational semantics

## Tiling window management as the core execution model

i3 implements a deterministic tiling paradigm in which all application surfaces are allocated to non-overlapping containers. Each container participates in a hierarchical tree structure that dictates spatial composition (horizontal split, vertical split, tabbed, or stacked modes). This eliminates ad-hoc window placement and enforces a predictable spatial topology that enhances task throughput and reduces cognitive overhead during multi-application workflows.

Key points:

* Every window is a *node* in a managed container tree.
* Layout transitions occur through explicit user directives rather than pointer-driven manipulation.
* Screen real estate is treated as a finite asset subject to strict allocation logic.

---

## Workspaces as logical segmentation units

A workspace in i3 functions as a virtualized desktop environment; an isolated, named context that hosts an independent tree of containers. Workspaces enable horizontal task partitioning and reduce context-switch penalties.

Operational characteristics:

* Each workspace is addressable via a numeric or custom identifier.
* Only one workspace is rendered per monitor at a time, providing clean separation between workflows (e.g., code, browser, terminals, monitoring dashboards).
* Windows can be reassigned across workspaces, allowing dynamic load redistribution.

Core actions:

* **Switch workspace**: `$mod+NUMBER`
* **Move focused window to workspace**: `$mod+Shift+NUMBER`

This facilitates high-velocity transitions and enforces a scalable organizational model.

---

## Baseline keybinding schema

The default configuration (a strategic baseline optimized for operational efficiency) defines keybindings around the `$mod` variable (typically `Mod4`/Super for most deployments). These bindings act as high-leverage control functions for launching, navigating, and reorganizing windows.

Primary bindings:

* **Launch terminal**: `$mod+Enter`

  * Invokes the environment’s configured terminal emulator, accelerating access to shell resources.
* **Focus navigation**: `$mod+h/j/k/l` or arrow-key equivalents

  * Moves focus across containers following the directional model.
* **Split orientations**:

  * Horizontal: `$mod+h` (depending on config)
  * Vertical: `$mod+v`
* **Container layout modes**: `$mod+e` (toggle split modes), `$mod+s` (stacking), `$mod+w` (tabbed)
* **Workspace operations**: `$mod+NUMBER` (switch), `$mod+Shift+NUMBER` (move window)

These bindings create a deterministic control layer that eliminates pointer latency and enables workflow scale-up.

---
