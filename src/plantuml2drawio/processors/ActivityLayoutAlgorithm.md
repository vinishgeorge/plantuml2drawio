# Algorithm for Positioning Elements in an Activity Diagram

The algorithm positions nodes of an activity diagram recursively and handles the following node types:

- **Start and end nodes**
- **Activity nodes** (always one incoming edge, exactly one outgoing edge)
- **Decision nodes** (two outgoing edges: "true" and "false")
- **Merge nodes** (two incoming edges)

All nodes are arranged vertically with equal spacing from top to bottom. For decisions, the false path is shifted by a fixed horizontal offset. When decisions appear on already shifted false paths, the additional offset is applied cumulatively, and all subsequent nodes—whether on the original vertical path or on a false path—inherit at least the maximum offset reached so far.

---

### Parameters

- **verticalSpacing:** Fixed vertical distance between nodes.
- **horizontalOffset:** Fixed horizontal shift added whenever the false path is taken.
- **currentOffset:** Local offset representing the cumulative shift along the current path.
- **globalOffset:** Maximum offset reached on any false path that also applies to the "true" (vertical) path so previously placed false paths remain aligned.

---

### Pseudocode

```pseudo
function layout(node, baseX, currentY, currentOffset, globalOffset):
    // Position the current node:
    // The x-value equals the base plus the greater of currentOffset or globalOffset
    node.x = baseX + max(currentOffset, globalOffset)
    node.y = currentY

    // Prepare the next vertical start point
    newY = currentY + verticalSpacing

    if node.type == 'Decision':
        // TRUE path: follows vertically without extra offset.
        if node.trueSuccessor exists:
            layout(node.trueSuccessor, baseX, newY, currentOffset, globalOffset)

        // FALSE path: increase currentOffset by the horizontalOffset.
        newFalseOffset = currentOffset + horizontalOffset
        // Update globalOffset to reflect the maximum reached offset.
        newGlobalOffset = max(globalOffset, newFalseOffset)
        if node.falseSuccessor exists:
            layout(node.falseSuccessor, baseX, newY, newFalseOffset, newGlobalOffset)

    else if node.type == 'Activity' or node.type == 'Start' or node.type == 'Merge':
        // These nodes have a single successor.
        if node.successor exists:
            layout(node.successor, baseX, newY, currentOffset, globalOffset)

    else if node.type == 'End':
        // End node: no successors
        return
```

---

### Behavior and considerations

1. **Start and vertical placement:**
   The layout begins with the start node. Each node is placed so its x-coordinate is `baseX + max(currentOffset, globalOffset)`. The y-value is always increased by the fixed `verticalSpacing`.

2. **Decision nodes:**
   - For the **true branch**, `currentOffset` remains unchanged and the path continues vertically.
   - For the **false branch**, `currentOffset` increases by `horizontalOffset`. This new offset becomes the basis for all nodes on that path.
   - `globalOffset` is updated so nodes that later return to the "true" (vertical) path inherit the maximum offset. This ensures previously shifted false paths stay aligned even if another decision occurs on the vertical path.

3. **Decisions on false paths:**
   The algorithm treats decisions on false paths the same way as on the vertical path:
   - The **false branch** again increases `currentOffset` by `horizontalOffset` and updates `globalOffset`.
   - This guarantees that nested decisions continue shifting to the right cumulatively.

4. **Merge nodes:**
   Merge nodes with two incoming edges may need their x-position calculated from both incoming x-values (for example, the maximum). The pseudocode assumes the passed offset is sufficient; a merging strategy can be added as needed.

---

### Example call

Initialize the algorithm with the start node, for example:

```pseudo
layout(startNode, 0, 0, 0, 0)
```

Here `baseX` is 0 and both `currentOffset` and `globalOffset` start at 0.

---

### Summary

- **Recursive layout:** Each node is positioned using vertical spacing and the current horizontal offset.
- **Decisions:**
  - The true path stays vertical, while the false path shifts right by a fixed offset.
  - The shift is cumulative so decisions on already false paths keep pushing subsequent nodes to the right.
- **globalOffset:** Ensures all nodes—even those returning to the vertical path—inherit at least the maximum offset reached, preserving layout consistency.

This description captures the required layout rules and behavior for nested decisions.
