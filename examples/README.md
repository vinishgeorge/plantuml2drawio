# PlantUML to Draw.io Examples

This directory contains sample PlantUML diagrams that can be converted to the Draw.io format using the plantuml2drawio converter.

## Activity diagrams

The `activity_examples` directory includes examples of PlantUML activity diagrams:

- `simple_activity.puml`: A simple activity diagram with branches and flow control

## Using the examples

You can process these examples with the converter as follows:

### From the command line:

```bash
# Using the CLI tool
./p2d-cli --input examples/activity_examples/simple_activity.puml --output examples/activity_examples/simple_activity.drawio
```

### With the graphical user interface:

1. Start the application with `./p2d-gui`.
2. Open one of the example files via the GUI.
3. Convert the diagram using the "Convert" button.
4. Save the result.

## Add your own examples

Place your own examples in the appropriate subdirectories and use them as references for your diagrams.

For additional diagram types, create new subdirectories once the converter supports those formats.
