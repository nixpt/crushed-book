# Python SDK Guide

The **Crush Python SDK (`crush-sdk-py`)** allows you to leverage Python's rich ecosystem (AI, Data Science, Scripting) inside the secure Exosphere environment.

## 📦 Installation

```bash
pip install crush-sdk
```

## 🛠️ Build Your First Capsule

In Python, you inherit from the `Capsule` base class.

```python
from crush_sdk import Capsule, Manifest, run_capsule

class MyAgent(Capsule):
    def init(self, manifest: Manifest):
        print(f"Agent '{manifest.name}' is waking up...")

    def run(self, entry_point: str):
        if entry_point == "main":
            self.execute_task()

    def execute_task(self):
        # Using capabilities
        from crush_sdk import io, fs
        io.print("Scanning data directory...")
        
        files = fs.list("/data")
        print(f"Found {len(files)} files.")

# The entry point that ties into the CRUSH runtime
if __name__ == "__main__":
    run_capsule(MyAgent())
```

---

## 🧠 Why Python for Agents?

Exosphere is designed to solve the "Trust Problem" for AI agents. By running a Python agent in an Exosphere capsule, you get:
- **Sandbox Safety**: The agent can only touch the files and URLs you explicitly allow.
- **Resource Limits**: Prevent an unoptimized agent from consuming all host RAM or CPU.
- **Auditability**: Every action the agent takes is mediated and logged by the kernel.

---

## 🛡️ Using Capabilities

The Python SDK exposes capabilities as standard Python functions, but they are internally redirected to the CRUSH HAL.

### Networking
```python
from crush_sdk import net

# Fetches content securely if net.http_get is in permissions
html = net.http_get("https://example.com")
```

### Inter-Capsule Communication (IPC)
```python
from crush_sdk import icc

# Request data from a database capsule
result = icc.call("db-service", {"action": "query", "sql": "SELECT * FROM users"})
```

---

## 📝 The Manifest (`Capsule.toml`)

Just like Rust capsules, Python capsules require a manifest.

```toml
[capsule]
name = "python-ai-agent"
version = "0.1.0"
capsule_type = "agent"
entry_point = "main"

[permissions]
required = ["io.print", "fs.list", "net.http_get"]
scopes = ["net.http_get:https://*.google.com/*"]
```

## 🚀 Deployment

Python capsules are packed along with a minimal Python runtime (or a reference to one) and distributed as `.cap` files using `packman`.
