# Performance Optimization

Tips and techniques for optimizing Crush programs.

## Bytecode Optimization

### Minimize Stack Operations

```crush
// Less efficient
let a = 1;
let b = 2;
let c = 3;
let result = a + b + c;

// More efficient
let result = 1 + 2 + 3;
```

### Reduce Function Calls

```crush
// Less efficient
for i in range(0, 1000) {
    process(i);
}

// More efficient (if possible)
process_batch(range(0, 1000));
```

## Capability Call Overhead

Capability calls have overhead. Batch operations when possible:

```crush
// Less efficient: Multiple calls
@fs.write("file1.txt", "data1");
@fs.write("file2.txt", "data2");
@fs.write("file3.txt", "data3");

// More efficient: Batch write (if supported)
@fs.write_batch([
    {"path": "file1.txt", "data": "data1"},
    {"path": "file2.txt", "data": "data2"},
    {"path": "file3.txt", "data": "data3"}
]);
```

## Language Block Overhead

Each language block has initialization overhead:

```crush
// Less efficient: Multiple blocks
@python { x = 1 }
@python { y = 2 }
@python { z = x + y }

// More efficient: Single block
@python {
    x = 1
    y = 2
    z = x + y
}
```

## Use Native Code for Performance

For performance-critical sections, use compiled languages:

```crush
// Use Rust for compute-intensive tasks
@rust {
    fn compute_intensive() -> i64 {
        let mut sum = 0;
        for i in 0..1_000_000 {
            sum += i * i;
        }
        sum
    }
    
    result = compute_intensive();
}
```

## Profiling

```bash
# Profile your program
crush run --profile program.crush

# View profile report
crush profile-report
```

## Binary Format

Use binary format for faster loading:

```bash
# Compile to binary
crush compile program.crush --output program.casmb

# Binary loads 2-3x faster
crush run program.casmb
```

## Next Steps

- **[Compilation](compilation.md)**: Understanding the pipeline
- **[CASM Reference](../casm/instruction_reference.md)**: Low-level optimization
