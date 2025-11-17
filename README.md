# PlantUML to Draw.io Converter

A tool for converting PlantUML diagrams to Draw.io format.

*[German version below](#german-version)*

<p align="center">
  <img src="https://via.placeholder.com/700x200?text=PlantUML+to+Draw.io+Converter" alt="PlantUML to Draw.io Converter Logo"/>
</p>

## 📋 Overview

This project enables the conversion of PlantUML diagrams to Draw.io format, allowing for seamless integration of UML diagrams into various documentation and presentation workflows. The converter currently supports activity diagrams and is continuously being expanded to support additional diagram types.

## ✨ Key Features

- 🔄 Conversion of PlantUML activity diagrams to Draw.io format
- 🔍 Automatic detection of PlantUML diagram type
- 🖥️ User-friendly GUI and command-line interface
- 📐 Automatic layout calculation for optimal diagram display
- 🧩 Modular design for easy extensibility

## 🚀 Quick Start

### Installation

```bash
# Clone repository
git clone https://github.com/doubleSlash-net/plantuml2drawio.git
cd plantuml2drawio

# Install dependencies
pip install -r requirements.txt

# Or install in development mode
pip install -e .
```

### Usage

#### Command Line

```bash
# Using the entry point scripts
./p2d-cli --input examples/activity_examples/simple_activity.puml --output output.drawio

# Or using Python modules
python -m src.plantuml2drawio.core --input examples/activity_examples/simple_activity.puml --output output.drawio
```

#### Graphical User Interface

```bash
# Using the entry point scripts
./p2d-gui

# Or using Python modules
python -m src.plantuml2drawio.app
```

## 📦 Project Structure

The project has been reorganized for better maintainability and extensibility:

```
plantuml2drawio/
├── README.md                    # This file
├── LICENSE                      # License information
├── requirements.txt             # Python dependencies
├── setup.py                     # Setup script for installation
├── plantuml2drawio-cli          # Command-line entry point
├── plantuml2drawio-gui          # GUI entry point
├── src/                         # Main source code
│   ├── plantuml2drawio/         # Core package
│   │   ├── core.py              # Core functionality
│   │   ├── app.py               # GUI application
│   │   └── config.py            # Configuration settings
│   └── processors/              # Diagram processors
│       ├── base_processor.py    # Base class for processors
│       └── activity_processor.py # Activity diagram processor
├── tests/                       # Tests
├── docs/                        # Documentation
├── examples/                    # Example diagrams
└── resources/                   # Resources like icons
```

## 📚 Documentation

Detailed documentation is available in the `docs` directory:

- [Installation and Usage](docs/Installation_und_Benutzung.md)
- [Workflow](docs/Arbeitsablauf.md)
- [System Architecture](docs/Systemarchitektur.md)
- [Extension Possibilities](docs/Erweiterungen.md)

## 🧪 Examples

The project contains examples in the `examples` directory:

### Activity Diagram

**PlantUML Input**:
```plantuml
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

**Draw.io Output**:

<p align="center">
  <img src="https://via.placeholder.com/500x300?text=Draw.io+Activity+Diagram" alt="Draw.io Activity Diagram Example"/>
</p>

## 🛠️ Technology Stack

- Python 3.6+
- customtkinter for GUI
- Regular expressions for parsing
- XML libraries for Draw.io generation

## 📦 Executables

The project provides pre-built executables for both Windows and macOS through GitHub Actions. These executables are automatically built when:
- A new version tag is pushed (e.g., `v1.0.0`)
- The workflow is manually triggered via GitHub Actions UI

### Download Executables

1. Go to the [Releases](https://github.com/doubleSlashde/plantuml2drawio/releases) page to download the latest release
2. Or download the latest build artifacts from the [Actions](https://github.com/doubleSlashde/plantuml2drawio/actions) page:
   - `p2d-windows` - Windows executable with all dependencies
   - `p2d-macos` - macOS application bundle (.app)

### Building Executables Locally

You can build the executables locally using PyInstaller. You only need the runtime dependencies and PyInstaller:

```bash
# Install build requirements (includes runtime dependencies)
pip install -r requirements-build.txt

# Build executable
python -m PyInstaller --clean p2d.spec
```

The built executables will be available in the `dist` directory:
- Windows: `dist/p2d/p2d.exe` (with dependencies)
- macOS: `dist/p2d.app` (application bundle)

Note: The final executable will include all necessary runtime dependencies, so end users don't need to install Python or any requirements.

## 🗺️ Roadmap

- [x] Support for activity diagrams
- [ ] Support for usecase diagrams
- [ ] Support for sequence diagrams
- [ ] Support for class diagrams
- [ ] Support for component diagrams
- [ ] Advanced layout management
- [ ] Integration with PlantUML server
- [ ] Web interface

## 🤝 Contributing

Contributions are welcome! Check out the [Extension Possibilities](docs/Erweiterungen.md) to learn more about possible contributions.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

- [PlantUML](https://plantuml.com/) for the excellent UML diagram syntax
- [Draw.io](https://www.draw.io/) for the open XML format and diagram editing functionality

---

<p align="center">
  Created with ❤️ for UML enthusiasts and software developers
</p>

---

<a name="german-version"></a>
# German Version (English translation)

## 📋 Overview

This translated section mirrors the information above for readers who expected German content. The converter turns PlantUML diagrams into the Draw.io format so they can be integrated into documentation and presentation workflows. It currently supports activity diagrams and is being expanded to additional diagram types.

## ✨ Key Features

- 🔄 Conversion of PlantUML activity diagrams to the Draw.io format
- 🔍 Automatic detection of the PlantUML diagram type
- 🖥️ User-friendly GUI and command-line interface
- 📐 Automatic layout calculation for optimal diagram display
- 🧩 Modular structure for easy extensibility

## 🚀 Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/doubleSlash-net/plantuml2drawio.git
cd plantuml2drawio

# Install dependencies
pip install -r requirements.txt

# Or install in development mode
pip install -e .
```

### Usage

#### Command Line

```bash
# Using the entry point scripts
./p2d-cli --input examples/activity_examples/simple_activity.puml --output output.drawio

# Or using Python modules
python -m src.plantuml2drawio.core --input examples/activity_examples/simple_activity.puml --output output.drawio
```

#### Graphical User Interface

```bash
# Using the entry point scripts
./p2d-gui

# Or using Python modules
python -m src.plantuml2drawio.app
```
