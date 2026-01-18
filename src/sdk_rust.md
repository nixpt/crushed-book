# Rust SDK Guide

The **Crush Rust SDK (`crush-sdk`)** is the primary tool for building high-performance, secure capsules with first-class Exosphere integration.

## 📦 Getting Started

Add the SDK to your `Cargo.toml`:

```toml
[dependencies]
crush-sdk = "0.1.0"
```

## 🛠️ Defining a Capsule

In Rust, you implement the `Capsule` trait and use the `capsule_main!` macro to generate the entry point logic.

```rust
use crush_sdk::{Capsule, Manifest, Result, capsule_main};

struct MyCapsule;

impl Capsule for MyCapsule {
    fn init(&mut self, manifest: &Manifest) -> Result<()> {
        println!("Initializing capsule: {}", manifest.name);
        Ok(())
    }

    fn run(&mut self, entry_point: &str) -> Result<()> {
        match entry_point {
            "main" => self.do_work(),
            _ => Err("Unknown entry point".into()),
        }
    }
}

impl MyCapsule {
    fn do_work(&self) -> Result<()> {
        // Use capabilities through the SDK
        crush_sdk::io::print("Hello from Rust!")?;
        Ok(())
    }
}

capsule_main!(MyCapsule);
```

---

## 🛡️ Working with Capabilities

The SDK provides type-safe wrappers for every standard library capability.

### Filesystem Access
```rust
use crush_sdk::fs;

let data = fs::read("/data/config.json")?;
fs::write("/logs/output.log", b"Task complete")?;
```

### IPC Communication
```rust
use crush_sdk::icc;

// Send a message to the "logger" capsule
icc::send("logger", "Job finished successfully")?;
```

---

## 📝 The Manifest (`Capsule.toml`)

Every Rust capsule must include a `Capsule.toml` in its root directory. This file defines the capsule's identity and its required permissions.

```toml
[capsule]
name = "my-rust-app"
version = "1.0.0"
capsule_type = "tool"
entry_point = "main"

[permissions]
required = ["io.print", "fs.read", "fs.write"]
scopes = ["fs.read:/data/*", "fs.write:/logs/*"]
```

## 🚀 Building & Running

1. **Compile**: `cargo build --release`
2. **Pack**: `packman pack ./target/release/my-capsule ./my-capsule.cap`
3. **Run**: `packman run ./my-capsule.cap`
