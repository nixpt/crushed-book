# Crush Lang & Compilation

Crush supports a custom scripting language (`.crush`) that compiles to **CASM**.

> **Note**: Detailed language documentation is being migrated to this guide.


## Compilation Pipeline

1.  **Parsing**: The source code is parsed into an Abstract Syntax Tree (AST).
    - `crush-lang/src/ast.rs` defines the structure.
2.  **Compilation**: The AST is traversed to generate linear CASM instructions.
    - `crush-lang/src/compiler.rs` handles the translation.
    - Example: `1 + 2` becomes `push_int 1`, `push_int 2`, `add`.
3.  **Execution**: The resulting `Program` struct (containing functions and instructions) is loaded into the VM.

## Polyglot Support
Because the VM executes CASM, any language that can compile to CASM can run on Crush.
- **Python**: A python walker can traverse Python AST and emit CASM.
- **Rust**: A Rust compiler plugin or walker can emit CASM.
- **Bash**: A shell script parser can emit CASM.
