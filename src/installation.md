# Installation

Setting up Exosphere is designed to be straightforward. Currently, we support **Linux** as the primary host environment, with macOS and Windows support in the roadmap.

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:

-   **Rust (1.75+)**: The core runtime is built in Rust.
    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```
-   **Git**: For version control.
-   **Python (3.10+)**: (Optional) Required if you plan to build Python-based capsules.

---

## 🚀 Building the Core Runtime

The "Heart" of Exosphere is the CRUSH runtime.

```bash
# Clone the core repository
git clone https://github.com/nixpt/crush.git
cd crush

# Build the workspace
cargo build --release

# The resulting binary is located at ./target/release/crush-cli
```

## 📦 Installing the Developer CLI

For convenience, we recommend adding the `crush` tool to your path.

```bash
# Install the CLI tool
cargo install --path tools/crush-cli
```

Verify your installation:
```bash
crush --version
```

---

## 📥 Getting the System Capsules

Exosphere is a minimal kernel by design. To do anything useful, you need the **System Capsules** (Vortex, Packman, etc.).

```bash
# Clone the capsules repository
git clone https://github.com/nixpt/crush-capsules.git
cd crush-capsules

# (Optional) Build all core tools
cargo build --release
```

## 🧪 Quick Test

Once installed, try launching **Vortex** (The Exosphere Shell):

```bash
# Run vortex directly from the build artifacts
./target/release/vortex
```

If you see the `vortex (crush)>` prompt, your Exosphere environment is active and ready for work!
