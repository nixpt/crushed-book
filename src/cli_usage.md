# CLI Usage

The `crush` binary is the primary entry point for all Crush operations.

## Usage

```bash
crush [OPTIONS] <COMMAND>
```

## 1. Batch Execution

Run a supported source file or a compiled capsule:
```bash
crush run script.py
crush run application.casm
```

### Command Flags
- `--isolated`: Runs the capsule in a strict sandbox without host capability access.
- `--capsule <name>`: Explicitly specifies the capsule name if it cannot be inferred.

## 2. Interactive Shell (Vortex)

Launch the interactive REPL by running `crush` without arguments:
```bash
crush
```

### Features
- **Cross-Language Eval**: Execute snippets of Python, Rust, or Crush directly from the prompt.
- **Auto-Bootstrap**: Standard capabilities (IO, FS) are automatically injected into the shell session.
- **Meta Commands**:
    - `:help` / `.help`: Show help.
    - `:load <path>`: Load a file into the current session.
    - `:exit`: Terminate the shell.

## 3. Package Management (Packman)

See [Packman Reference](pacman.md) for details.

## 4. Error Handling & Debugging

When a fault occurs at runtime, the CLI provides:
- **Semantic Error**: A high-level description of what went wrong.
- **Source Trace**: The file and line number mapping from the original source code.
- **Instruction Trace**: The last executed CASM instructions before the crash.
