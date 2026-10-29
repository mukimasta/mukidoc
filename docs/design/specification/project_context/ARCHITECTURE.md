# ARCHITECTURE Design

ARCHITECTURE helps a person or AI encountering the project for the first time quickly build the skeleton of the whole system: what the main parts are, how they relate, how they unfold layer by layer inside, and how the system actually runs.

ARCHITECTURE is diagram-led; text only adds the responsibilities, boundaries and important relationships that the diagrams cannot show. The reading order goes from coarse to fine, progressively zooming into the same system.

The structure of the whole text is:

**Overall architecture → Layer-by-layer refinement → Runtime → Architecture tree → File structure**

### Overall architecture

Start at the highest level by drawing the system boundary, the main actors, external objects and the most central module relationships.

This level only needs to let the reader answer:

1. Who uses or affects the system.
2. Roughly what the system itself is made of.
3. How the system relates to the outside world.

A single Mermaid block diagram is enough. Nodes use complete, directly understandable names, not single letters, abbreviations or code names that only the author knows.

### Layer-by-layer refinement

After the overall architecture, keep zooming into the same system for 2–3 more levels.

Each level adds only the detail hidden by the previous one; it can expand the whole diagram or just one important module. The new diagrams should feel like continuously zooming in, not like re-describing the project with a different classification.

Each group usually contains:

1. A short sentence stating what this level is expanding.
2. A Mermaid architecture diagram.
3. Where needed, a short passage on important relationships the diagram cannot express directly.

If the diagram already explains things, do not repeat them in text.

### Runtime

Once the static structure is established, observe the system again from the runtime perspective.

Runtime picks the most typical complete run and shows the interaction order among the main actors. Prefer a Mermaid Sequence Diagram, kept as simple as possible while retaining the core information.

Runtime describes only the steps needed to understand how the whole runs, without expanding on specific algorithms, interface calls, state machines or implementation detail.

### Architecture tree

The architecture tree organizes the whole architecture completely from a hierarchical perspective, supplementing module responsibilities, containment relationships and boundaries that are hard to express in the diagrams.

Each entry corresponds to a real architecture node; the tree is not used to list design principles or ideas. Connections already visible directly in the diagrams are not repeated.

The architecture tree always uses a multi-level ordered list:

* Use ordered lists throughout.
* Use multiple levels where possible, with clear hierarchy.
* Indent each level by a fixed 4 spaces, with no blank lines between entries.
* Use short, direct language.

### File structure

The file structure goes at the very end as the finest-grained static view.

Use a text directory tree to show the main files and directories, so the reader can map the logical architecture built so far onto the real project. Show only the levels needed to understand the project structure, without expanding unrelated code files and engineering detail.

The overall reading experience of ARCHITECTURE should be: first see the system, then gradually see it clearly, then understand how it runs, and finally know where these structures actually land.
