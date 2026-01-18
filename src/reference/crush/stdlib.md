# Standard Library

The Crush standard library provides additional capabilities and utilities beyond the core language. This chapter provides an overview and links to detailed documentation.

## Importing Modules

```crush
import std.io;
import std.fs;
import std.net;
import std.sys;
```

### With Aliases

```crush
import std.fs as filesystem;
import std.io as console;
```

## Available Modules

### I/O Module (`std.io`)

Input/output operations:

- `@io.print(message)` - Print to stdout
- `@io.read()` - Read from stdin
- `@io.eprint(message)` - Print to stderr

See the [main documentation](../../book/stdlib_io.md) for complete details.

### Filesystem Module (`std.fs`)

File and directory operations:

- `@fs.read(path)` - Read file
- `@fs.write(path, content)` - Write file
- `@fs.exists(path)` - Check if exists
- `@fs.delete(path)` - Delete file
- `@fs.list(path)` - List directory

See the [main documentation](../../book/stdlib_fs.md) for complete details.

### System Module (`std.sys`)

System-level operations:

- `@sys.exec(command)` - Execute command
- `@sys.env(name)` - Get environment variable
- `@sys.args()` - Get command-line arguments
- `@sys.exit(code)` - Exit program

See the [main documentation](../../book/stdlib_system.md) for complete details.

### Network Module (`std.net`)

Network operations:

- `@net.http(url)` - HTTP request
- `@net.get(url)` - HTTP GET
- `@net.post(url, body)` - HTTP POST

## Example Usage

```crush
import std.io;
import std.fs;
import std.sys;

fn main() {
    // Get command-line arguments
    let args = @sys.args();
    
    if args.length < 2 {
        @io.eprint("Usage: program <filename>");
        @sys.exit(1);
    }
    
    let filename = args[1];
    
    // Check if file exists
    if @fs.exists(filename) {
        let content = @fs.read(filename);
        @io.print(content);
    } else {
        @io.eprint("File not found: " + filename);
        @sys.exit(1);
    }
}
```

## Next Steps

For complete standard library documentation, see:

- **[I/O Module](../../book/stdlib_io.md)** - Input/output operations
- **[Filesystem Module](../../book/stdlib_fs.md)** - File operations
- **[System Module](../../book/stdlib_system.md)** - System operations
- **[Main Documentation](../../book/stdlib.md)** - Complete stdlib reference
