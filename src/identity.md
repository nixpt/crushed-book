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

## Wave3 Identity (DID)

Exosphere integrates with the **Wave3 Protocol** to provide decentralized identity (DID) resolution. 
*   **DID Mapping**: Capsule IDs can be cryptographically mapped to `did:wave3` strings.
*   **Resolution**: The `exo-core` maintains a mapping between DIDs, Capsule IDs, and Public Keys for global discovery.

## Cryptographic Delegation

Crush supports **Third-Party Delegation** through Wave3 Envelopes:
1.  **Granter**: Signs a delegation for a specific resource and action.
2.  **Grantee**: Presents this delegation envelope to `exo-core`.
3.  **Kernel**: Validates the signature and grants the capability, cryptographically linking the grant to the granter's DID.

This allows for secure, cross-capsule and cross-host permission sharing without centralized brokers.
