# Vortex: Interactive Shell & Dashboard

**Vortex** is more than just a shell; it is the **Command Center** for the Agent-Native OS. It converges multiple languages and capsules into a single, unified interactive environment.

---

## 🐚 The Convergent REPL

Vortex allows you to switch between language contexts fluidly. Use meta-commands (starting with `:`) to control the environment.

```bash
vortex (crush)> echo "Exosphere is active."
vortex (crush)> :set lang python
vortex (python)> print("Seamlessly switched to Python.")
vortex (python)> :set lang rust
vortex (rust)> println!("Now in a high-performance Rust context.");
```

---

## 📊 The Interactive Dashboard

Launch the TUI Dashboard from Vortex using `:dash` or `:vortex`.

![Vortex Screenshot](assets/vortex.png)

### Key Features
1.  **Resource Monitor**: Real-time tracking of CPU, RAM, and Gas usage for all active capsules.
2.  **Capability Inspector**: View exactly what permissions are currently granted to the active session.
3.  **Audit Ledger**: A live stream of security-verified system events and capability invocations.
4.  **Capsule Manager**: Start, stop, and inspect capsules directly from the TUI.

---

## ⌨️ Meta-Command Reference

| Command | Action |
|---------|--------|
| `:help` | Show available commands and language tips. |
| `:set lang <l>` | Switch the active language interpreter. |
| `:dash` / `:vortex`| Open the interactive dashboard. |
| `:list` | List all running capsules and their status. |
| `:stop <name>` | Securely terminate a running capsule. |
| `:exit` | Close the Vortex session. |
