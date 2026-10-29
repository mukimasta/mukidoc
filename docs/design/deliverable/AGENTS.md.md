# AGENTS.md Design

AGENTS.md is MukiDoc's project-level working protocol for AI Agents. It sits in the repository root and is maintained by MukiDoc.

It "compiles" the Design and rules scattered across MukiDoc into one high-density context suited to long-term loading by an Agent. Compilation keeps the information that affects how an Agent understands, judges and acts, and omits derivations, explanations, examples and other human-facing elaboration that do not.

AGENTS.md must be usable on its own. Other projects that adopt MukiDoc may receive only this one protocol, with no access to MukiDoc's own specification documents; the protocol should therefore contain what is needed to establish, maintain and evaluate the whole documentation system, while the project's concrete goals, design and facts are kept in that project's own documents.

Compilation aims at semantic coverage and sets no line limit. For each type of document, its responsibility, content scope, fixed structure, necessary length and format constraints, creation and update conditions, and easily confused boundaries should all be kept. What is omitted is repetition, discussion history and elaboration that do not affect understanding or behavior; a rationale or example that is needed for an independent judgment should also be kept. When checking the result, compare it item by item against the source specification and ask whether an Agent that has not read the source would produce results that deviate from the design for lack of information.

The protocol must clearly separate the fixed skeleton from on-demand content: the base directories and skeleton documents must exist even when empty, while Areas and optional documents are created on demand. A check must not overlook a missing fixed entry point on the grounds that "there is no content yet", nor invent body text to fill out the structure.

The delivered protocol carries an identifiable version, maintained separately from the version of the bootstrap Skill. Bootstrap can recognize an older version and ask whether to update; existing files are kept by default, and before a replacement is confirmed the actual differences are explained and the original is backed up. A same-version modification, a missing version marker and a higher version should not be lumped together as "outdated". A protocol update changes only the working rules; it does not mean the target project's knowledge has been migrated.

The protocol also states that documents are written in the language the project or Human uses.

AGENTS.md should place full trust in the Agent's understanding, reasoning and execution. It provides the project map, semantic boundaries and important constraints, but avoids prescribing fixed procedures, reading orders or specific methods. It constrains only what truly must not be broken and leaves the rest to the Agent's own judgment for the task at hand.

The text has five parts:

**Role → MukiDoc → Design → Develop → Evaluate**

### Role

Defines the basic relationship between Human and Agent, and the Agent's autonomy in the project.

The core is to make the Agent understand that:

* Human and Agent take part in the project together and maintain its knowledge together.
* Human cares more about requirements, direction, judgment and final intent.
* The Agent can proactively take part in analysis, design, implementation, investigation, testing, evaluation and documentation maintenance.
* The Agent should use its own abilities to solve problems rather than mechanically execute preset steps.
* When a requirement is clear enough, proceed autonomously; return to Human only questions that truly concern direction or intent, or that cannot reasonably be inferred.

This part first establishes trust and collaboration, not a permission list.

### MukiDoc

Lets the Agent quickly understand the knowledge system it works in.

This part should condense MukiDoc's overall architecture so the Agent knows what kind of knowledge Project Context, Design Chain, Information and Evaluation each hold, and which content represents current state versus history, evidence or auxiliary context.

It does not prescribe "read this, then that". The Agent decides how much context the task needs, and avoids loading the whole documentation directory indiscriminately for the sake of feeling safe.

It should also make the Agent understand the nature and authority of different kinds of knowledge, so that historical investigations, experiment results or raw materials are not mistaken for the current formal design.

### Design

Compiles all rules concerned with "forming and maintaining project knowledge".

It needs to include:

* The meaning and boundaries of the three layers Design, System Design and Implementation.
* The core responsibility of each kind of Project Context document.
* The purpose of each type of Information.
* General rules for editing, organizing and writing documents.
* The most important structural constraints of special documents such as PHILOSOPHY, ARCHITECTURE, ROADMAP, DECISION and DEVLOG.

It does not copy the full Document Design, but compresses into AGENTS.md the rules sufficient for the Agent to write documents correctly.

The Agent should be free to decide how a document unfolds, but must not break the abstraction levels, document responsibilities and structural constraints already defined.

### Develop

Defines the relationships the Agent must maintain when changing the actual project.

The focus is keeping design, project knowledge and actual implementation consistent, not prescribing development steps.

The Agent may choose its own implementation approach, debugging method, tools and task breakdown; the Implementation layer should leave wide engineering freedom. The closer to the project's upper-level intent, the more careful it must be, and it should not change Design just to make the code easier to write.

New knowledge produced during development should go to the most suitable place. Formal conclusions, investigation processes, experiment results, key decisions and project-level development history each have a different home and should not all be piled into one kind of document.

When code and the real system change meaningfully, documents that have become distorted as a result should be updated as well.

### Evaluate

Lets the Agent judge not only whether "the code runs" but whether the commitments of each layer actually hold.

The Agent should choose suitable verification methods for the task on its own.

Evaluation can come from PHILOSOPHY, Design, System Design and Implementation. The currently delivered AGENTS.md does not yet include the MukiCheck content and directory conventions that have not landed; they will be added once available. When an evaluation fails, analyze at which layer the problem really arises and fix the corresponding content, rather than patching locally just to make the check pass.

Evaluation itself likewise prescribes no uniform way of execution. Tests, scripts, benchmarks, Agent evaluation, human judgment or real-world usage feedback can all serve as evidence.

AGENTS.md should ultimately do two things: let a new Agent quickly understand the knowledge world and basic rules of the project, while imposing no unnecessary procedural constraints, so that a strong model can make full use of its own abilities to work autonomously.
