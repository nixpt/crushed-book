# Hello World

Let's write a simple Crush script.

## 1. Create a File

Create a file named `hello.crush` with the following content:

```python
# hello.crush
def main():
    io.print("Hello, World!")
```

## 2. Run It

Execute the script using the `crush` CLI:

```bash
crush run hello.crush
```

You should see:
```text
Hello, World!
```

## 3. How It Works

1. **Source**: The `.crush` file is parsed into an AST.
2. **Compilation**: The AST is compiled into CASM (Crush Assembly) instructions.
3. **VM**: The Crush VM executes the instructions.
4. **Capabilities**: The `io.print` function is a *capability* provided by the standard library. The VM ensures the script has permission (though currently `io.print` is often permissible by default or part of the base set).
