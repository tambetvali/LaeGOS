##### Architectural Choices - AI read first

We have the following architectural choices for implementation:
- Hosting: Pythonanywhere, [PythonAnywhere](https://www.pythonanywhere.com/), [LaeGOS 🏠](https://laegna.pythonanywhere.com/).
- Version Control: Git, [GitHub](https://www.github.com/), [github LaeGOS 🏠](https://www.github.com/tambetvali/LaeGOS), [github LaeGOS-Widgets 📟].(https://www.github.com/tambetvali/LaeGOS-Widgets); this is also the development platform.
- Programming Language: [Python](https://www.python.com/).
- Server type: [Flask](https://flask.palletsprojects.com/en/stable/), [Jinja](https://jinja.palletsprojects.com/en/stable/) templates in-box.
- Windows system: [WinBox.js](https://nextapps-de.github.io/winbox/).

# LaeGOS Architecture  
### A Minimal, Extensible Operating System for Laegna Mathematics

LaeGOS is a micro‑OS built around a single idea:  
**a number can be an environment.**  
The architecture grows outward from this smallest meaningful object, allowing users to explore Laegna mathematics through modular, reusable components.

This document provides a concise overview of the system’s structure and design principles.

---

## 1. Core Principle: The Single Number

At the center of LaeGOS is **one active number**.  
This number is the current context for all widgets, transformations, and visualizations.

Why a single number?

- It is cognitively lightweight.  
- It provides a stable anchor for UI and logic.  
- It keeps the system small enough to understand, yet open enough to extend.  
- It mirrors how Laegna mathematics treats numbers as *contexts*, not static values.

Compound numbers (e.g., X, Y, Z) will be supported later, but even then the system maintains **one active number** at a time. This preserves clarity and prevents interface overload.

---

## 2. Widgets: The Real “OS”

LaeGOS does not imitate traditional operating systems.  
Instead, it defines an OS as:

> **A set of reusable widgets for interacting with numbers.**

Widgets include:

- number displays  
- sliders and scrollbars  
- increment/decrement controls  
- inspectors and converters  
- visual metaphors  
- context switchers  

Each widget is small, focused, and self‑contained.  
Together, they form the functional surface of LaeGOS.

Widgets are the building blocks from which users can assemble:

- calculators  
- dashboards  
- compound‑number tools  
- experimental interfaces  
- custom modes  

This modularity is the foundation of scalability.

---

## 3. Window‑Based Modular System

Every LaeGOS window is a module with:

- its own HTML template  
- its own JavaScript logic  
- its own CSS  
- its own internal state  

This design ensures:

- components are easy to inspect  
- users can fork or remix any module  
- complexity stays localized  
- the system remains understandable as it grows  

A window is not a subsystem — it is a **component**.  
This keeps LaeGOS flexible and avoids monolithic architecture.

---

## 4. Three‑Layer Ecosystem

LaeGOS operates across three coordinated layers:

### **1. Neocities (spireason.neocities.org)**  
Human‑facing conceptual hub.  
Provides navigation, introductions, and the “console” entry point.

### **2. PythonAnywhere (laegna.pythonanywhere.com)**  
Runtime environment for the OS.  
Hosts the Flask application and all interactive components.

### **3. GitHub (github.com/tambetvali/LaeGOS)**  
Documentation and AI‑compatible knowledge layer.  
Stores Markdown manuals, tasks, explanations, and configuration files.

This separation ensures:

- humans get clarity  
- AIs get structured information  
- the OS remains lightweight and focused  

LaeGOS windows can later render GitHub Markdown directly, bridging runtime and documentation.

---

## 5. Why This Architecture Scales

LaeGOS grows from a stable core rather than collapsing under complexity.

- A single number keeps the system grounded.  
- Widgets provide reusable interaction patterns.  
- Windows isolate complexity into manageable modules.  
- GitHub ensures the knowledge layer is readable by both humans and AIs.  
- The ecosystem remains open for future extensions (compound numbers, file systems, custom modes).

This architecture is intentionally minimal — not to limit growth, but to **enable it**.

---

## 6. Future Directions

The next architectural layers will include:

- definition of the Laegna Number object  
- the first widget set  
- the window manager skeleton  
- module loading and composition  
- Markdown rendering from GitHub  
- optional compound‑number contexts  

Each addition will follow the same principle:  
**small, modular, and centered on the active number.**

---

## Summary

LaeGOS is a micro‑OS built from the smallest meaningful unit — a number — and expanded through modular widgets and windows. Its architecture is intentionally minimal, scalable, and designed to support both human exploration and AI‑assisted reasoning.

This document outlines the essential structure.  
The rest of the system grows one component at a time.

---

# LaeGOS Architecture

***This was used by CoPilot to generate article before, in beginning of this document.***

LaeGOS is Laegna Calculator Operating System with the following framework:

Single number is active instance every window can access:
- Tool can create *class instance*, an active instance which contains list of named numbers.
  - In such case, single number is always selected.

With this single number:
- Screens allow to view it.
- Keyboards allow to change it, and animators do it in time-based way.
- Visualizations and simulations can help one understand the number.

Complexity:
> Simple enough to start developing alone.

Simplicity:
> Enough features for user to build their own interaction with Laegna numbers.
