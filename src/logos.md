# CRUSH ASCII Logo Variants (v2)

Official ASCII art logos for the CRUSH project, updated to reflect the premium 3D visual identity.

## 1. Canonical Logo (v2)

**Use for:** `crush --version`, CLI startup banner, documentation headers.
**Design:** Vaulted Hexagon with isolated Kernel Cube.

```text
            .─────.
           /       \
          o  ┌───┐   o
             │[#]│
          o  └───┘   o
           \       /
            '─────'

         C R U S H
```

**ANSI Color Mapping:**
- **Cyan**: Hexagon boundary (`.─────.`, `/ \`, `\ /`, `'─────'`)
- **Green**: Capability nodes (`o`)
- **Yellow**: Kernel Cube frame (`┌───┐`, `│ │`, `└───┘`)
- **White**: Kernel core (`[#]`)
- **Multi-Color**: Project name (`C R U S H`)

---

## 2. Circuit Banner (Minimal v2)

**Use for:** `crush help`, REPL startup, compact displays.

```text
  ┌─────o─────┐
  │ ┌───────┐ │  CRUSH
  │ │  [#]  │ │  [v0.1.0-alpha]
  └─────o─────┘
```

---

## 3. Pixel Prompt (REPL v2)

**Use for:** Interactive REPL prompt.

```text
 .-.
[#]
 '-' 
```

---

## 4. Abstract Cube (One-Line)

**Use for:** Logs, CI, and technical status bars.

```text
     _ ___ _
   /___ ___/|
  |   |   | |  CRUSH
  |___|___|/
```

---

## Design Philosophy

The V2 ASCII art moves away from plain characters to **Box-Drawing Unicode characters** (`┌`, `┐`, `└`, `┘`, `│`, `─`) where supported, fallback to robust ASCII otherwise. 

It visually reinforces:
1.  **3D Layering**: Shading and depth hints.
2.  **Architectural Hierarchy**: The kernel is clearly nested within the VM boundary.
3.  **Authority Points**: Capability nodes are strategically placed as connection "ports."
