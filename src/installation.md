# Installation

## Prerequisites

- **Rust**: Ensure you have a recent version of Rust installed (1.70+ recommended).
  ```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```

## Building from Source

Clone the repository and build the workspace:

```bash
git clone https://github.com/nixp/crush.git
cd crush
cargo build --release
```

## Installing the CLI

You can install the `crush` binary directly to your cargo bin path:

```bash
cargo install --path crush-cli
```

Verify the installation:

```bash
crush --version
```
