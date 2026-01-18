# Cookbook & Examples

The Exosphere Cookbook is a collection of practical, battle-tested patterns for building production-ready capsules.

---

## 🥘 Common Recipes

### 1. [Building a Web Service](cookbook_web.md)
Learn how to use the `net` and `io` capabilities to create a secure, isolated HTTP server.

### 2. [Secure Data Processing](cookbook_data.md)
Patterns for reading sensitive data, processing it in an isolated VM, and writing results to a scoped output.

### 3. [Cross-Language Integration](cookbook_polyglot.md)
How to build a "Spider" capsule that uses Rust for speed and Python for logic, sharing data through CASM.

---

## 🧪 Testing Your Recipes

Every recipe in this book includes a companion test script in the `tests/` directory of the Exosphere repo.

```bash
# Run all cookbook tests
cargo test --test cookbook_*
```

## 🚀 Pro-Tip: The "Zero-Knowledge" Pattern
When building agents that handle private keys or sensitive data, always use the **Encrypted VM** mode. This ensures that even if the host machine is compromised, your capsule's memory remains unreadable.
