# Exosphere Design System (v1.0)

This document formalizes the visual tokens and design language for the CRUSH ecosystem, ensuring a unified "OS-like" experience across all tools and interfaces.

## 1. Core Color Palette

The palette is inspired by "Luxury Cyberpunk": glassmorphism, neon glows, and high-contrast technical surfaces.

### 1.1 Primary Tokens (Tokens)

| Token | Name | HEX | HSL | Terminal (ANSI) | Purpose |
|---|---|---|---|---|---|
| `@exo-cyan` | **Boundary** | `#00D2FF` | `191, 100%, 50%` | `Cyan` / `36` | Hexagons, VM boundaries, Ports |
| `@exo-amber` | **Kernel Core** | `#FF9F00` | `37, 100%, 50%` | `Yellow` / `33` | Kernel Cube, Security Alerts, Gas |
| `@exo-indigo` | **Polyglot Logic** | `#6B46C1` | `258, 53%, 52%` | `Magenta` / `35` | User code, Variable names |
| `@exo-green` | **Capability OK** | `#48BB78` | `145, 45%, 51%` | `Green` / `32` | Granted authority, Audit success |
| `@exo-red` | **Boundary Breach** | `#E53E3E` | `0, 77%, 57%` | `Red` / `31` | Access Denied, Encryption locks |
| `@exo-white` | **Primary Data** | `#EDF2F7` | `210, 38%, 95%` | `White` / `37` | Primary text, Manifest values |

## 2. Terminal Theming (CLI)

### 2.1 UI Accents
*   **Prompt**: `@exo-cyan` hex-dot, `@exo-green` user, `@exo-white` text.
*   **Banners**: V2 ASCII art using `@exo-cyan` for frames and `@exo-amber` for core icons.

### 2.3 Official Themes
The Exosphere Dark aesthetic is available for several major terminal emulators:

*   **[Alacritty](themes/exosphere_alacritty.toml)**
*   **[Kitty](themes/exosphere_kitty.conf)**
*   **[iTerm2](themes/exosphere_iterm.itermcolors)**

These themes transform the terminal background to a deep Exosphere Charcoal (`#0F172A`) and map the standard ANSI colors to our official design tokens.

## 3. Visual Metaphors

1.  **Isolation**: Translucent glass, closed hexagonal perimeters.
2.  **Authority**: Glowing "Ports" (nodes) on the perimeter.
3.  **Auditability**: Unbroken vertical streams of data (Ledgers).
4.  **Density**: Minimalist icons with high internal detail (3D renders).

## 4. Typography

*   **Monospace (Primary)**: *JetBrains Mono* or *Fira Code* (with Ligatures).
*   **Display**: *Outfit* (Semi-bold) for headings and high-fidelity branding.

## 5. Implementation Guide

All tools (`vortex`, `teddy`, `crush-cli`) should use the central `branding` package or environment variables to pull these tokens, ensuring that a theme change in one updates the entire toolchain.
