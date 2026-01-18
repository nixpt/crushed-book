# Variable Scoping and Environment in CRUSH

CRUSH uses a flat local environment per function and a shared registry for cross-capsule data.

## Environment Scoping

### 1. Function Local Environment
Each function call has its own `HashMap<String, RuntimeValue>`. Variables are stored and loaded from this environment using the `store` and `load` CASM instructions.

### 2. Shared Registry
The VM maintains a `shared_registry` for variables that need to be accessed across function boundaries or by different capsules.
- `export_var`: Moves a value from the stack into the shared registry.
- `import_var`: Loads a value from the shared registry onto the stack.

## Data Types

Variables can hold any `RuntimeValue`:
- Primitives: `Int`, `Float`, `Bool`, `Null`.
- Arena References: `Str`, `Array`, `Map`, `Object`.

---

## See Also

- [API Reference](../API_REFERENCE.md)
- [Pointers & Memory](pointers.md)