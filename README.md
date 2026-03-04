# mental-models

A repository for storing [draw.io](https://www.drawio.com/) diagrams used for learning and designing across multiple projects.

## Structure

```
mental-models/
├── learning/   # Diagrams used to study and understand concepts
└── design/     # Architecture and design diagrams for projects
```

## Usage

1. Open any `.drawio` file directly in [draw.io](https://www.drawio.com/) (desktop or web).
2. The [draw.io VS Code extension](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio) can be used to edit diagrams directly in the editor.
3. Place new diagrams in the appropriate folder based on their purpose.

## File Format

All diagrams are stored as `.drawio` (XML) files. They are treated as binary by Git (see `.gitattributes`) to avoid merge conflicts, but can be inspected as plain-text XML when needed.
