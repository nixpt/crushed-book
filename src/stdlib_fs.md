# Filesystem Module (`fs`)

Provides capabilities for file and directory manipulation.

## Capabilities

### `fs.read`
Reads the entire content of a file as a string.
- **Args**: `path: String`
- **Returns**: `String`
- **Example**: `var content = fs.read("data.txt")`

### `fs.write`
Writes a string to a file, overwriting it or creating it if it doesn't exist.
- **Args**: `path: String`, `content: String`
- **Returns**: `Null`
- **Example**: `fs.write("log.txt", "Log entry")`

### `fs.ls`
Lists the contents of a directory.
- **Args**: `path: String` (optional, defaults to current dir)
- **Returns**: `Array<String>`
- **Example**: `var files = fs.ls(".")`

### `fs.cd`
Changes the current working directory.
- **Args**: `path: String`
- **Returns**: `Null`
- **Example**: `fs.cd("/tmp")`

### `fs.pwd`
Returns the current working directory.
- **Args**: None
- **Returns**: `String`
- **Example**: `var cwd = fs.pwd()`

### `fs.mv`
Moves or renames a file or directory.
- **Args**: `from: String`, `to: String`
- **Returns**: `Null`
- **Example**: `fs.mv("old.txt", "new.txt")`

### `fs.rm`
Removes a file or directory.
- **Args**: `path: String`
- **Returns**: `Null`
- **Example**: `fs.rm("temp.txt")`
