# Exosphere OS: Agent-Native Operating System

## 1. The Vision: Stripping the Kernel

The long-term goal of Exosphere is to transition from an application layer to a **standalone, agent-native operating system**. In this architecture, the Linux kernel serves as a high-performance **Hardware Abstraction Layer (HAL)**, while all higher-level services are implemented as decentralized Exosphere Capsules.

### Key Architectural Pillars:
- **Exosphere as `PID 1`**: The Exosphere Core acts as the init system, managing capsule lifecycles and resource quotas directly.
- **Micro-Kernel Philosophy**: Minimal host userland. Traditional tools (ls, cat, bash) are replaced by **CoreCaps** (Crush/Rust capsules).
- **Nexquelium Compositor**: Instead of a traditional Desktop Environment, Nexquelium serves as the Wayland compositor, rendering capability-governed capsule views.

## 2. NixOS Integration

NixOS provides the ideal foundation for building Exosphere OS due to its **declarative configuration** and **immutable system state**.

- **Exosphere-as-a-Flake**: The entire OS, including the custom kernel parameters, Wayland drivers, and the Exosphere Core, will be defined in a `flake.nix`.
- **Reproducible Images**: Using `nixpkgs.lib.nixosSystem` and the `iso-image` generator, we can produce bootable Exosphere OS images that are consistent across all hardware.
- **Atomic Rollbacks**: System-level upgrades or capsule runtime changes can be rolled back instantly if an anomaly is detected by the Sentry agent.

## 3. Testing & Development Strategy

Building an OS from scratch is complex, so we prioritize **Virtual Environments** for rapid iteration.

### QEMU / KVM
QEMU is the primary target for early "Metal" testing. It allows us to:
- Test the booting of the Exosphere Core as the init process.
- Debug Wayland surface rendering in a controlled virtual GPU environment (`virtio-gpu`).
- Simulate network partitions and resource exhaustion to test Sentry agent resilience.

### VirtualBox
For a more consumer-facing "Appliance" experience, we will provide VirtualBox `.ova` images. This allows developers to run "Exosphere-in-a-Box" on Windows/macOS/Linux hosts without altering their primary machine.

## 4. Roadmap to "The Metal"

1.  **Stage 1: The Nix Flake**: Define the system dependencies and build the Exosphere-Core as a Nix package.
2.  **Stage 2: The Init Test**: Boot a minimal NixOS kernel that skips `systemd` and executes a "Hello World" Crush capsule as the first process.
3.  **Stage 3: The Graphical Boot**: Initialize a minimal Wayland compositor (via Nexquelium) and render the Sentry Dashboard upon startup.
4.  **Stage 4: Hardware ISO**: Release a bootable ISO for x86_64 and ARM64 devices.

---

**Conclusion**: By combining the declarative power of **NixOS** with the capability-driven execution of **Exosphere**, we create an OS where security is not a "permission," but a structural guarantee enforced by agents and capsules.
