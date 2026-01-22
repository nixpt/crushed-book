# Nexquelium: The Agent-Native Browser

Nexquelium is the official browser-replacement for the Exosphere ecosystem. It is designed as a **capsule-driven shell** that decouples the rendering layer from the execution layer.

## Architecture

Traditional browsers bundle the runtime (JS engine), the sandbox, and the renderer together. Nexquelium separates these:

1.  **Core (Runtime)**: The Exosphere Rust core manages capabilities and execution.
2.  **Shell (Renderer)**: A Tauri-based native application that provides a window manager and WebView containers.
3.  **Capsules (Logic)**: Isolated units of work that provide both logic and optional view definitions.

## Nexquelium Control Protocol (NCP)

NCP is the bridge between capsules and the shell. It allows capsules to:
- Register views (`NCP.RegisterView`)
- Push state updates (`NCP.UpdateState`)
- Receive user interactions (`NCP.ViewEvent`)

## Development

To create a Nexquelium-native application, developers create a capsule that defines an `ncp` section in its `capsule.toml`. This tells the shell which assets to render and how to communicate with the capsule.

```toml
[ncp]
view_id = "my-app"
render_type = "html"
entry_point = "ui/index.html"
```

The shell then loads these assets using the `exo://` protocol, ensuring security and isolation.
