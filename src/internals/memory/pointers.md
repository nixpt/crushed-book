# CRUSH Memory and Arena System

The CRUSH memory system is built around a task-isolated **Arena** that provides memory safety through a runtime borrow-checking mechanism. This system ensures that all heap-allocated objects are managed safely across language boundaries.

## Core Concepts

### The Arena

The Arena is a contiguous storage for complex objects like `String`, `Array`, and `Map`. Every object in the Arena is indexed by a unique `usize` reference.

### RuntimeValue::Ref

In CRUSH, memory addresses are represented by the `Ref(usize)` variant of the `RuntimeValue` enum. When an instruction (like `push_str`) creates an object, it is allocated in the Arena, and its reference is pushed onto the VM stack.

### Borrow Checking

CRUSH implements a runtime equivalent of Rust's borrow checker via `BorrowState`:

- **Immutable Refs**: Multiple read-only references can exist.
- **Mutable Ref**: Only one exclusive write reference can exist at a time.

If an instruction attempts to mutate an object while it is immutably borrowed, a `BorrowError` is raised, halting the VM.

## Supported Objects

The Arena can store the following `Object` types:

- **Str**: UTF-8 strings.
- **Array**: Vectors of `RuntimeValue`.
- **Map**: String-keyed hash maps.
- **Object**: Language-specific object structures with fields.
- **Tagged**: Metadata-wrapped values for advanced type tracking.

## Capability Integration

Host capabilities interact with the Arena through the `HostAdapter`. When a capability like `fs.read` is called, it:

1. Uses the Arena to resolve string references (e.g., file paths).
2. Allocates new objects (e.g., file content) in the Arena.
3. Returns a `Ref` to the VM stack.

## Safety and Security

- **Isolation**: Each VM instance has its own private Arena.
- **Validation**: References are checked for validity before access.
- **Reference Tracking**: The VM tracks object lifetimes to prevent use-after-free conditions.

---

## See Also

- [Core Modules](../CORE_MODULES.md)
- [API Reference](../API_REFERENCE.md)
- [Architecture](../ARCHITECTURE.md)