# Hello World Capsule

Let's build a simple capsule that prints a message and performs a capability-gated file write. This will demonstrate both the SDK usage and the manifest-based security model.

---

## 🛠️ 1. Create the Project

Using the Exosphere CLI:

```bash
crush init my-hello-capsule --lang rust
cd my-hello-capsule
```

## 📝 2. The Logic (`src/main.rs`)

Open the generated file. It will use the `crush-sdk`.

```rust
use crush_sdk::{Capsule, Manifest, Result, capsule_main, io, fs};

struct HelloCapsule;

impl Capsule for HelloCapsule {
    fn run(&mut self, _entry: &str) -> Result<()> {
        io::print("Hello, Exosphere!")?;
        
        // Write a greeting to our isolated VFS
        fs::write("/greeting.txt", b"Created by an Agent.")?;
        
        Ok(())
    }
}

capsule_main!(HelloCapsule);
```

---

## 📜 3. The Manifest (`Capsule.toml`)

The manifest is where we "ask" the host for permissions.

```toml
[capsule]
name = "my-hello"
version = "0.1.0"

[permissions]
required = ["io.print", "fs.write"]
scopes = ["fs.write:/greeting.txt"]
```

## 🚀 4. Build, Pack, and Run

```bash
# Build the binary
cargo build --release

# Pack into a .cap artifact
packman pack ./target/release/my-hello-capsule ./hello.cap

# Run it!
packman run hello.cap
```

### What just happened?
1.  **Orchestrator Check**: `packman` verified that your capsule possesses the `io.print` and `fs.write` permissions locally.
2.  **VM Spin-up**: The CRUSH VM was initialized with a **Scoped HAL**.
3.  **VFS Translation**: When your code wrote to `/greeting.txt`, the HAL redirected it to a secure subfolder on your host, like `~/.exo/vfs/my-hello/greeting.txt`.
4.  **Secure Exit**: The VM shut down gracefully, returning control to your terminal.

**Congratulations! You've just built your first Agent-Native workload.**
