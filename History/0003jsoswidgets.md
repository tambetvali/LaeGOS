# LaeGOS Windowing Environment — Architectural Notes and Library Choice

This document outlines the reasoning, architecture, and design decisions behind the LaeGOS windowing environment. It explains why **WinBox.js** was selected as the foundational library, how it fits the goals of the LaeCalc OS, and which alternatives were evaluated and ultimately rejected.

---

## 1. Library Choice: **WinBox.js**

After surveying a wide range of JavaScript UI and window‑management libraries, **WinBox.js** was selected as the core windowing engine for the LaeGOS environment.

WinBox.js is:

- lightweight  
- dependency‑free  
- easy to integrate into any HTML/Flask template  
- flexible enough to support both “window” and “widget” modes  
- simple to extend with custom OS‑like behaviors  
- visually neutral, allowing LaeGOS to define its own aesthetic  

It provides the essential primitives needed for a desktop‑like environment without imposing a full framework or complex architecture.

---

## 2. Explanation of the Choice

### ✔ Simplicity and Control  
WinBox.js offers a minimal API that exposes exactly what is needed for a windowing system:

- create windows  
- move windows  
- resize windows  
- focus windows  
- embed arbitrary HTML inside windows  

This allows LaeGOS to build its own OS‑like behaviors on top without fighting a pre‑built desktop framework.

### ✔ Windows Are Just DIVs  
A WinBox window is fundamentally a styled `<div>` with a titlebar and controls.  
This makes it trivial to:

- embed widgets  
- reuse the same widget inline or inside a window  
- apply custom themes  
- animate transitions (e.g., minimize to icon)  
- integrate with Flask templates  

### ✔ Sandbox‑Friendly  
WinBox.js does not introduce:

- global state managers  
- virtual DOMs  
- component frameworks  
- routing systems  
- build pipelines  

This keeps the LaeGOS environment **transparent**, **hackable**, and **easy to extend**.

### ✔ Extensible for OS‑like Features  
Although WinBox.js does not include:

- minimize‑to‑icon  
- desktop icons  
- start menu  
- persistence  

…it provides enough hooks to implement all of these cleanly.

### ✔ Perfect Fit for LaeGOS Philosophy  
LaeGOS is a modular, widget‑driven system.  
WinBox.js supports this by allowing:

- widgets to be inline  
- widgets to be windows  
- windows to contain multiple widgets  
- windows to be spawned from icons or menus  

This aligns with the LaeGOS idea of “tools as objects” rather than “apps as pages.”

---

## 3. Architecture for LaeGOS OS Using WinBox.js

This section describes the planned structure of the LaeGOS desktop environment built on top of WinBox.js.

### 🟦 3.1 Desktop Layer  
A simple `<div id="desktop">` acts as the background surface.  
It contains:

- icons  
- the start menu  
- optional widgets  
- the area where windows appear  

Icons are simple HTML elements styled as desktop shortcuts.

### 🟩 3.2 Window Layer  
Each window is a WinBox instance.  
Windows can contain:

- calculators  
- displays  
- converters  
- harmonic tools  
- any LaeGOS widget  

Windows support:

- drag  
- resize  
- focus stacking  
- fullscreen  
- custom themes  

### 🟧 3.3 Widget/Window Duality  
Every LaeGOS widget is designed as a standalone HTML component.  
It can be:

- placed inline on the page  
- embedded inside a WinBox window  
- transformed into a window dynamically  

This duality is essential for LaeGOS, where tools are not “apps” but “objects.”

### 🟨 3.4 Minimize‑to‑Icon System  
WinBox.js does not include minimize behavior, but it can be implemented:

1. Capture the window’s bounding rectangle  
2. Capture the icon’s bounding rectangle  
3. Animate the window shrinking to the icon  
4. Hide the window  
5. Mark the icon as active  
6. Restore by reversing the animation  

This creates a familiar OS‑style minimize effect.

### 🟪 3.5 Start Menu  
A simple `<div id="start-menu">` toggled by a button.  
It can spawn:

- windows  
- widgets  
- settings panels  
- system tools  

### 🟫 3.6 Persistence  
Window positions and sizes can be stored in:

- `localStorage`  
- Flask session  
- server database  

On load, windows are restored using `.move()` and `.resize()`.

---

## 4. Alternatives Considered and Why They Were Rejected

### ❌ Interact.js  
**Why we considered it:**  
- excellent drag/resize mechanics  
- very flexible  

**Why we rejected it:**  
- not a window system  
- no titlebars, chrome, or window controls  
- no desktop or start menu  
- would require building *everything* from scratch  

### ❌ GoldenLayout  
**Why we considered it:**  
- powerful docking system  
- good for multi‑pane interfaces  

**Why we rejected it:**  
- not a desktop environment  
- no floating windows  
- no icons or start menu  
- too heavy for LaeGOS  

### ❌ Tweakpane  
**Why we considered it:**  
- elegant widget system  
- good for controls and panels  

**Why we rejected it:**  
- not a window manager  
- no desktop  
- no window chrome  
- no minimize/maximize  
- cannot serve as an OS shell  

### ❌ jQuery UI  
**Why we considered it:**  
- has draggable/resizable dialogs  

**Why we rejected it:**  
- outdated  
- heavy  
- visually incompatible  
- not suitable for modern OS‑like UI  

### ❌ OS.js  
**Why we considered it:**  
- full desktop environment  
- windows, icons, start menu included  

**Why we rejected it:**  
- too heavy  
- too opinionated  
- too complex for LaeGOS  
- difficult to integrate with Flask  
- would force LaeGOS into a predefined structure  

---

# Summary

WinBox.js was chosen because it provides the **simplest, cleanest, and most flexible foundation** for building a LaeGOS desktop environment. It gives us real windows without imposing a full framework, allowing LaeGOS to evolve organically and maintain its modular, experimental nature.

The architecture described above outlines how WinBox.js will be extended to support:

- windows  
- widgets  
- desktop icons  
- start menu  
- minimize animations  
- persistence  

This approach keeps LaeGOS lightweight, hackable, and fully under our control.
