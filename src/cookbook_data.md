# Cookbook: Secure Data Processing

This recipe shows how to build a capsule that processes sensitive data (e.g., logs, financial records) with strict I/O scoping.

## 🥣 Ingredients

-   **`fs.read:/input/*`**: Read-only access to the input folder.
-   **`fs.write:/output/*`**: Write-only access to the results folder.
-   **`Encrypted VM Mode`**: Ensures memory is never swapped to disk in plaintext.

---

## 👨‍🍳 Implementation (Python)

```python
from crush_sdk import Capsule, fs, io

class DataProcessor(Capsule):
    def run(self, entry_point):
        io.print("Scanning /input for new records...")
        
        for filename in fs.list("/input"):
            data = fs.read(f"/input/{filename}")
            
            # Perform processing (pseudo-code)
            result = self.process_sensitive_data(data)
            
            output_name = f"/output/processed_{filename}"
            fs.write(output_name, result)
            io.print(f"Archived result to {output_name}")

    def process_sensitive_data(self, data):
        # Logic here...
        return data.upper() # Example
```

---

## 📝 The Manifest (`Capsule.toml`)

```toml
[capsule]
name = "secure-processor"
version = "1.0.0"

[permissions]
required = ["fs.read", "fs.write", "io.print"]
scopes = [
    "fs.read:/input/*", 
    "fs.write:/output/*"
]
```

## 🛡️ The "Isolated Sink" Pattern

This pattern is called an **Isolated Sink**. The capsule can ingest data from one pipe and output to another, but it cannot "leak" that data to the network or other capsules because it lacks the `net` or `icc` capabilities.

This makes it the perfect environment for:
- **Privacy-Preserving AI**: Run LLMs on local data without fear of telemetry leaks.
- **Log Aggregation**: Scrub PII from logs before they hit long-term storage.
- **Credit Card Processing**: Handle PCI data in a dedicated, tamper-proof sandbox.
