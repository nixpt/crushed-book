# Encrypted Execution

CRUSH supports a comprehensive Encrypted Execution environment designed for high-security workloads. This allows you to "compile once, run confidentially" anywhere.

## Key Features

1.  **Confidentiality**: The capsule bytecode is encrypted using ChaCha20-Poly1305.
2.  **Integrity**: The execution package (`.ecap`) is integrity-protected with a Merkle Tree.
3.  **Key Management**: Keys are managed via the OS Keyring and derived hierarchically.
4.  **Auditability**: A cryptographic transcript of execution is logged to verify what code ran.

## commands

*   `crush key generate`: Create a master key.
*   `crush encrypt <file>`: Encrypt a `.casm` file.
*   `crush inspect <file>`: Verify an encrypted package.
*   `exo run <file>`: Execute (automatically handles decryption).

## Architecture

The VM uses a specialized `EncryptedProgramContext` to fetch instructions. Instead of loading the entire program into memory, it:
1.  Decrypts 4KB pages on-demand.
2.  Locks them in memory (`mlock`) to prevent swapping.
3.  Clears them immediately after use (LRU cache).

For a full guide, see the [Encrypted Execution Guide](../../guides/ENCRYPTED_EXECUTION.md).
