# Capsule Design & Package Management

## 1. The Capsule Format (`.cap`)

A **Capsule** is the fundamental unit of distribution in Crush. It is a compressed archive (ZIP) containing code, assets, and metadata.

### 1.1 Structure
```
my-package.cap (ZIP Archive)
├── Crush.toml       # Manifest
├── README.md        # Documentation
├── signature.sig    # Cryptographic Signature (Ed25519)
└── payload/         # Content
    ├── main.casm.json
    ├── lib.casm.json
    └── assets/
        └── data.csv
```

### 1.2 Manifest (`Crush.toml`)
```toml
[package]
name = "my-package"
version = "1.0.0"
authors = ["nixp"]
description = "A sample Crush capsule"
license = "MIT"

[capsule]
type = "binary" # binary, library, service, or generic
entry = "payload/main.casm.json" # Optional, for execution

[dependencies]
std = "0.1"
utils = { version = "1.2", source = "registry" }
```

### 1.3 Capsule Types
1.  **Binary**: Executable logic (CASM). Entry point required.
2.  **Library**: Reusable code. No entry point.
3.  **Service**: Long-running daemon config.
4.  **Generic**: Arbitrary data (models, datasets, UI assets). No strict structure required inside `payload/`.

## 2. Package Management

### 2.1 The Repository
Capsules are stored in a Content-Addressable Store (CAS).
-   **Local**: `~/.crush/capsules/<SHA256>/`
-   **Global**: P2P Swarm.

### 2.2 Identification
Capsules are identified by:
1.  **Content Hash**: Immutable reference (e.g., `sha256:abc123...`).
2.  **Name/Version**: Mutable reference resolved via Registry (e.g., `std@1.0.0`).

### 2.3 The `cpm` (Crush Package Manager)
Integrated into `crush` CLI.

```bash
# Workflow
crush init            # Create Crush.toml
crush package         # Build .cap archive from current dir
crush publish         # Sign and announce to Federation
crush install <name>  # Resolve and download
crush run <name>      # Run installed capsule
```

## 3. Federation Strategy
We leverage the `federation` crate for distribution.
-   **Registry**: A Kademlia DHT stores `package_name:version` -> `content_hash`.
-   **Storage**: Nodes serve the `.cap` files via Bitswap (or simple HTTP/RPC for v1).
