# Extension Possibilities

This document describes potential extensions and improvements for the PlantUML to Draw.io converter.

## Support for additional diagram types

The current version of the converter supports only activity diagrams. The modular architecture makes it straightforward to add further diagram types.

### Priorities for new diagram types

Based on popularity and complexity, the recommended implementation order is:

1. **Sequence diagrams**
   - Widely used
   - Clear, linear structure
   - Well-defined elements (participants, messages, activations)

2. **Class diagrams**
   - Fundamental for object-oriented modeling
   - Manageable number of element types
   - More demanding layout

3. **Component diagrams**
   - Medium complexity
   - Clear structure
   - Limited number of element types

4. **State diagrams**
   - Similarities to activity diagrams
   - Medium complexity

5. **ER diagrams**
   - Focused on data modeling
   - More complex relationships

### Implementation approach for new diagram types

Create a specialized module for each new diagram type:

```
modules/
  ├── activity_processor.py
  ├── sequence_processor.py
  ├── class_processor.py
  ├── component_processor.py
  └── ...
```

Each module should provide the following functions:

1. **Validation function**
   ```python
def is_valid_<type>_diagram(plantuml_content: str) -> bool:
    # Validate a <type> diagram
    # ...
```

2. **Parsing function**
   ```python
def parse_<type>_diagram(plantuml_content: str) -> Tuple[List[Node], List[Edge]]:
    # Analyze the PlantUML code
    # Build internal data structures
    # ...
```

3. **Layout function**
   ```python
def layout_<type>_diagram(nodes: List[Node], edges: List[Edge], **kwargs) -> None:
    # Calculate an optimal layout
    # ...
```

4. **XML generation function**
   ```python
def create_<type>_drawio_xml(nodes: List[Node], edges: List[Edge]) -> str:
    # Create XML in Draw.io format
    # ...
```

Then update the core module `src/plantuml2drawio/core.py` to import and use the new module for the appropriate diagram type.

## Improve the user interface

The GUI can be expanded in several areas:

### Real-time preview

A split view that shows the PlantUML code and a preview of the generated diagram:

```
+------------------------+-----------------------+
| PlantUML code          | Draw.io preview       |
|                        |                       |
| @startuml              |      +--------+       |
| start                  |      | Start  |       |
| :Step 1;               |      +--------+       |
| if (Condition?) t...   |          |            |
|                        |          v            |
|                        |      +--------+       |
|                        |      | Step 1 |       |
|                        |      +--------+       |
+------------------------+-----------------------+
```

### Enhanced syntax highlighting

Improve syntax highlighting with extra features:

- Auto-complete PlantUML keywords
- Highlight invalid code
- Automatic indentation
- Line numbers

### Diagram type selection

Dropdown to choose the diagram type once multiple types are supported:

```
+-------------------------+
| Diagram type:  [Activity v]
+-------------------------+
| [ ] Automatic detection
+-------------------------+
```

### Export options

Additional export choices:

- Different Draw.io styles
- Direct export as PNG/SVG/PDF
- Export sizes and scaling
- Color palettes

## Technical extensions

### Better layouts

- Optimized layout algorithms for complex diagrams
- Support for custom layout parameters
- Automatic resizing of elements based on text length

### Integration with external tools

- PlantUML server integration for previews
- Export to other diagram tools (beyond Draw.io)
- VCS integration (Git, SVN)

### Reverse conversion

Implement the reverse conversion from Draw.io to PlantUML:

```
Draw.io XML -> Internal representation -> PlantUML code
```

This would enable a complete round-trip workflow.

### Command-line extensions

- Batch processing of multiple files
- Configuration files for repeated conversions
- Integration into build processes

## Infrastructure improvements

### Automated tests

- Broaden test coverage
- Integration tests for the full conversion flow
- Property-based testing for robust validation

### Documentation

- Full API documentation
- User guide with examples
- Contribution guide for open-source developers

### Distribution

- Packages for different package managers (pip, conda)
- Standalone installers for various operating systems
- Docker container for containerized execution

## Implementation strategy

### Short-term priorities

1. Support for sequence diagrams
2. Improved error handling and user feedback
3. Optimize layout algorithms for activity diagrams

### Mid-term goals

1. Support for class and component diagrams
2. Implement the real-time preview
3. Enhanced syntax highlighting

### Long-term vision

1. Full support for all PlantUML diagram types
2. Reverse conversion (Draw.io to PlantUML)
3. Deeper integration with development environments

## Adding a new diagram type

To support a new diagram type, complete the following steps:

1. **Detect the diagram type**
   - Extend diagram type detection in `src/plantuml2drawio/core.py`
   - Add detection patterns specific to the new type

2. **Parsing and conversion**
   - Create a new processor in `src/processors/`
   - Implement the parsing logic for the new diagram type
   - Develop the conversion logic for Draw.io XML

3. **Implement the required functions:**
   - `is_valid_diagram(content)`: checks whether the content is a valid diagram of the new type
   - `parse_diagram(content)`: extracts nodes and edges from the PlantUML code
   - `layout_diagram(nodes, edges)`: calculates the layout for the new diagram type
   - `create_drawio_xml(nodes, edges)`: generates Draw.io XML for the new diagram type
   - `create_json(nodes, edges)`: creates a JSON representation of the diagram

4. **Update configuration:**
   - Add the new diagram type in `src/plantuml2drawio/config.py`:
     ```python
     AVAILABLE_PROCESSORS = {
         DIAGRAM_TYPE_ACTIVITY: "plantuml2drawio.processors.activity_processor.ActivityDiagramProcessor",
         DIAGRAM_TYPE_SEQUENCE: "plantuml2drawio.processors.sequence_processor.SequenceDiagramProcessor"
     }
     ```

5. **Test the new diagram type:**
   - Create test cases in `tests/`
   - Add examples in `examples/`
