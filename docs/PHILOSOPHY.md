# MukiDoc Philosophy

**Situation and problem.** In traditional software development, much important knowledge does not really live in the project; it is scattered across people's heads, code, meetings and ad hoc conversations. Requirements, design, system structure and concrete implementation also blur together easily: an idea quickly turns into code, and an implementation choice gradually ends up defining the system itself. The larger the project, the more understanding the project becomes understanding the code, and the more modifying the system depends on a developer's memory of countless details.

AI changes this relationship. Once code can be generated, modified and refactored quickly, the work that is truly scarce for humans moves upward. More important than personally completing every implementation detail is understanding the problem, forming a design, building structure, making trade-offs, and judging whether the final result really matches the original intent.

**Needs and ideas.** We therefore want a method built from the start for humans and AI to develop together. Humans no longer control a project mainly by operating on code directly, but express intent, design and judgment through more stable documents; the AI keeps refining from this context and completes the implementation, while maintaining consistency between code and documents.

The documents here are not manuals written after development is done; they are part of the development process itself. They serve humans in understanding and thinking about the project, and serve the AI in obtaining sufficiently complete and stable context.

**The essence of the need.** The real problem is not how to make AI better at writing code, but how to make a software project's important knowledge not depend on one person, one conversation or one version of the code.

A complete software project needs to know not only "what the code looks like now," but also to retain what it is, why it exists, why it is designed this way, how it is organized internally, how it is currently implemented, what important decisions were made, what changes it went through, and whether the final result is actually effective. Only when this context is continuously externalized can a new developer or a new AI re-enter the project without excavating code and chat logs from scratch.

At the same time, this knowledge must not be collapsed into one layer. What we want, how the system works internally, and how it is concretely implemented now are essentially three different questions. Mixing them makes upper-level design bind to lower-level technology too early, and makes every change ripple through the whole chain.

**Core approach.** This method is first of all a software engineering method designed for human-AI collaboration. Humans are mainly responsible for understanding the problem, forming intent, building abstractions and making judgments; the AI is mainly responsible for continuing to refine those decisions, completing the implementation, and keeping the project state consistent during development. Documents sit between the two, serving as shared context and the main collaboration interface.

It also tries to keep the key context software engineering needs in the project itself, rather than relying on external memory. A project should be able to explain, through its own documents, its goals, ideas, overall structure, design, implementation state, evolution and actual results. That way the code can change, the AI can be replaced, and conversations can end, yet the project's core understanding persists.

In concrete design, the core is three continuous but mutually decoupled layers: Design, System Design and Implementation.

Design describes what the created thing itself should be like. It concerns its functions, rules, behavior and domain properties, without presupposing how it must be implemented internally.

System Design describes how the internal system should be organized and run to realize that design. It turns the external design into system structure, state, relationships and operating mechanisms, while still leaving freedom over the concrete technical approach.

Implementation then lands the system design in the current concrete engineering environment, deciding which technologies and implementation approaches are actually adopted.

The three layers form a relationship of successive refinement: the upper layer defines what must hold, and the lower layer decides how to make it hold. The same Design can have different System Designs, and the same System Design can have different Implementations. A lower-level design is also an implementation of a higher-level design.

This layering is not meant to draw an absolute boundary between "design" and "implementation," but to decouple decisions at different levels of abstraction, so that a project can freely evolve the system structure and concrete implementation underneath while keeping the upper-level intent stable.

**How it operates.** When a new requirement appears, the human first clarifies what they really want, then works with the AI to refine it layer by layer into a system design and an implementation plan; once the information is clear enough, the AI completes the code and updates the affected documents in sync, and the human mainly checks whether the documents still accurately express the project. Running the system and Evaluation produce new facts; if the results fall short of expectations, we judge whether the problem belongs to the design, the system design or the concrete implementation, fix the corresponding layer, and let the AI continue to synchronize downward, forming a continuous iterative development loop.

**Why it works.** This approach splits a complex problem that would otherwise have to be held all at once across different levels of abstraction. Humans can focus on the judgments that currently matter, and as the design becomes clearer layer by layer, the space the AI must guess in shrinks. Meanwhile the complete context is kept inside the project, so that a new AI or developer can rebuild understanding without depending on anyone's memory. Humans can thus devote more energy to intent, structure and trade-offs, leave the large volume of elaboration, implementation, synchronization and repetitive engineering to the AI, and still keep control of the project.

**Principles and approach.**

1. The important context of software engineering should live in the project itself as much as possible, rather than depend on human memory, ad hoc conversation or one version of the code.
2. Design, System Design and Implementation should keep clear levels of abstraction and decoupling: the upper layer defines semantics, and the lower layer decides how to implement.
3. Documents are the main collaboration interface between humans and AI and the project's long-lived shared state; code is the concrete implementation of those designs under current conditions.
4. Humans are mainly responsible for problems, intent, judgment and trade-offs; the AI is mainly responsible for refinement, implementation, synchronization and execution.
5. Documents and code should evolve together. When development changes the system, it should also change the knowledge describing the system.
6. Implementation is not the end point. New facts produced by actual operation and Evaluation should keep flowing back to the right design layer and drive the next iteration.

In the end, this method hopes to keep a project's intent, structure and knowledge always in human hands, while letting the AI take on more and more of the work between a clear design and its concrete implementation.
