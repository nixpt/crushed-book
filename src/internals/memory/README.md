# CRUSH Memory Management

CRUSH uses an Arena-based memory management system to provide safety and isolation for polyglot execution.

## Core Components

### 1. The Arena
The **Arena** is a contiguous memory pool that stores all heap-allocated objects (Strings, Arrays, Maps, Objects). This ensures that memory is isolated between VM tasks and can be efficiently managed.

### 2. Runtime Borrow-Checking
To prevent data races and memory corruption across language boundaries, CRUSH implements a runtime borrow checker.
- Multiple immutable borrows are allowed.
- Only one mutable borrow is allowed.

---

## See Also

- [Pointers and References](pointers.md)
- [Architecture](../ARCHITECTURE.md)
- [API Reference](../API_REFERENCE.md)