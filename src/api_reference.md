# CRUSH API Reference

This document provides a reference for the CRUSH runtime, focusing on the CASM instruction set and the Capability system.

## Table of Contents

- [CASM Instruction Set](#casm-instruction-set)
- [Capability System](#capability-system)
- [Runtime Value Types](#runtime-value-types)
- [CLI Reference](#cli-reference)

---

## CASM Instruction Set

CASM (CRUSH Assembly) is the low-level format executed by the CRUSH VM. Each instruction is a JSON object with an `op` field and optional `args`.

### Stack Operations

| Op | Arguments | Description |
|---|---|---|
| `push_int` | `{ "value": i64 }` | Push an integer. |
| `push_float` | `{ "value": f64 }` | Push a float. |
| `push_str` | `{ "value": string }` | Push a string (allocates in Arena). |
| `push_bool` | `{ "value": bool }` | Push a boolean. |
| `push_null` | None | Push a null value. |
| `pop` | None | Remove top value. |
| `dup` | None | Duplicate top value. |

### Memory Operations

| Op | Arguments | Description |
|---|---|---|
| `store` | `{ "name": string }` | Store TOS in local variable. |
| `load` | `{ "name": string }` | Load variable onto stack. |
| `export_var` | `{ "name": string }` | Store TOS in shared registry. |
| `import_var` | `{ "name": string }` | Load from shared registry. |

### Arithmetic & Logic

| Op | Description |
|---|---|
| `add` | TOS = pop() + pop() |
| `sub` | TOS = pop() - pop() |
| `mul` | TOS = pop() * pop() |
| `div` | TOS = pop() / pop() |
| `eq` | TOS = pop() == pop() |
| `ne` | TOS = pop() != pop() |
| `lt` | TOS = pop() < pop() |
| `gt` | TOS = pop() > pop() |
| `and` | TOS = pop() && pop() |
| `or` | TOS = pop() \|\| pop() |
| `not` | TOS = !pop() |

### Control Flow

| Op | Arguments | Description |
|---|---|---|
| `jmp` | `{ "target": usize }` | Absolute jump. |
| `jmp_if` | `{ "target": usize }` | Jump if TOS is truthy. |
| `jmp_if_not` | `{ "target": usize }` | Jump if TOS is falsy. |
| `call` | `{ "function": string }` | Call internal function. |
| `ret` | None | Return from function. |
| `restart` | `{ "task_id": usize }` | Restart a task (supervisor only). |
| `watchdog` | `{ "task_id": usize, "deadline": u64, "action": string }` | Set task watchdog. |

### Capabilities

| Op | Arguments | Description |
|---|---|---|
| `cap_call` | `{ "name": string, "argc": usize }` | Call host capability. |

---

## Capability System

Capabilities provide access to host-level functionality. Namespaces are organized as `namespace.capability`.

### I/O Namespace (`io`)

- `io.print(*args)`: Prints values to standard output.
- `io.input()`: Reads a line from standard input. Returns a string reference.

### Filesystem Namespace (`fs`)

- `fs.read(path)`: Reads file content to a string.
- `fs.write(path, content)`: Writes string content to a file.

### Network Namespace (`net`)

- `net.http_get(url)`: Performs an asynchronous HTTP GET request.

### FFI Namespace (`ffi`)

- `ffi.python(func_name, *args)`: Invokes a Python function.
- `ffi.c(func_name, *args)`: Invokes a C function.

### Task Namespace (`task`)

- `task.restart(task_id)`: Restarts the specified task.
- `task.watchdog(task_id, deadline, action)`: Sets a watchdog timer.

---

## Runtime Value Types

- `Int`: 64-bit signed integer.
- `Float`: 64-bit IEEE 754 float.
- `Bool`: Boolean `true` or `false`.
- `Str`: UTF-8 string (Reference type).
- `Array`: Contiguous list of `RuntimeValue` (Reference type).
- `Map`: String-to-Value mapping (Reference type).
- `Ref`: An index into the task-isolated Arena.
- `Null`: Represents the absence of a value.

---

## CLI Reference

### `crush-cli run <file>`
Executes a CRUSH- **File Format**: `.casm` (JSON-encoded)
).

### `crush-cli serve`
Starts a federation node for P2P code execution.

---

## See Also

- [Core Modules](CORE_MODULES.md)
- [Architecture](ARCHITECTURE.md)
- [Pointers & Memory](memory/pointers.md)
