# MUKICHECK Evaluation Design

MukiCheck is the project health check built into every MukiDoc project. It looks at whether the project's knowledge is correct, clear and self-consistent, whether it stays aligned with the real code, and whether these documents can ultimately help an unfamiliar Agent understand and continue the project.

MukiCheck evaluates whether, after adopting MukiDoc, the project's knowledge system is healthy. Whether the project's own product goals, user experience and business results succeed remains the responsibility of the project's own Evaluation.

MukiCheck has three layers:

**Static document check → Document–code joint check → Dynamic comprehension check**

The earlier layer examines the knowledge itself; the later layers bring in more real engineering and real use. Together the three decide whether MukiDoc can still carry the project's long-term context.

## Static document check

The static check reads only MukiDoc and judges whether the project knowledge currently stored is healthy in itself.

### Specification correctness

First check the constraints that can be stated clearly as rules, such as file structure, naming, length, heading levels, list format, and the fixed structure each type of document prescribes.

This layer answers the most basic question: do the documents exist as the MukiDoc specification requires? It should be as deterministic and objective as possible, and it clears away low-level errors before the semantic checks.

### Placement and layer correctness

Next check whether knowledge sits in the right place.

Even content that is entirely correct will damage the whole knowledge system if it is in the wrong document or at the wrong abstraction level. Design should not be tied to a concrete implementation, Implementation should not carry upper-level product design, and history, investigations, experiments and formal design should each keep their own nature.

This layer asks whether MukiDoc's knowledge classification still holds, and whether content has moved into a more natural place as it matured and changed.

### Internal consistency

Check whether all formal documents, taken together, still describe the same project.

Individual documents can each be correct while Architecture, Design Chain, Project Context and so on still contradict one another, leave gaps or drift apart. The same concept may gradually acquire different definitions, and historical state may get mixed with current state.

This layer ensures that what MukiDoc ultimately forms is one unified project knowledge system, not a set of Markdown files that are each valid on their own.

### Philosophy alignment

The highest layer of the static check returns to the project's own PHILOSOPHY.

PHILOSOPHY describes the project's core purpose, ideas and long-term basis for judgment. Even when later design is correctly formatted and mutually consistent, it may have drifted over long iteration from the problem the project originally set out to solve.

This layer checks whether the project direction expressed by the current documents still conforms to its own core Philosophy. It can only judge whether the current design matches the declared Philosophy; whether that Philosophy actually works in real use must still be verified by the project's own Evaluation.

## Document–code joint check

Once the static documents are healthy, MukiCheck brings in the real code. It checks whether the architecture, behavior, system mechanisms and implementation constraints described in the documents still actually exist in the codebase, and whether the important structures and mechanisms that have formed in the code have been settled back into the corresponding documents. It concerns two-way consistency: documents must not describe a system that no longer exists, and the code must not, after long evolution, quietly accumulate large amounts of project knowledge that exists only in the implementation.

## Dynamic comprehension check

The dynamic check uses a fresh Agent, usually a Subagent, with no chat history or implicit context, which relies only on the documents currently stored in the project to understand it anew, to verify whether MukiDoc really carries the project context. It focuses on whether this Agent can correctly understand the project goals, core Philosophy, overall architecture and main design; find the right place for knowledge; judge, given a new requirement, roughly which layers it affects; and, when the documents are insufficient, explicitly identify the uncertainty instead of making things up. What it ultimately answers is: if the current project is handed to a completely unfamiliar Agent, can it, relying on MukiDoc alone, correctly understand the project and have a basis to continue working?
