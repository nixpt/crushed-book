# Agent Communication Protocol (ACP)

> "The Nervous System of Exosphere."

ACP is the specialized IPC (Inter-Process Communication) and RPC (Remote Procedure Call) protocol for Agents. It supersedes generic HTTP for agent-to-agent and agent-to-host communication.

## Protocol Layers

1.  **Transport**: Unix Domain Sockets (local) or QUIC (remote).
2.  **Formatting**: JSON-RPC 2.0.
3.  **Security**: All messages are signed by the sender's **Capsule Identity**.

## Capabilities

ACP handles:

*   **Tool Use**: Calling functions in other capsules (`acp.call_tool`).
*   **Resource Sharing**: Sending file handles or memory references.
*   **Coordination**: Heartbeats and status updates to the Joker Coordinator.

## Example

```json
// Request
{
  "jsonrpc": "2.0",
  "method": "capsule.calculate_pi",
  "params": { "precision": 100 },
  "id": 1,
  "headers": {
    "sender": "cap_xyz...",
    "signature": "sig_abc..."
  }
}
```
