# EXO Core Contract

The **EXO Core Contract** is the philosophical foundation of Crush. It dictates a strict separation of concerns to maximize portability and security.

## The Principle

> **EXO owns mechanism. Capsule owns meaning.**

## Implications

1.  **No Ambient Authority**: A capsule cannot simply "open a file". It must possess a capability (mechanism) granted by the host, and it uses that capability to perform an action (meaning).
2.  **Explicit Dependencies**: All capabilities required by a capsule must be declared in its **Manifest**.
    ```json
    {
        "required_capabilities": ["fs.read", "io.print"]
    }
    ```
3.  **HAL Isolation**: The VM and Standard Library must never call Host OS APIs directly (e.g., `std::fs::File::open`). Instead, they must go through the **HAL Traits** defined in `exo-core`. This allows the entire system to be retargeted (e.g., to WASM, to a microkernel) by simply swapping the HAL implementation.
4.  **Scoped Execution**: When a capsule runs, it is wrapped in a `ScopedHal` that provides a private, virtualized view of the system. This includes:
    - **Handle Registry**: Maps virtual resource handles to real system handles, preventing resource harvesting.
    - **VFS Path Virtualization**: Scopes all filesystem operations to a designated root directory (e.g., `~/.exo/vfs/<capsule_name>`).
    - **Environment Sandboxing**: Provides isolated environment variables per capsule.
