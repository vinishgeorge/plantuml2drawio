# Installation and Usage

This document describes how to install and use the PlantUML to Draw.io converter.

## Installation

### Prerequisites

- Python 3.6 or higher
- pip (Python package manager)

### Installation from GitHub

1. Clone the repository:
   ```bash
   git clone https://github.com/[username]/plantuml2drawio.git
   cd plantuml2drawio
   ```

2. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Install as a Python package (optional)

Alternatively, install the package in development mode:

```bash
pip install -e .
```

Once the package is available on PyPI:

```bash
pip install plantuml2drawio
```

## Usage

The converter can be used from the command line or via the graphical user interface.

### Command Line

#### Basic usage

Using the entry point scripts:
```bash
./p2d-cli --input <input_file.puml> --output <output_file.drawio>
```

With the installed package:
```bash
p2d-cli --input <input_file.puml> --output <output_file.drawio>
```

Example:
```bash
./p2d-cli --input examples/activity_examples/simple_activity.puml --output output.drawio
```

#### Show only the diagram type

```bash
./p2d-cli --input <input_file.puml> --info
```

Example:
```bash
./p2d-cli --input examples/activity_examples/simple_activity.puml --info
```

#### Show help

```bash
./p2d-cli --help
```

### Graphical User Interface

Start the GUI with:

Using the entry point scripts:
```bash
./p2d-gui
```

With the installed package:
```bash
p2d-gui
```

#### Using the GUI

1. **Enter PlantUML code**
   - Type PlantUML code directly into the text field, or
   - Load a PlantUML file via "Open File"

2. **Start conversion**
   - Click "Convert"
   - The detected diagram type is displayed
   - On success, the Draw.io XML is generated

3. **Save the result**
   - Click "Save" or "Save As"
   - Choose a filename ending with .drawio

## Supported diagram types

The following PlantUML diagram types are currently supported:

| Diagram type        | Support level |
|---------------------|---------------|
| Activity diagram    | ✓ Fully supported |
| Sequence diagram    | ✗ Planned |
| Class diagram       | ✗ Planned |
| Component diagram   | ✗ Planned |
| State diagram       | ✗ Planned |
| ER diagram          | ✗ Planned |

## Examples

### Activity diagram

**PlantUML input**:
```
@startuml
start
:Step 1;
if (Condition?) then (yes)
  :Step 2a;
else (no)
  :Step 2b;
endif
:Step 3;
stop
@enduml
```

**Result**: A Draw.io-compatible activity diagram with the corresponding elements.

## Error handling

### Common errors

1. **Invalid PlantUML code**:
   - Error message: "Invalid PlantUML code"
   - Solution: Check the syntax and ensure the code starts with @startuml and ends with @enduml.

2. **Unsupported diagram type**:
   - Error message: "Unsupported diagram type"
   - Solution: Use one of the supported diagram types or wait for a future version.

3. **File not found**:
   - Error message: "File not found"
   - Solution: Verify the path to the input file.

### Logs

For troubleshooting, enable detailed logs:

```bash
./p2d-cli --input <input_file.puml> --output <output_file.drawio> --debug
```

## Tips and tricks

1. **Complex activity diagrams**:
   - Split complex diagrams into smaller parts
   - Use clear identifiers for activities and decisions

2. **Compatibility with Draw.io**:
   - Generated .drawio files can be opened in all Draw.io-compatible tools
   - This includes the online version, desktop application, and the VS Code extension

3. **Workflow integration**:
   - Integrate the conversion into CI/CD pipelines
   - Example: a Git hook script to automatically convert on commit

## Support

If you have questions or issues:

1. Check the FAQ in the [Wiki](https://github.com/[username]/plantuml2drawio/wiki)
2. Open a [GitHub Issue](https://github.com/[username]/plantuml2drawio/issues)
3. Contact the developer: [email@example.com]
