# Crush VM

The **Crush VM** (`crush-vm`) is a stack-based virtual machine designed to execute **CASM** (Crush Assembly).

## Key Components

### 1. The Stack
Stores temporary values (`RuntimeValue`) during computation.
- Integers (`i64`)
- Floats (`f64`)
- Booleans (`bool`)
- References (`Ref`) to heap objects

### 2. The Arena
A heap that stores complex objects like Strings, Arrays, and Maps. This avoids complex lifetime management in the VM implementation, using simple integer indices (`Ref`) instead.

### 3. The Registry
Holds the set of available **Capabilities**. When the VM encounters a `cap_call` instruction, it looks up the implementation in the Registry.

### 4. Manifest Enforcement
When initialized with a `Manifest`, the VM enforces that the code can only call capabilities explicitly listed in the manifest's `allowed_capabilities` section. It also wraps the system HAL in a `ScopedHal` for process-level isolation.

### 5. Local Scope Management
The VM implements nested scope management for functions. Each function call creates a new local environment where parameters are bound to arguments, ensuring variables do not leak between function boundaries while allowing access to global and shared registries.
