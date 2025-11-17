# Module Descriptions

This section provides detailed information about each module of the PlantUML to Draw.io converter.

## src/plantuml2drawio/core.py - Core module

The core module is responsible for:

- Processing command-line arguments
- Detecting the PlantUML diagram type
- Coordinating the conversion process
- Selecting the appropriate processor for the detected diagram type
- Producing output in the desired format

### Key functions

- `determine_plantuml_diagram_type(content)`: Detects the type of a PlantUML diagram
- `process_file(input_file, output_file, info_only)`: Drives the conversion process
- `main()`: Entry point for command-line handling

### Constants

| Constant | Description |
|-----------|--------------|
| `OUTPUT_FORMAT_JSON` | Label for JSON output format |
| `OUTPUT_FORMAT_XML` | Label for XML output format |
| `DEFAULT_JSON_EXT` | Default extension for JSON output |
| `DEFAULT_DRAWIO_EXT` | Default extension for Draw.io output |
| `DIAGRAM_TYPE_ACTIVITY` | Label for activity diagrams |
| `DIAGRAM_TYPE_NOT_PLANTUML` | Label for invalid PlantUML content |

### Imported modules

- `modules.activity_processor`: Functions for processing activity diagrams
- Standard libraries: `sys`, `argparse`, `os`, `re`, `typing`

## modules/activity_processor.py - Activity diagram processing

This module specializes in processing PlantUML activity diagrams and contains all required functions.

### Classes

| Class | Description |
|--------|--------------|
| `Node` | Represents a diagram node with properties like ID, label, shape, position, and size |
| `Edge` | Represents an edge between two nodes with properties like ID, source, target, and label |

### Key functions

| Function | Description |
|----------|--------------|
| `is_valid_activity_diagram(plantuml_content)` | Checks whether a valid PlantUML activity diagram is present |
| `parse_activity_diagram(plantuml_content)` | Analyzes the PlantUML activity diagram and creates node and edge lists |
| `layout_activity_diagram(nodes, edges, ...)` | Calculates an optimal layout for the diagram |
| `create_activity_drawio_xml(nodes, edges)` | Generates Draw.io XML from nodes and edges |
| `create_json(nodes, edges)` | Generates a JSON representation from nodes and edges |

### Imported modules

- Standard libraries: `re`, `xml.etree.ElementTree`, `sys`, `collections.defaultdict`, `json`

## src/plantuml2drawio/app.py - Graphical User Interface

The GUI component provides:

- A user-friendly interface for conversion
- Functions to load and save files
- Display of the detected diagram type
- Visualization of the conversion process

### Main classes

- `FileSelectorApp`: Main application class
- `PlantUMLEditor`: Editor for PlantUML code
- `StatusBar`: Status bar for messages

### Key methods of FileSelectorApp

| Method | Description |
|---------|--------------|
| `__init__(self, root)` | Initializes the GUI and its components |
| `create_menubar(self)` | Builds the menu bar |
| `show_about(self)` | Displays application information |
| `open_file(self)` | Opens a PlantUML file via a file dialog |
| `update_text_and_button_state(self)` | Updates button state based on content |
| `apply_syntax_highlighting(self)` | Applies syntax highlighting to PlantUML code |
| `convert_to_drawio(self)` | Converts the current PlantUML code to Draw.io format |

### Imported modules

- `modules.activity_processor`: Functions for processing activity diagrams
- `customtkinter`: Extended Tkinter for modern GUI elements
- Standard libraries: `os`, `sys`, `tkinter`, `traceback`

## src/processors/base_processor.py - Base class for processors

This base class defines the interface for all diagram processors:

- Abstract methods for handling different diagram types
- Shared functionality for all processors
- Base classes for diagram elements (nodes, edges)

## src/processors/activity_processor.py - Activity diagram processor

Specialized module for processing activity diagrams:

- Parse PlantUML activity diagrams
- Extract nodes and edges
- Calculate layouts
- Generate Draw.io XML

### Key functions

- `is_valid_activity_diagram(content)`: Validates an activity diagram
- `parse_activity_diagram(content)`: Extracts nodes and edges
- `layout_activity_diagram(nodes, edges)`: Calculates the layout
- `create_activity_drawio_xml(nodes, edges)`: Generates Draw.io XML

## Module interactions

The typical conversion flow:

1. **Input**:
   - `core.py` is called with input and output parameters
   - `app.py` displays the user interface

2. **Processing**:
   - `core.py` detects the diagram type
   - The appropriate processor is selected
   - The processor parses the diagram and calculates the layout
   - The processor generates the Draw.io XML

3. **Output**:
   - `core.py` or `app.py` saves the result

## Extending with new diagram types

To support a new diagram type:

1. Create a new processor in `src/processors/` that inherits from `BaseDiagramProcessor`.
2. Implement the abstract methods for the new diagram type.
3. Update `core.py` to use the new module for the corresponding diagram type.

Thanks to the modular architecture, no major changes to existing code are required.
