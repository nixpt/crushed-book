# Teddy: Terminal IDE

**Teddy** is the "cozy" default editor and IDE for the Exosphere platform. Built for speed and agentic interaction, it provides everything you need to build capsules without leaving the terminal.

---

## 🧸 Why Teddy?

Teddy is designed for **Pair-Programming with Agents**. It includes deep integration with the Exosphere coordination protocols:

- **Protocol Awareness**: Teddy understands `.agent/PROTOCOL.md` and helps you follow git policies.
- **Capability-Gated OS Access**: Teddy runs as an Exosphere capsule itself, meaning it is as secure as the code it writes.
- **CASM Inspect**: Built-in viewer for CASM bytecode and CAST trees.

---

## 🚀 Quick Usage

Fire up Teddy by pointing it to a directory or file:

```bash
teddy ./my-agent-capsule/
```

### Key Keyboard Shortcuts
- **`Ctrl+S`**: Save file and trigger an incremental CRUSH build.
- **`Ctrl+R`**: Run the current capsule in a side-pane.
- **`Ctrl+P`**: Open the Command Palette for Exosphere tools (Packman, Vortex).
- **`Alt+A`**: Summon your AI coding assistant (Agent Mode).

---

## 🎨 Customizing Your Experience

Teddy supports CSS-based themes and a modular plugin system built—you guessed it—using Exosphere capsules.

**Example Theme snippet:**
```css
/* teddy_theme.css */
.editor-active-line {
    background-color: var(--exo-cyan-dim);
    border-left: 2px solid var(--exo-cyan-bright);
}
```

![Teddy Logo](assets/teddy.png)
