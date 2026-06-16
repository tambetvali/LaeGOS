# LaeGOS History  
## Structure, Numbering System, and Purpose

The `History/` directory documents the architectural decisions, design reasoning, and conceptual evolution of the LaeGOS ecosystem. It serves as a durable journal of choices made across:

- https://github.com/tambetvali/LaeGOS
- https://github.com/tambetvali/LaeGOS-widgets
- https://spireason.neocities.org
- https://laegna.pythonanywhere.com

This folder is not a changelog.  
It is a **decision log**, capturing *why* the system is built the way it is.

---

# 1. Numbering System

Each entry begins with a **four‑digit, zero‑padded integer**, for example:

\`\`\`
0001whylaegos.md
0002OAuthDatabases.md
0003architecture-shift.md
\`\`\`

### Why zero‑padding?

GitHub sorts filenames **lexicographically**, not numerically.  
Without padding, the order becomes incorrect:

\`\`\`
1.md
10.md
11.md
2.md
\`\`\`

Zero‑padding ensures correct ordering forever:

\`\`\`
0001...
0002...
0003...
\`\`\`

This pattern is stable, predictable, and compatible with all tools.

---

# 2. Ordering Philosophy

The History folder uses **two layers of ordering**:

### 1. Filename order  
Represents the *logical* or *conceptual* sequence of decisions.

### 2. Git commit timestamps  
Represent the *temporal* evolution of the project.

This dual system allows:

- chronological browsing  
- conceptual grouping  
- easy referencing  
- stable URLs  

---

# 3. Purpose of Each Entry

Each file in the History folder should answer:

- **What decision was made?**  
- **Why was it made?**  
- **What alternatives were considered?**  
- **What constraints shaped the choice?**  
- **What does this enable for LaeGOS?**

Entries may include:

- architectural reasoning  
- rejected alternatives  
- future implications  
- diagrams or examples  
- links to related code or commits  

---

# 4. Recommended Format for New Entries

A typical entry should follow this structure:

\`\`\`
# Title of the Decision

## Summary
A short explanation of the decision and its importance.

## Context
What problem or question led to this decision.

## Options Considered
- Option A — description
- Option B — description
- Option C — description

## Decision
Which option was chosen and why.

## Consequences
What this enables, what it restricts, and what future work it implies.

## References
Links to commits, issues, or external resources.
\`\`\`

This format keeps the journal consistent and easy to navigate.

---

# 5. When to Create a New Entry

Create a new history entry when:

- a major architectural choice is made  
- a previous assumption is overturned  
- a new subsystem is introduced  
- a dependency or backend is replaced  
- a conceptual shift occurs  
- a design philosophy is clarified  

Small implementation details do **not** belong here.

---

# 6. Current Entries

- `0001whylaegos.md` — Why LaeGOS exists  
- `0002OAuthDatabases.md` — Evaluating database‑provided OAuth and stateless identity  

More entries will be added as the system evolves.

---

# 7. Philosophy

The History folder is a **living document**.  
It preserves the reasoning behind LaeGOS so that future contributors — or even future versions of yourself — can understand not just *what* was built, but *why*.
