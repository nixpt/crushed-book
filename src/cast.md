# CAST: The Abstract Syntax Tree

**CAST (Crush Abstract Syntax Tree)** is the middle-man of the Exosphere ecosystem. It is a JSON-serializable representation of program logic that is easy for walkers to generate and for the compiler to consume.

## Structure of a CAST Node

Every node in the CAST is a structured object. A typical node looks like this:

```json
{
  "kind": "BinaryExpr",
  "op": "Add",
  "left": {
    "kind": "Literal",
    "value": {"Integer": 5}
  },
  "right": {
    "kind": "Literal",
    "value": {"Integer": 10}
  }
}
```

---

## 🛠️ Core Node Types

### 1. Declarations
- **`Function`**: Defines a callable block of code.
- **`Variable`**: Defines a named storage location.
- **`Struct`**: Defines a composite data type (Coming Soon).

### 2. Expressions
- **`Literal`**: Primitive values (Int, Float, String, Bool, Null).
- **`Identifier`**: Reference to a variable or function.
- **`Call`**: Invokes a function or capability.
- **`BinaryExpr`**: Arithmetic and logical operations (`+`, `-`, `*`, `/`, `&&`, `||`).

### 3. Statements
- **`If`**: Branched execution.
- **`While`**: Loop control.
- **`Return`**: Exits a function.
- **`Block`**: A sequence of statements.

---

## 🌀 Standard Library Normalization

The main power of CAST is its ability to normalize native language features into CRUSH capabilities. For example, a Python `print()` call is translated into a CAST `Call` node targeting the `io.print` capability.

```python
# Python Source
print("Hello")

# Equivalent CAST (Simplified)
{
  "kind": "Call",
  "name": "io.print",
  "args": [{"kind": "Literal", "value": {"String": "Hello"}}]
}
```

This ensures that the compiler only needs to know how to emit CASM for the `Call` node, regardless of the source language's syntax.
