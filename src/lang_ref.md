# Language Reference

The Exosphere Language Suite is designed for maximum flexibility and performance. It allows you to use your favorite high-level languages while benefiting from the deterministic, secure execution of the CRUSH runtime.

---

## The CRUSH Translation Pipeline

Exosphere does not run source code directly. Instead, it uses a three-stage translation pipeline:

1.  **Source Code**: High-level code (e.g., Python, Rust).
2.  **[CAST (Crush AST)](cast.md)**: A machine-readable, language-agnostic intermediate representation.
3.  **[CASM (Crush Assembly)](casm.md)**: A low-level, stack-based bytecode format that the VM executes.

---

## Supported Languages

| Language | Walker Status | Notes |
|----------|---------------|-------|
| **CRUSH** | Native | The "home" language of Exosphere. Built-in support. |
| **Python** | ✅ Beta | Fully featured with Tree-Sitter based walker. |
| **Rust** | ✅ Beta | Supports structural parsing and macro expansion. |
| **JavaScript** | 🟡 Early Alpha | Basic control flow and function support. |
| **Go** | 🟡 Alpha | Structural parsing and primitive types. |
| **C / Zig** | 🟡 Alpha | LLVM-based translation in progress. |

---

## 🚀 Why Polyglot?

Modern agentic systems require diverse tools. A data-science agent might prefer **Python** for its libraries, while a low-level system agent might need **Rust** for performance.

By normalizing all languages into **CASM**, Exosphere allows these agents to:
- **Share Data**: Objects created in Python can be processed in Rust.
- **Unified Security**: One permission model for every language.
- **Isolated Performance**: Gas limits apply equally to all guest runtimes.
