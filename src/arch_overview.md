# Architecture Overview

Crush is built on a layered architecture designed to enforce the **EXO Core Contract**: *Mechanism belongs to the system; Meaning belongs to the capsule.*

## Layers

```mermaid
graph TD
    A[Capsule Code] -->|Compiles to| B[CASM Bytecode]
    B -->|Executed by| C[Crush VM]
    C -->|Uses| D[Capabilities (Stdlib)]
    D -->|Calls| E[HAL (Hardware Abstraction Layer)]
    E -->|Abstracts| F[Host OS (Linux, etc.)]
```

![Polyglot Vortex](assets/polyglot_vortex.png)

1.  **Capsule Code**: The source logic (Crush, Python, Rust, etc.).
2.  **VM**: The sandbox execution environment. It knows nothing about files or network, only instructions and abstract capabilities.
3.  **Capabilities**: The "standard library" functions (e.g., `fs.read`, `io.print`) that provide meaning to resource access.
4.  **HAL**: The strictly defined interface to the outside world. It handles the raw mechanism of reading bytes or opening sockets, without enforcing policy.
