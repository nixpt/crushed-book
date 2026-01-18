# CASM: Assembly & Bytecode

**CASM (Crush Assembly)** is the low-level language of the CRUSH Virtual Machine. It is a stack-oriented bytecode format designed for performance, security, and deterministic execution.

## The Stack Model

CRUSH is a **Stack-Based VM**. Operands are pushed onto a data stack, and instructions operate on the top-most values.

```casm
// Adding 2 + 3
PUSH 2
PUSH 3
ADD
// Result (5) is now on top of the stack
```

---

## 📋 Instruction Set Overview

### 1. Data Movement
- **`PUSH <value>`**: Push a literal onto the stack.
- **`STORE <id>`**: Pop value and store in local/global variable.
- **`LOAD <id>`**: Load value from variable onto stack.
- **`POP`**: Discard the top value.

### 2. Arithmetic & Logic
- **`ADD`, `SUB`, `MUL`, `DIV`**: Basic math operations.
- **`EQ`, `LT`, `GT`**: Comparison operations.
- **`AND`, `OR`, `NOT`**: Logical operations.

### 3. Flow Control
- **`JUMP <target>`**: Unconditional jump to a label.
- **`JUMP_IF_FALSE <target>`**: Jump if the top value is false.
- **`CALL <id>`**: Invoke a function or capability.
- **`RET`**: Return from a function.

---

## 🔒 Capability Invocation

Capability calls are the "System Calls" of the CRUSH VM. They are invoked using the `CALL` instruction with a capability identifier.

```casm
// Printing "Hello"
PUSH "Hello"
CALL io.print
```

### Gas and Limits
Every CASM instruction has a fixed "Gas Cost." The VM tracks the total gas consumed by a capsule and terminates it if it exceeds its allocated quota. This prevents infinite loops and resource exhaustion attacks.

## CASM Artifact Format

CASM is typically distributed as a JSON binary blob (ending in `.casm.json`). This allows for easy inspection and debugging during development.

```json
{
  "version": "1.0",
  "instructions": [
    {"opcode": "PUSH", "arg": {"Integer": 42}},
    {"opcode": "CALL", "arg": "io.print"}
  ],
  "manifest": {
    "name": "example",
    "permissions": ["io.print"]
  }
}
```
