# CRUSH Encrypted Execution Guide

Encrypted Execution enables you to distribute and run CRUSH capsules with cryptographic guarantees for confidentiality, integrity, and auditabilty.

## Overview

The encrypted execution workflow involves:
1.  **Key Generation**: Creating a Master VM Key (MVK) stored securely in your OS keyring.
2.  **Encryption**: Packaging your CASM bytecode into an `.ecap` (Encrypted Capsule) file.
3.  **Inspection**: Verifying the integrity and metadata of encrypted capsules without exposing contents.
4.  **Execution**: Running the encrypted capsule in a secure VM environment.
5.  **Auditing**: Reviewing the cryptographic transcript and execution logs.

## 1. Key Management

Before using encrypted execution, you must initialize your key ring.

### Generate a Master Key
The Master VM Key (MVK) is the root of trust.

```bash
crush key generate
```

This will generate a secure 256-bit key and store it in your OS keyring (e.g., secret-service on Linux, Keychain on macOS).

### View Public Key Info
You can view the ID and public parameters of your keys (privacy-safe, no secrets shown):

```bash
crush key list
```

## 2. Encrypting Capsules

To distribute a capsule securely, you encrypt its compiled `.casm` file.

```bash
# Compile source to CASM first
exo compile my_script.crush

# Encrypt the CASM file
crush encrypt my_script.casm --output my_package.ecap
```

This command:
1.  Derives a unique artifact key from your MVK for this specific capsule.
2.  Encrypts the bytecode using ChaCha20-Poly1305.
3.  Wraps it in the ECAP container format.
4.  Generates a Merkle tree for integrity verification.

## 3. Inspecting Capsules

You can inspect the metadata of an `.ecap` file to verify its structure and integrity.

```bash
crush inspect my_package.ecap
```

Output includes:
*   Encrypted sections list
*   Compression ratios
*   Integrity hashes

To verify the Merkle tree integrity:

```bash
crush inspect my_package.ecap --verify
```

## 4. Running Encrypted Capsules

The `exo run` command automatically detects `.ecap` files and switches to encrypted mode.

```bash
exo run my_package.ecap
```

**What happens internally:**
1.  The VM accesses the MVK from your keyring.
2.  It derives the specific decryption key for the artifact.
3.  The bytecode is decrypted **page-by-page** on demand directly into protected memory.
4.  Execution proceeds with audit logging enabled.

## 5. Audit Logging

Every encrypted execution generates a tamper-evident audit log.

**Log Location:** `~/.crush/audit.jsonl`

### Log Format
Each line is a JSON object representing an event:

*   **CapsuleLoad**: Recorded when the package is verified.
*   **CasmDecrypt**: Recorded for every page decrypted.
*   **ExecutionComplete**: Recorded on exit, containing the **Transcript Hash**.

### Transcript Hash
The `transcript_hash` in the `ExecutionComplete` event is a SHA-256 hash of every instruction executed and capability invoked. This provides a cryptographic proof of the exact execution path.

## 6. FAQ

### What happens to generated artifacts?

*   **Running `.ecap` files**: No intermediate files (`.casm`, `.cast`) are created on disk. All decryption occurs in protected memory.
*   **Running source files (`.py`, `.rs`)**: The CLI compiles source code for execution.
    *   By default, `exo run source.py` uses temporary directories for intermediate artifacts, which are deleted immediately after execution.
    *   To persist artifacts for debugging, use `exo compile source.py` manually.
