# Pacman

**Pacman** is the Package Manager for Crush. It manages **Capsules**, which are isolated units of software.

## Philosophy

Pacman manages capsules in a local registry (`~/.crush/capsules`). It ensures that executed software is tracked, versioned, and verified.

## Commands

### `install`
Installs a capsule from a local directory or archive.
```bash
crush pacman install ./my_capsule
```

### `remove`
Removes an installed capsule.
```bash
crush pacman remove my_capsule
```

### `list`
Lists all installed capsules.
```bash
crush pacman list
```

### `run`
Runs an installed capsule.
```bash
crush pacman run my_capsule
```

### `info`
Displays detailed information about a capsule.
```bash
crush pacman info my_capsule
```
