# Standard Library

The **Crush Standard Library (crush-stdlib)** provides the bridge between the isolated VM and the outside world. It defines the core set of **Capabilities** that capsules use to perform useful work.

---

## 🧩 Module Overview

| Module | Purpose | Key Capabilities |
|--------|---------|-----------------|
| **[I/O](stdlib_io.md)** | Standard input/output | `print`, `input`, `clear` |
| **[Filesystem](stdlib_fs.md)** | Virtualized file access | `read`, `write`, `list`, `exists` |
| **[System](stdlib_system.md)** | Resource monitoring | `env`, `time`, `mem_info` |
| **[Networking](stdlib_net.md)** | Isolated network access | `http_get`, `tcp_connect` |

---

## 🛡️ The Scoped HAL Guard

Unlike traditional standard libraries that wrap direct system calls, `crush-stdlib` always operates through the HAL. This means:
- **Portability**: The same `fs.read` call works whether you are on Linux, Windows, or a bare-metal kernel.
- **Security**: The Standard Library itself doesn't need to be "trusted"; it can only do what the `ScopedHal` allows.

## Example: Capability Scoping

In Exosphere, standard library calls are inherently scoped. When you call `fs.read("/config.json")`, the library doesn't just open a file; it requests the `fs.read` capability from the VM. The VM then translates the virtual path into a secure host path.

```rust
// Internals of stdlib_fs (simplified)
fn read(path: String) -> Result<Vec<u8>> {
    let cap = get_capability("fs.read")?;
    cap.invoke(path)
}
```
