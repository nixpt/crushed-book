# CRUSH Type System

The CRUSH type system is based on the `RuntimeValue` enum, which provides a safe and flexible way to represent data across polyglot boundaries.

## RuntimeValue Variants

- **Int(i64)**: Signed 64-bit integer.
- **Float(f64)**: 64-bit floating point.
- **Bool(bool)**: Boolean value.
- **Str(String)**: UTF-8 string stored in the Arena.
- **Ref(usize)**: A reference (index) to an object in the Arena.
- **Null**: Represents the absence of a value.

## Arena Objects

The `Ref` type points to complex objects managed by the `Arena`:

- **Array**: A vector of `RuntimeValue`s.
- **Map**: A hash map with string keys and `RuntimeValue` values.
- **Object**: A generic object structure.
- **Tagged**: A value with associated type metadata.

---

## See Also

- [Memory Management](../memory/pointers.md)
- [API Reference](../API_REFERENCE.md)