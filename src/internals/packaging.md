# CRUSH Package Manager

CRUSH Package Manager is a tool for installing, managing, and creating packages for CRUSH, the universal polyglot language and code converter. The package manager allows you to extend CRUSH with new language walkers, code snippets, and libraries.

## Installation

The CRUSH Package Manager is included with CRUSH. If you have installed CRUSH, you already have the package manager.

To install the package manager dependencies:

```bash
pip install crush[pkg]
```

## Usage

CRUSH Package Manager is accessed through the `crush pkg` command-line interface.

### Basic Commands

Here are the most common commands:

```bash
# Install a package
crush pkg install my-package

# Uninstall a package
crush pkg uninstall my-package

# Update a package
crush pkg update my-package

# Update all packages
crush pkg update --all

# Search for packages
crush pkg search "walker"

# List installed packages
crush pkg list

# Get information about a package
crush pkg info my-package
```

### Repository Management

The package manager can work with multiple repositories:

```bash
# List configured repositories
crush pkg list --repositories

# Add a remote repository
crush pkg repo add custom-repo https://example.com/packages

# Add a local repository
crush pkg repo add local-repo /path/to/repo --type local

# Add a GitHub repository
crush pkg repo add github-repo https://github.com/username/repo --type github

# Remove a repository
crush pkg repo remove custom-repo
```

### Creating Packages

You can create your own CRUSH packages:

```bash
# Create a new package
crush pkg create my-package

# Create a specific type of package
crush pkg create my-walker --type walker

# Create with author information
crush pkg create my-package --author-name "Your Name" --author-email "email@example.com"

# Publish a package to a repository
crush pkg publish ./my-package --repository local-repo
```

## Package Types

CRUSH supports several types of packages:

- **Walker**: Language converters that can translate between languages
- **Library**: Reusable code libraries for CRUSH
- **Snippets**: Collection of code snippets for various languages
- **Template**: Project templates for starting new projects
- **Mixed**: Combination of multiple package types

## Package Structure

A typical CRUSH package has the following structure:

```
my-package/
├── crush_package.json       # Package metadata
├── walkers/                 # Language walkers (optional)
│   └── my-package/          
│       ├── __init__.py
│       └── my-package_walker.py
├── lib/                     # Library code (optional)
│   └── my-package.crush
├── snippets/                # Code snippets (optional)
│   └── example.crush
├── templates/               # Project templates (optional)
│   └── project.crush
└── docs/                    # Documentation (recommended)
    └── README.md
```

The `crush_package.json` file contains the package metadata:

```json
{
  "name": "my-package",
  "version": "0.1.0",
  "description": "A CRUSH package",
  "package_type": "mixed",
  "authors": [
    {
      "name": "Your Name",
      "email": "your.email@example.com"
    }
  ],
  "license": "MIT",
  "homepage": "https://example.com/my-package",
  "repository": "https://github.com/username/my-package",
  "dependencies": [
    {
      "name": "another-package",
      "version": "1.0.0",
      "type": "package"
    }
  ],
  "languages": ["python", "c"],
  "keywords": ["example", "package"],
  "created_at": "2023-07-01T12:00:00.000000",
  "updated_at": "2023-07-01T12:00:00.000000"
}
```

## Creating a Language Walker Package

To create a language walker that adds support for a new programming language:

```bash
crush pkg create my-language --type walker
```

This creates a template for a language walker. You'll need to implement two key functions:

1. `from_source`: Convert source code to CRUSH AST
2. `to_my_language`: Convert CRUSH AST to your language

Edit the generated files in the `walkers` directory to implement these functions.

## Contributing

Contributions to the CRUSH Package Manager are welcome! If you find a bug or have a feature request, please open an issue on GitHub.

## License

The CRUSH Package Manager is released under the MIT License.