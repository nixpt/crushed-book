# System Module (`system`)

Provides access to system information and environment.

## Capabilities

### `system.env`
Returns a Map of all environment variables.
- **Args**: None
- **Returns**: `Map<String, String>`
- **Example**: `var env = system.env(); io.print(env.PATH)`

### `system.os`
Returns information about the operating system.
- **Args**: None
- **Returns**: `Map<String, String>` containing `os`, `arch`, `family`.
- **Example**: `var info = system.os(); io.print(info.os)`
