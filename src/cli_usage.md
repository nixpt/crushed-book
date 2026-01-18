# CLI Toolchain Masterclass

Master the commands that power the Exosphere developer experience.

---

## 🛠️ The `crush` Developer CLI

The `crush` tool (from the `crush-cli` crate) is your primary interface for development and compilation.

### Core Commands

| Command | Usage | Description |
|---------|-------|-------------|
| `init` | `crush init <name>` | Scaffold a new capsule project. |
| `compile` | `crush compile <file>`| Translate source (Python/Rust) to CAST/CASM. |
| `run` | `crush run <file.cap>` | Execute a packed capsule in a local VM. |
| `check` | `crush check <manifest>`| Verify capability compliance of a manifest. |

### 🌀 Integrated Compilation
You don't need to manually run walkers. `crush compile` automatically detects the source language and uses the appropriate language walker to generate the CASM artifact.

---

## 📦 `packman`: The Package Manager

`packman` is responsible for the lifecycle of capsule distribution.

### 1. Packing
Turn your build artifacts and manifest into a single, signed `.cap` file.
```bash
packman pack <source_dir> <output.cap>
```

### 2. Orchestration
Manage running capsules on your host.
```bash
# List all active capsules
packman list

# Securely terminate a capsule
packman stop <capsule_id>

# Install a capsule to the local registry
packman install <file.cap>
```

---

## 📊 Interaction with Vortex

The CLI tools are designed to work in synergy with the **Vortex** shell. When you `packman install` a capsule, it becomes available to search and launch from within the Vortex REPL.

## 🚀 Pro-Tip: Debugging with `--trace`
Running `crush run --trace` will provide a step-by-step audit of every CASM instruction executed, along with the state of the data stack. This is invaluable for debugging complex logic or capability failures.
