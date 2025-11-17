# System Overview

## Purpose and functionality

The PlantUML to Draw.io converter transforms PlantUML diagrams into the Draw.io format. This is particularly useful when users create diagrams in a text-based environment with PlantUML but later want to refine them in Draw.io to benefit from visual editing features.

## Architecture

The application is modular and follows separation of concerns. The key components are:

1. **Core module (core.py)**:
   - Main module that handles diagram type detection and orchestrates the conversion process
   - Provides a command-line interface for direct use
   - Implements the logic to detect different PlantUML diagram types

2. **Activity diagram module (modules/activity_processor.py)**:
   - Specialized module for processing PlantUML activity diagrams
   - Contains functions for validation, parsing, layout, and conversion of activity diagrams
   - Kept separate to enable extension to other diagram types

3. **User interface (app.py)**:
   - Graphical user interface (GUI) for the converter
   - Allows loading, editing, and converting PlantUML diagrams
   - Provides syntax highlighting for PlantUML code

## Operation

The conversion process goes through the following steps:

1. **Diagram type detection**: Analyze the input PlantUML file to determine the diagram type.
2. **Validation**: Check whether the diagram is valid and matches the supported format.
3. **Parsing**: Convert the PlantUML diagram into an internal representation of nodes and edges.
4. **Layout calculation**: Optimize positions and sizes of nodes to produce a clear diagram.
5. **XML/JSON generation**: Convert the internal representation into the Draw.io XML format or optionally JSON.
6. **Output**: Write the result to a file or display it in the GUI.

## Interfaces

- **Command-line interface (CLI)**: Enables control and automation of the conversion process.
- **Graphical user interface (GUI)**: Provides a user-friendly interface for interactive use.
- **Modular API**: Allows embedding conversion functions into other applications.

## Future and extensibility

The system was designed with extensibility in mind. It currently supports activity diagrams, but the modular structure simplifies adding more PlantUML diagram types such as:

- Sequence diagrams
- Class diagrams
- Component diagrams
- State diagrams
- ER diagrams

Each new diagram type can be implemented as a separate module without affecting existing code.
