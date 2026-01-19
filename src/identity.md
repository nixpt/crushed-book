# Identity & Provenance

> "Every action is signed. Every capsule is unique."

Crush implements an **AI-Native Identity** system based on cryptographic provenance. Unlike traditional OSs that rely on user accounts (`uid`), Crush relies on **Keypairs**.

## The Capsule ID

A Capsule ID is not a random number; it is derived from the capsule's public key.

```rust
// CapsuleID = version + base58(sha256(public_key))[0..32]
let capsule_id = "cap_2k39...";
```

This ensures that:
1.  **Spoof-proof**: You cannot claim an ID without the private key.
2.  **Location Independent**: The ID is the same regardless of which host it runs on.

## Key Management

Keys are stored in the **Keystore** (`~/.crush/keystore/`), isolated by the VFS.
*   **Private Key**: Held only by the `exo-core` (Host).
*   **Signing**: Capsules request signatures via `sys.sign()`, they never see the private key.

## Verification

When a capsule communicates (via ACP) or commits data (to AKGS), the header includes:
*   `Sender-ID`: The capsule ID.
*   `Signature`: Ed25519 signature of the payload.
*   `Timestamp`: Replay protection.

This creates an immutable **Audit Trail** for every AI action.
