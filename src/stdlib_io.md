# I/O Module (`io`)

Provides input and output capabilities.

## Capabilities

### `io.print`
Prints arguments to standard output, followed by a newline.
- **Args**: `vl: Any...`
- **Example**: `io.print("Hello", 123)`

### `io.echo`
Prints arguments to standard output, separated by spaces, followed by a newline.
- **Args**: `vl: Any...`
- **Example**: `io.echo("Hello", "World")`

### `io.input`
Reads a line from standard input.
- **Args**: None
- **Returns**: `String`
- **Example**: `var name = io.input()`
