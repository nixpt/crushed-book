# Visual Coordination & File Icons

Exosphere uses a "Truth First" visual strategy. Technical system state should be obvious at a glance through consistent file identifiers and icons.

## Canonical Identifiers

Before integrating icons, we must lock down the identifiers that Operating Systems and IDEs hook into.

### File Extensions

| Extension | Content Type | MIME Type |
|-----------|--------------|-----------|
| `.casm` | CRUSH Assembly (Bytecode) | `application/x-crush-casm` |
| `.crush` | Capsule Manifests / Logic | `application/x-crush-capsule` |
| `.cap` | Compiled Capsule Bundle | `application/x-crush-capsule` |
| `.ecap` | Encrypted Capsule Bundle | `application/x-crush-ecapsule` |
| `.joker` | Joker Protocol State & Plans | `application/x-joker-protocol` |
| `.exo` | Exosphere Kernel/Config | `application/x-exosphere-config` |

---

## IDE Integration

### VS Code
The **Exosphere Icons** extension provides high-fidelity icons for all canonical extensions.

**Installation:**
1. Navigate to `crush-sdk/tools/vscode-exosphere`.
2. Pack the extension: `vsce package`.
3. Install the `.vsix` file in VS Code.

### JetBrains (IntelliJ, CLion, etc.)
JetBrains users can associate icons via the **File Types** setting or by installing the Exosphere JetBrains plugin (Coming Soon).

---

## Operating System Integration

### Linux (GNOME, KDE)
Linux desktops resolve icons via MIME associations. Run the following to register Exosphere types locally:

```xml
<!-- ~/.local/share/mime/packages/exosphere.xml -->
<mime-info xmlns="http://www.freedesktop.org/standards/shared-mime-info">
  <mime-type type="application/x-crush-casm">
    <comment>CRUSH Assembly</comment>
    <glob pattern="*.casm"/>
    <icon name="application-x-crush-casm"/>
  </mime-type>
</mime-info>
```

### macOS & Windows
Integration on these platforms is typically handled via the **Exosphere Toolchain** installer or the **Teddy IDE** desktop bundle.

---

## Icon Assets
All canonical icons are maintained as pure SVGs for maximum scalability and ROI. You can find them in `crush-sdk/assets/icons/`.

![CASM Icon](assets/icons/casm.svg)
![Crush Icon](assets/icons/crush.svg)
![Cap Icon](assets/icons/cap.svg)
![ECap Icon](assets/icons/ecap.svg)
![Joker Icon](assets/icons/joker.svg)
![Exo Icon](assets/icons/exo.svg)
