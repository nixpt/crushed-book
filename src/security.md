# Capability-Based Security

Exosphere rejects the "ACL" (Access Control List) model in favor of **Capability-Based Security**.

## The Metadata Metaphor: Unforgeable Tokens

Imagine a traditional OS where every file has a "list of allowed users." To open a file, the system checks if you are on the list.

In Exosphere, resources are shielded. To access a resource, you must possess an **Unforgeable Token** (a Capability). If you have the key, you can open the door. If you don't, the door doesn't even exist in your reality.

![Security Metaphor](assets/security_metaphor.png)

## Anatomy of a Capability

Capabilities in Exosphere follow a structured format: `namespace.action:scope`.

- **Namespace**: The resource category (e.g., `fs`, `net`, `hw`).
- **Action**: What you can do (e.g., `read`, `write`, `open`).
- **Scope**: The specific constraint (e.g., `/data/tmp/*`, `port:8080`).

### Example: Filesystem Capability
`fs.read:/etc/config.json` grants exactly what it says: read access to one specific file.

---

## The Mediation Flow

1.  **Declaration**: The capsule defines its needs in the `Capsule.toml` (Manifest).
2.  **Attestation**: At load time, the Orchestrator verifies the manifest and checks the host's security policy.
3.  **Instantiation**: If approved, the VM is started with a `ScopedHal` containing the specific capabilities.
4.  **Invocation**: When the code calls `fs.read`, the VM validates the call against the capsule's granted capabilities.
5.  **Execution**: The `ScopedHal` executes the request through the `NativeHal`, translating virtual paths/handles to real ones.

## 🛡️ Security Guarantees

- **No Ambient Authority**: Capsules start with zero permissions.
- **PoLP (Principle of Least Privilege)**: Only the exact capabilities needed are granted.
- **Reference Monitor**: The `exo-core` acts as a central reference monitor that cannot be bypassed.
- **Cryptographic Audit**: (Optional) In Encrypted Mode, every capability invocation is cryptographically signed and logged.
