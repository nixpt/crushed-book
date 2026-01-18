# FFI & C ABI

The **Exosphere C ABI** is the lowest common denominator for polyglot interoperability. It defines the binary interface that all high-level SDKs and language walkers use to communicate with the CRUSH VM.

---

## 🏗️ The Core Interface

The CRUSH interaction model is built on a simple set of C-compatible function pointers.

### 1. The Global Hal
Every capsule is provided with a pointer to a `Hal` structure.

```c
typedef struct {
    void* handle_registry;
    void* vfs_root;
    // Function pointers for raw I/O
    int (*hal_read)(void* handle, void* buffer, size_t size);
    int (*hal_write)(void* handle, const void* buffer, size_t size);
} Hal;
```

---

## 🔗 Building New Walkers

If you are building a new language walker (e.g., for Go or Zig), you must implement the **Crush Native Interface (CNI)**.

### The CNI Lifecycle

1.  **`crush_init(const Manifest* manifest)`**: Called by the VM to initialize your guest runtime.
2.  **`crush_load_bytecode(const char* data, size_t len)`**: Loads the CASM/CAST into your runtime.
3.  **`crush_execute(const char* entry_point)`**: Starts the execution loop.

---

## 🎨 Why a C ABI?

By targeting a stable C ABI, Exosphere achieves:
- **Maximum Compatibility**: Almost every modern language can call C functions (FFI).
- **Minimum Overhead**: Direct binary communication without heavy serialization.
- **Retargetability**: The same ABI works whether the host is Linux, a Web Browser (WASM), or a custom microkernel.

## 🚀 Pro Tip: Using Zig
**Zig** is the recommended language for building new Exosphere SDKs or low-level HAL bridges, as it offers the best C-interop and memory safety primitives without the complexity of a heavy runtime.
