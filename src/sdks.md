# Developer SDKs

Exosphere is built to be language-agnostic, and our SDKs provide the the high-level tools you need to build powerful **Capsules** in your language of choice.

---

## 🚀 Choosing Your SDK

| SDK | Language | Best For... |
|-----|----------|-------------|
| **[Rust SDK](sdk_rust.md)** | Rust | High performance, system tools, and low-level drivers. |
| **[Python SDK](sdk_py.md)** | Python | Rapid prototyping, AI/ML agents, and data orchestration. |
| **[C SDK](sdk_c_sdk.md)** | C | High performance, system integration, and low-level control. |
| **[Swift SDK](sdk_swift.md)** | Swift | Cross-platform development with modern language features. |
| **[JVM SDK](sdk_jvm.md)** | Java/Kotlin | Enterprise-grade applications and Android integration. |
| **[C ABI](sdk_c.md)** | C / FFI | Building new language walkers and low-level integrations. |

---

## 🛠️ Common SDK Features

Every Exosphere SDK provides a set of common abstractions:

1.  **Manifest Definition**: Easy macros or configuration for declaring capabilities.
2.  **Capability Proxies**: Type-safe wrappers for standard library calls.
3.  **Capsule Lifecycle**: Hooks for `init`, `run`, and `shutdown`.
4.  **Serialization**: Integrated support for CBV and JSON for cross-capsule communication.

---

## 🎨 Design Philosophy: "Don't Call us, We'll Call You"

Exosphere SDKs use a **Inversion of Control** pattern. Instead of a linear `main` function, you define a `Capsule` object that responds to events from the CRUSH runtime.

### The "Hello" Signature
Regardless of the language, the entry point for an Exosphere capsule looks conceptually like this:

```
initialize(manifest) -> result
run(entry_point) -> result
handle_message(sender, message) -> result
```

This uniform lifecycle allows the Exosphere Orchestrator to manage capsules from different languages using exactly the same logic.
