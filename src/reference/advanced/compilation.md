# Compilation Pipeline

This chapter explains how Crush source code is transformed into executable bytecode.

## Pipeline Overview

```text
┌──────────────────────┐
│  Crush Source Code   │
│  (.crush file)       │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  Lexer & Parser      │
│  (Syntax Analysis)   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  CAST Generation     │
│  (Abstract Syntax    │
│   Tree)              │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  CASM Compiler       │
│  (Code Generation)   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  CASM Bytecode       │
│  (.casm file)        │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  Crush VM            │
│  (Execution)         │
└──────────────────────┘
```

## Stages

### 1. Lexing and Parsing

Converts source code into an Abstract Syntax Tree (AST).

### 2. CAST Generation

Transforms language-specific AST into universal CAST format.

### 3. CASM Compilation

Compiles CAST to stack-based CASM bytecode.

### 4. Execution

The Crush VM executes the CASM bytecode.

## Using the Compiler

```bash
# Compile Crush to CASM
crush compile program.crush

# Run directly (compiles and executes)
crush run program.crush

# Compile to binary format
crush compile program.crush --output program.casmb
```

## Next Steps

- **[Writing Walkers](walkers.md)**: Add support for new languages
- **[Performance](performance.md)**: Optimization techniques
