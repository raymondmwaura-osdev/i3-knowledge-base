## Transition from i3 to Sway

### Introduction

This document outlines the reasoning behind migrating from the i3 window manager to Sway. The primary objective is to adopt a keyboard-centric tiling window management workflow that remains aligned with contemporary and future display-server technologies.

### Background on i3 and X11

I selected i3 initially because of its efficient, keyboard-oriented design and predictable tiling behavior. The original intent of this repository was to serve as a knowledge base for my ongoing work with i3.

However, further investigation into display-server architectures revealed a structural limitation: i3 is tightly coupled to the X11 protocol. X11, while historically significant, is now considered legacy software. It is currently in maintenance mode, receiving only essential fixes with no major feature development. As a result, its long-term viability is limited.

### Emergence of Wayland

Wayland has been developed as a modern alternative to X11, offering a more secure, efficient, and maintainable architecture. Although Wayland is still evolving and does not yet match X11’s maturity in all areas, industry momentum is clearly shifting toward it. Over time, Wayland is expected to become the dominant display protocol, while X11’s relevance will continue to decline.

Given that i3 does not natively support Wayland and is unlikely to do so, continued investment in i3 would not be strategically sound for long-term use.

### Strategic Shift to Sway

To maintain a consistent keyboard-driven tiling workflow while aligning with modern display-server trends, I have chosen to transition to Sway.

Sway is a tiling window manager designed specifically for Wayland and intentionally mirrors the i3 user experience. Its configuration model, behavior, and philosophy closely resemble i3, making it the most practical successor for users who want the i3 paradigm without being constrained by X11.

All future notes and findings related to Sway will be documented [here](https://github.com/raymondmwaura-osdev/integrating-sway).

### Conclusion

This transition does not represent an ending but rather an expansion into a more sustainable, forward-compatible ecosystem. The exploration of Wayland and Sway is only beginning.

---
