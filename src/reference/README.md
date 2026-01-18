# Crushed: The Crush Language Guide

Welcome to **Crushed**, the comprehensive language reference for **Crush** and **CASM** (Crush Assembly).

## What is Crush?

Crush is a modern, capability-based scripting language designed for **polyglot programming**. It allows you to seamlessly combine code from multiple languages (Python, JavaScript, Bash, Rust, C, Go) in a single program while maintaining security through a capability-based permission system.

## What is CASM?

CASM (Crush Assembly) is the low-level bytecode format that powers the Crush Virtual Machine. It's a stack-based instruction set that serves as the compilation target for all languages in the Crush ecosystem.

## Architecture Overview

```text
┌─────────────────────────────────────────┐
│  Source Languages                       │
│  (Crush, Python, JS, Bash, Rust, C, Go) │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Language Walkers                       │
│  (Tree-sitter based parsers)            │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  CAST (Crush Abstract Syntax Tree)      │
│  (Universal intermediate representation) │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  CASM Compiler                          │
│  (CAST → CASM bytecode)                 │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  CASM Bytecode                          │
│  (Stack-based assembly)                 │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Crush VM                               │
│  (Isolated execution with capabilities) │
└─────────────────────────────────────────┘
```

## Who is this book for?

This book is for:

- **Crush developers** who want to write programs in the Crush language
- **Polyglot programmers** who want to combine multiple languages in one project
- **Language implementers** who want to add support for new languages to Crush
- **VM developers** who want to understand the CASM bytecode format
- **Security researchers** interested in capability-based security models

## How to use this book

This book is divided into three main parts:

### Part I: CASM (Crush Assembly)

Learn about the low-level bytecode format that powers Crush. This section covers:
- The CASM instruction set
- Program structure and serialization
- Writing and debugging CASM programs

**Start here if:** You want to understand how Crush works under the hood, or you're implementing a language walker.

### Part II: Crush Language

Learn the Crush programming language from basics to advanced features:
- Syntax and semantics
- Data types and operators
- Control flow and functions
- The capability system
- Polyglot programming

**Start here if:** You want to write Crush programs.

### Part III: Advanced Topics

Deep dive into advanced concepts:
- The compilation pipeline
- Writing language walkers
- Performance optimization

**Start here if:** You're extending Crush or optimizing performance-critical code.

## Quick Start

### Hello World in Crush

```crush
fn main() {
    @io.print("Hello, World!");
}
```

### Hello World in CASM

```json
{
  "version": "0.1",
  "functions": {
    "main": {
      "params": [],
      "locals": [],
      "body": [
        {"op": "push_str", "value": "Hello, World!"},
        {"op": "cap_call", "name": "io.print", "argc": 1},
        {"op": "ret"}
      ]
    }
  }
}
```

## Additional Resources

- [Main Crush Documentation](../book/README.md) - Architecture, VM, and system design
- [GitHub Repository](https://github.com/nixpt/crush) - Source code and examples
- [API Reference](../docs/API_REFERENCE.md) - Complete API documentation

## Contributing

Found an error or want to improve the documentation? Contributions are welcome! See the [Contributing Guide](../CONTRIBUTING.md) for details.

---

Let's get started! Choose a section from the table of contents to begin your journey with Crush and CASM.
