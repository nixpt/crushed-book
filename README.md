# Crushed: The Guide to Exosphere

![Book Cover](src/assets/cover.png)

This repository contains the source code and assets for **Crushed**, the official technical handbook and user manual for the **Exosphere** ecosystem.

## 📖 About the Book
"Crushed" is designed to be a comprehensive resource for developers, architects, and agents transitioning to the **Agent-Native OS** paradigm. It covers everything from the core philosophical contracts to low-level CASM bytecode specifications.

### Key Sections
-   **The Vision**: Philosophical foundations of Exosphere.
-   **Architecture**: Deep dives into the CRUSH VM and EXO Kernel.
-   **Language Reference**: Specifications for CAST and CASM.
-   **Developer SDKs**: Guides for building capsules in Rust and Python.
-   **Cookbook**: Practical, secure implementation patterns.

---

## 🛠️ Building the Book
The book is built using **[mdBook](https://github.com/rust-lang/mdBook)**.

### Prerequisites
-   Rust & Cargo
-   mdBook (`cargo install mdbook`)

### Local Development
```bash
# Build the book
mdbook build

# Serve the book locally with hot-reloading
mdbook serve --open
```

The generated HTML will be located in the `book/` directory.

---

## 🎨 Branding & Identity
This repository also serves as the central hub for the **Exosphere Design System** and branding assets. High-fidelity logos, icons, and technical illustrations can be found in `src/assets/`.

---
© 2026 Exosphere Project | [Exosphere Root](https://github.com/nixpt/Exosphere)
