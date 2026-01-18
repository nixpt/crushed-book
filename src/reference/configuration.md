# CRUSH Configuration System

The CRUSH configuration system allows users to customize various aspects of the CRUSH environment through a `config.json` file. This file stores settings for the CRUSH VM, interactive shell, language walkers, and more.

## Configuration File

By default, CRUSH looks for a configuration file at `~/.crush/config.json`. This file is automatically created with default values the first time CRUSH is run. You can also manually edit this file using any text editor.

## Configuration Categories

The configuration file contains settings organized into the following categories:

### General Settings

```json
"general": {
  "debug_mode": false,
  "color_output": true
}
```

- `debug_mode`: Enable additional debug output
- `color_output`: Use colored output in the terminal

### VM Settings

```json
"vm": {
  "stack_size_limit": 1000,
  "max_recursion_depth": 100,
  "call_timeout_ms": 10000,
  "memory_limit_mb": 256
}
```

- `stack_size_limit`: Maximum number of items allowed on the stack
- `max_recursion_depth`: Maximum depth of the call stack
- `call_timeout_ms`: Timeout for function calls in milliseconds
- `memory_limit_mb`: Memory limit for the VM in megabytes

### Interactive Shell Settings

```json
"interactive": {
  "history_size": 1000,
  "prompt_style": "default",
  "show_line_numbers": true,
  "auto_save_history": true,
  "tab_width": 4,
  "default_editor": ""
}
```

- `history_size`: Maximum number of commands to store in history
- `prompt_style`: Style of the interactive prompt
- `show_line_numbers`: Show line numbers when listing code
- `auto_save_history`: Automatically save command history on exit
- `tab_width`: Number of spaces for tabs
- `default_editor`: Editor to use when editing files (empty string uses system default)

### Language Walker Settings

```json
"walkers": {
  "python": {
    "indent_size": 4,
    "use_double_quotes": false
  },
  "c": {
    "indent_size": 4,
    "include_comments": true,
    "braces_style": "same_line"
  },
  "bash": {
    "indent_size": 2,
    "shebang": "#!/bin/bash"
  }
}
```

Each language walker can have its own configuration settings for controlling the generated code style.

### Capabilities Settings

```json
"capabilities": {
  "allowed": ["io.print", "io.input", "fs.read", "fs.write"],
  "default_sandbox_level": "medium"
}
```

- `allowed`: List of allowed capabilities
- `default_sandbox_level`: Default sandbox level for capabilities (options: "none", "low", "medium", "high")

### Package Manager Settings

```json
"packages": {
  "default_repository": "default",
  "auto_update_check": true,
  "install_dir": ""
}
```

- `default_repository`: Default repository to use
- `auto_update_check`: Check for package updates automatically
- `install_dir`: Directory for installed packages (empty string uses default location)

## Managing Configuration

### Using the Interactive Shell

The CRUSH interactive shell provides commands for viewing and modifying configuration settings:

- `config_list`: List all configuration values
- `config_get <key>`: Get a specific configuration value
- `config_set <key> <value>`: Set a configuration value
- `config_reset`: Reset all configuration to defaults

Examples:

```
CASMVM[idle:-][~]> config_get vm.stack_size_limit
vm.stack_size_limit = 1000 (int)

CASMVM[idle:-][~]> config_set vm.stack_size_limit 2000
Configuration updated: vm.stack_size_limit = 2000
Applied to current VM: stack_size_limit = 2000

CASMVM[idle:-][~]> config_list

=== CRUSH Configuration ===
version = 1.0.0

[capabilities]
  default_sandbox_level = medium

[general]
  color_output = True
  debug_mode = False

[interactive]
  auto_save_history = True
  default_editor = 
  history_size = 1000
  prompt_style = default
  show_line_numbers = True
  tab_width = 4

[packages]
  auto_update_check = True
  default_repository = default
  install_dir = 

[vm]
  call_timeout_ms = 10000
  max_recursion_depth = 100
  memory_limit_mb = 256
  stack_size_limit = 2000
```

### Using the API

You can also access and modify the configuration programmatically:

```python
from crush.core.config import get_config, set_config, reset_config

# Get a configuration value
stack_limit = get_config("vm.stack_size_limit")

# Set a configuration value
set_config("vm.stack_size_limit", 2000)

# Reset to defaults
reset_config()
```

## Custom Configuration Path

You can specify a custom configuration file path when initializing the configuration manager:

```python
from crush.core.config import ConfigManager

# Use a custom configuration file
config_manager = ConfigManager("/path/to/custom/config.json")
```

## Troubleshooting

If you encounter issues with your configuration:

1. Try resetting to defaults with `config_reset` in the interactive shell
2. Check permissions on the configuration file
3. Ensure the configuration file contains valid JSON

If problems persist, you can delete the configuration file and CRUSH will regenerate it with default values on the next run.