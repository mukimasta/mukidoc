# MukiDoc Agent Protocol

<!-- MukiDoc protocol version: 0.1.0 -->

## Role

You develop and maintain this project together with the Human. The Human cares most about problems, requirements, intent, direction and trade-offs; you may take an active part in discussion, design, implementation, investigation, testing, evaluation and documentation upkeep. When a requirement is clear enough, proceed autonomously and use your own judgment about tools, reading scope and execution. Consult the Human when a change touches core intent, or when there is a disagreement that cannot be reasonably inferred and would affect the outcome.

The project uses MukiDoc to preserve long-term context. People mainly use documents to express intent, understand structure and check results; you refine the design, complete the implementation and maintain project knowledge on the basis of that context. The goals of the work include making it possible for a new Agent with no chat history to re-understand and continue the project, and for the Human to stay in control of the project's intent and structure without memorizing large amounts of code detail.

This file is a self-contained MukiDoc working protocol. It holds the rules needed to establish, maintain and evaluate a documentation system, and using it requires no access to any other specification of the MukiDoc method itself. The current project's goals, design, implementation and facts live in the project's own documents and engineering; they cannot be inferred from this protocol.

The protocol constrains what knowledge means and which relationships must be maintained. It does not prescribe a uniform reading order or a fixed development workflow. Gather enough context for the task, and avoid loading every document indiscriminately. Likewise, do not omit project knowledge that a future newcomer needs just because the current conversation already knows it.

## MukiDoc

### Core Idea

A project needs to preserve over the long term what it is, why it exists, what it hopes to achieve, how it works internally, how it is currently implemented, which key changes it has gone through, and whether the results are valid. This knowledge should live in the project itself and survive across developers, Agents, sessions and technical implementations.

The core design chain is `Design → System Design → Implementation`. Each upper layer defines the semantics and constraints that must hold, and the layer below decides how to make them hold. One Design can have different System Designs, and one System Design can have different Implementations. This lets people make judgments at a suitable level of abstraction, and lets lower layers evolve without changing the intent of the layers above.

Documents and engineering evolve together. Documents express design intent and project knowledge; actual code, tests and run results provide implementation evidence. When the two conflict, find out whether the implementation has drifted, the document is stale, or the design has not yet landed. Do not simply rewrite one side to match the other and so hide the problem.

### Project Map

The root `README.md` is for users and handles presentation, onboarding and navigation; the root `AGENTS.md` is the Agent working protocol. Formal project knowledge lives in `docs/`:

1. Project Context: `OVERVIEW.md`, `PHILOSOPHY.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `DECISION.md`, `DEVLOG.md`, `TODO.md`. They hold, respectively, the project definition, its philosophical foundation, overall structure, long-term evolution, the reasoning behind key judgments, development history and current actions.
2. Design Chain: `design/`, `system_design/`, `implementation/`. They hold, respectively, the object design, the internal system mechanisms and the current concrete engineering implementation.
3. Information: `information/`, holding raw materials, external information, investigation evidence and exploration. It sits alongside Project Context.
4. Evaluation: `evaluation/`, holding the goals, methods, criteria and judgments for the commitments the project itself makes.

The base directories and skeleton documents below must be created and kept. When initializing or migrating a project into MukiDoc, fill in the whole skeleton even if there is no content yet; it provides stable entry points to knowledge. Source code, tests, scripts and the like continue to use whatever engineering structure suits the project.

```text
/
├── README.md
├── AGENTS.md
└── docs/
    ├── OVERVIEW.md
    ├── PHILOSOPHY.md
    ├── ARCHITECTURE.md
    ├── ROADMAP.md
    ├── DECISION.md
    ├── DEVLOG.md
    ├── TODO.md
    ├── design/
    ├── system_design/
    ├── implementation/
    ├── information/
    │   ├── raw_materials/
    │   ├── external_information/
    │   ├── investigations/
    │   └── playground/
    └── evaluation/
        ├── philosophy/
        ├── design/
        ├── system_design/
        └── implementation/
```

The fixed skeleton is handled separately from on-demand content. The root README.md and AGENTS.md, the seven Project Context documents under docs, and every directory in the tree above must exist. A skeleton document that has no content yet may contain just its title; never invent facts, decisions or to-dos to fill a file, and remember that a file's existence does not mean its content is complete. Empty directories in a Git project are kept with `.gitkeep`, which is not a project knowledge document.

Areas within each layer, specific design documents, Evaluation Suites, and optional documents such as `DATA_MODEL.md`, `RUNTIME.md`, `TECH_STACK.md` and `API.md` are still created on demand. When checking structure, report and fill in any missing fixed skeleton; a missing optional item does not automatically count as a problem.

### Knowledge Nature and Current State

The current formal documents describe the project's intent, design and known state; designs not yet implemented must be told apart from the actual implementation state. A README summary must not become a separately maintained second design. ROADMAP expresses the long-term path and does not prove that a stage is complete; TODO expresses decided to-dos and does not prove a capability exists.

DECISION and DEVLOG preserve the judgments and facts of their time; do not treat historical records as the current state. Information holds grounds, evidence and immature knowledge, and the original requirements, old plans or experiment results in it do not automatically become the current design. An Evaluation conclusion must be supportable by the corresponding evidence and state its scope of validity; one local check passing cannot by itself prove that the overall goal holds.

When you find missing knowledge, contradictions or states that cannot be confirmed, distinguish fact, inference and open questions. Consult the relevant documents and engineering evidence, and clarify with the Human when necessary; do not fabricate design intent, historical reasons or verification results.

## Design

### Design Chain: Three Layer Boundaries

**Design: what the object itself should be.** It holds features and capabilities, what participants can do, core behavior and rules, interaction and experience, domain concepts and their relationships, the properties that must be preserved, and the trade-offs of the object design. It focuses on what is ultimately wanted, and does not decide in advance how the software is organized internally or which technology it uses. As long as the object itself has not changed, this layer should stay largely stable even if the system is reimplemented.

**System Design: how the internal system makes it hold.** It holds module responsibilities and boundaries, module collaboration, core state and its changes, logical data relationships, lifecycles, key runtime flows, and system mechanisms such as concurrency, synchronization and error recovery, along with cross-module constraints. This layer goes inside the software but tries not to bind itself to specific technology, so that important mechanisms survive across technical implementations.

**Implementation: how the current engineering concretely realizes it.** It holds languages, frameworks, runtime environments, databases, caches, messaging systems, API and protocol contracts, concrete data structures and storage, dependencies, threading and task scheduling, serialization, configuration, deployment, performance optimization and the engineering constraints of the moment. It keeps the knowledge needed to understand the implementation and continue development, and does not restate the code line by line.

To decide where something belongs, ask what changing it would mean:

1. If the object's behavior, rules or properties change, it belongs to Design.
2. If the object stays the same but the internal structure, state, data relationships or runtime mechanisms change, it belongs to System Design.
3. If the system mechanisms stay the same and only the engineering and technical approach changes, it belongs to Implementation.

Take login as an example. Credential login, login-state persistence and the permissions of different identities are Design. How authentication, sessions and authorization cooperate is System Design. The password algorithm, session storage, cookie configuration and the interface implementation are Implementation. Swapping the session storage should not force the upper layers to redefine login behavior.

A lower-level design can also be an implementation of a higher-level one, so do not chase a mechanical, absolute classification. The point of the judgment is that each document keeps a consistent level of abstraction, so that concrete implementation does not in turn bind the upper-layer semantics.

### Area: Organization Within a Layer

Use "fixed Layers, free Areas": vertically keep the three layers, and horizontally organize by the problem spaces the project naturally forms. An Area may correspond to a deliverable, a product capability, a domain or a system concern, with no preset taxonomy.

1. No mirroring required: if one layer has an Area, other layers need not create a directory of the same name; create the corresponding documents only where that layer actually produces knowledge.
2. Grow on demand: while an Area has a single document, keep it as a flat file; create a directory once multiple documents naturally form, and subdivide inside it by the same principle.
3. Cross-cutting content goes at the layer root: do not force knowledge that spans several Areas into one local Area. System-level logical data relationships can go in `system_design/DATA_MODEL.md`, runtime mechanisms in `system_design/RUNTIME.md`, technology choices in `implementation/TECH_STACK.md`, and interface contracts in `implementation/API.md`; all of these files are created on demand.

### General Writing and Maintenance

Documents serve understanding; aim for clarity, naturalness and high information density. Do not cut necessary context and reasoning for brevity, and do not add structure just to look formal. The special format of a specific document takes precedence over the general rules below.

1. Keep content within the responsibility and level of abstraction of the document it lives in, use direct, concrete language, and avoid filler, repeated explanation and pointless lead-ins. When there is no real contrast, do not use contrastive constructions such as "not X but Y".
2. Prefer natural paragraphs for continuous reasoning, causal relationships and explanation. Use headings or lists only when the information is genuinely parallel and reads more clearly item by item; where an ordered list works, prefer it, and do not force bullet points for the sake of tidiness. Use bold only for necessary visual anchors.
3. Apart from the document's main title, use level-3 headings when the body has only one level of headings; levels 2 and 3 when it has two; levels 2, 3 and 4 when it has three. Use them continuously according to the real structure, and do not create unnecessary multi-level headings.
4. Formal document file names are all uppercase, with multiple words joined by underscores; the fixed file names prescribed for various purposes stay consistent. Raw materials keep their original form.
5. Make each document as complete as possible within its own responsibility, and avoid frequent jumps between documents. Reference another document only when the content truly belongs there, or when maintaining duplicates would cause consistency problems. Place facts and rules in their natural authoritative location, and do not copy complete versions into several places.
6. When editing, integrate content into its natural place and remove stale descriptions of the current state; do not keep piling patches at the end of the file. Append-style history documents follow their own rules.
7. Describe real rules and states directly. Use examples only when the scenario itself is the needed information, or when an abstract statement cannot convey it accurately.
8. The fixed directories and skeleton documents must be kept; create other documents and Areas only when they have independent maintenance value, and do not pre-create optional empty files or Areas with no content. Once existing content matures it may be moved, split or merged, and the related descriptions and navigation should stay true as it does.
9. Write documents in the language the project or the Human already uses. That this protocol is written in English does not require the project's documents to be in English.

### README: The Entry Point for Users

The root `README.md` helps someone opening the repository for the first time learn what the project is, whether it is worth reading on, how to get started, and where to go next. It usually contains the project name and a one-line value statement, a short introduction, necessary screenshots or a demo, a brief Quick Start when the project is usable, the entry point to the formal documents, and whatever status, installation, usage, contribution and License information the project actually needs.

It may present and summarize, but it does not carry formal knowledge and does not expand on design, architecture, development history or methodology. The README targets first-time users; OVERVIEW targets people preparing to understand and develop the project. For an existing project, keep a README that is still valid, only adding missing information, tidying structure and adding documentation navigation as needed, and do not rewrite it just to unify the format.

### OVERVIEW: The Project's External Understanding

The fixed structure is "project definition → the problem → deliverables → user scenario → closing sentence", normally within 800 words.

The opening uses a short paragraph, without a subheading, to define directly what the project is, who it is for and what its core function is. Next, `**The problem.**` describes the real-world predicament, ideally in one paragraph, staying at the level of the problem without philosophical derivation; `**Deliverables.**` states what users ultimately get or use, in a short list if there are many, without going into internal implementation; `**User scenario.**` writes one continuous typical scenario with a starting point, a usage process and a result, ideally in one paragraph, or two scenarios if necessary, and avoids listing features again. The last sentence expresses, from the angle of the usage result, the ideal state the project hopes to bring about.

The whole text builds an accurate, complete external understanding and does not go into internal design, architecture or implementation. The result the project hopes to deliver and its current degree of availability must remain distinguishable.

### PHILOSOPHY: The Project's Topmost Why

Derive the philosophical foundation from the real situation, so that readers can use it to judge whether future proposals fit the project's direction. It is not responsible for the project's overall picture, features, modules, directories or technical implementation. The whole text stays under 2000 words and advances continuously in this structure:

1. Situation and problem: the real scenario or background and the problems that existed, ideally 1–2 paragraphs.
2. Needs and ideas: the needs that arise naturally from this and the things hoped to change, ideally 1–2 paragraphs.
3. The essence of the need: the problem that really needs solving behind the surface need, ideally 1–2 paragraphs.
4. Core approach: derive the thinking, methods and relationships from the essential problem. This is the main body, ideally 3–6 paragraphs, taking the most space and staying at the Philosophy level.
5. How it operates: use a typical scenario to show how the thinking actually plays out and how participants collaborate, exactly one paragraph.
6. Why it works: explain how the core approach solves the original problem, exactly one paragraph, introducing no new core concepts.
7. Principles and approach: summarize the derived thinking as an ordered list, adding no new design; ideally fewer than 8 items, nested if complex, with no more than 8 outer items. The last sentence closes the whole text.

Each part of the body uses a `**Subheading.**` followed directly by the text, with no multi-level Markdown headings. Except for the final principles, default to natural paragraphs. Each part should follow naturally from the previous one; if a core point cannot be derived from what precedes it, supply the missing reasoning. After concrete architecture and technology change, the main ideas should still hold.

### ARCHITECTURE: The Skeleton of the Whole System

Mainly diagrams, in a fixed order: "overall architecture → layer-by-layer refinement → Runtime → architecture tree → file structure". Text only supplements the responsibilities, boundaries and important relationships that the diagrams cannot show.

1. Overall architecture: use one Mermaid block diagram to show the system boundary, main participants, external objects and the relationships among core modules. Nodes use complete, directly understandable names, avoiding abbreviations or code names only the author knows.
2. Layer-by-layer refinement: keep zooming into the same system for 2–3 levels, expanding the whole or important modules. Each level adds only the details the previous level hid, and does not re-describe the system with a different classification. Each group is usually one sentence of introduction, one Mermaid diagram and any necessary supplementary text; do not repeat what the diagram already makes clear.
3. Runtime: show the most typical complete run, preferably with a Mermaid Sequence Diagram expressing the interaction order of the main participants. Keep only the steps needed to understand the overall run; specific algorithms, interface calls, state machines and implementation details go into the corresponding design chain documents.
4. Architecture tree: use a multi-level ordered list to lay out the real architecture nodes, responsibilities, containment relationships and boundaries completely, without listing design principles and without repeating connections the diagrams already make explicit. Indent each level by 4 spaces, leave no blank lines between items, and keep the language short and direct.
5. File structure: finally, use a text directory tree to map the logical architecture to the main files and directories, expanding only the levels necessary to understand the project and omitting irrelevant engineering details.

### ROADMAP: Long-Term Capability Evolution

It describes how the project gradually gains new capabilities and maturity, stays relatively static, and is modified only when the overall path changes. Current tasks belong to TODO and actual history belongs to DEVLOG.

Stages are divided by qualitative shifts in capability or maturity, not mechanically grouped by feature, component, deliverable, version name or quarter. Each stage explains its core problem, the new capability or state it brings once complete, and why it becomes the foundation of the next stage. With specific tasks and dates removed, the progression of capability should still be visible; if the stages could be freely swapped, it is usually just a task list.

The format is `# Roadmap`, an opening short paragraph summarizing the final state, then the stages as numbered level-2 headings of the form `## 1. Stage Name`, each with 1–3 natural paragraphs and no specific tasks or implementation. The last stage describes the complete target state. There are usually 4–8 stages; a complex project may use a two-level structure, and the whole text stays under 2000 words.

### DECISION: Key Judgments Worth Keeping

Use a single `DECISION.md` to keep the reasoning behind the few judgments that future people are likely to get wrong and that have no more natural home. The test is: if it is not recorded, will a future person follow intuition back to a default approach that was already abandoned? There should usually be a natural default answer, a reason for deviating that is hard to re-derive easily, and long-term impact; even if it is overturned later, the original reasoning is still worth keeping. Conclusions and arguments that can naturally be written into the design chain are better kept there, and not repeated in DECISION.

Ordinary either-or preferences are not recorded. The exception is a choice that other documents, paths, tools or interfaces already depend on; then record the constraint it carries and why it cannot be changed casually. Ordinary implementation choices, temporary adjustments, development running logs and plans that have not happened do not go into DECISION.

Append entries in chronological order as an ordered list, nested if complex. Each entry is generally under 200 words and centers on one complete judgment, writing the background, default answer, key thinking, final decision and any necessary impact and scope; the emphasis is on why the decision was reached, without expanding into concrete implementation. Write only the reasons that actually existed at the time; if the reason is weak or unclear, record it as it was and do not invent one after the fact.

When a decision is overturned, keep the original record and append a new decision explaining the new facts or judgment, and point to the old entries that were overturned or affected.

### DEVLOG: The Project's Development History

Record key capabilities and milestone results, problems that affected progress, important facts and limitations found during development or testing, plan adjustments triggered by real-world feedback, deep system problems, and Evaluation results that affect direction. Keep only the project's main line, and do not repeat ordinary changes, simple refactors, small fixes and mechanical processes that Git already expresses completely.

Append by date, in the format of an ordered list under `### YYYY-MM-DD`. Entries from the same day are merged under the same date, and each is usually 1–3 sentences: first what happened, then, as needed, the cause, finding or impact, so that someone who did not take part can understand its significance. At the end of development, record what truly deserves to enter history; not every operation needs to leave a record.

Detailed troubleshooting goes into Information, and local implementation knowledge into Implementation. DEVLOG is normally append-only and is not rewritten to match the current state; when a new understanding overturns an old one, record the change under a new date. It does not describe the current state, nor does it arrange to-dos or priorities; it may explain how a completed result changed or unlocked later stages, but it does not treat unexecuted plans as history.

### TODO: Current Actions

Keep only executable items that are already decided, in priority order, starting with a verb where possible. Do not add Now / Next groupings, and do not expand on background or design. Decided items that cannot move forward for now go under `Waiting`, with the waiting condition stated. When there are no decided tasks, keep TODO.md and its title; do not invent to-dos, and do not delete this fixed entry point.

The format is `- [ ] concrete action` under `# TODO`; when there are waiting items, add `### Waiting`, under which use `- [ ] concrete action — waiting condition`. Delete items directly once done and do not accumulate completion history; important results go into DEVLOG and long-term direction into ROADMAP.

### Information: Materials, Evidence and Exploration

Information holds valuable context outside the formal design. It is divided from Project Context by nature: the former holds grounds, the latter holds the project's own formal narrative; when a material was produced and whether it concerns the whole project do not decide where it belongs. The following four category directories are always created, even if temporarily empty; the specific materials in them arise as actually needed.

1. `raw_materials/`: the project's own original discussions, requirements, historical inputs and existing materials. In principle keep them in their original form and do not keep rewriting them to fit the current design, so that later readers can trace the original context.
2. `external_information/`: external materials, excerpts and research summaries, keeping sources where possible and distinguishing fact from inference. The project's own formal design conclusions do not stay here posing as the current design.
3. `investigations/`: investigations of real bugs, anomalies or performance problems that have already occurred, keeping the reproduction, the troubleshooting process, key findings, root cause and necessary conclusions, to avoid repeating the diagnosis. If the root cause cannot be confirmed, record that as it is.
4. `playground/`: active exploration of unknown problems, holding feasibility experiments, performance and algorithm validation, tool trials, loose thinking and immature drafts. Failure, temporary results and having no conclusion are all allowed, as are records that serve no conclusion for now; it need not follow the structure of other formal documents and does not carry the description of the current state.

An Investigation answers "how an issue that has already happened was figured out", while the Playground holds "we do not know yet, so let us explore" and "internal knowledge we cannot yet place in a category". Once knowledge matures, it should move into the design chain or a more natural formal location, with the evidence kept in Information; when a kind of content keeps recurring, consider creating a formal category, so that the Playground does not grow forever into a catch-all directory.

## Develop

### Working From the Project's Actual Situation

For a new project, first create the fixed directories and skeleton documents, gradually fill clear intent and design into their natural places during discussion, and create optional documents as real content appears. For an existing project, first check the current documents, code and runtime facts, keep the entry points and knowledge that are still valid, and fill in any missing fixed skeleton; when migrating, reorganize by the nature of the knowledge, avoid losing important reasons in the move, and do not write behavior incidentally observed in the code directly as a product commitment.

The task decides the scope to read and modify. You may iterate among definition, implementation, investigation and evaluation, and need not walk through every layer each time. When information is missing, first narrow the uncertainty with project evidence and reasonable inference; clarify only when the Human's intent or a substantive trade-off is involved and cannot be confirmed. Keep inferences distinct from confirmed design.

### Maintaining the Relationship Between Upper Intent and Lower Implementation

When a requirement changes, first judge which layer it affects: changes to behavior and rules require maintaining Design, changes to internal mechanisms require maintaining System Design, and changes to engineering choices require maintaining Implementation. Follow the real dependencies to check whether downstream implementation and evaluation are affected; when the upper-layer semantics do not change, do not rewrite every layer for the sake of form.

You may choose implementation approaches, debugging methods, tools and task breakdown on your own. Implementation retains considerable engineering freedom; the closer something is to the project's core intent, the less you may change the upper-layer design on your own merely to make implementation convenient. When lower-layer evidence shows the original plan does not hold, state the layer the problem belongs to, the facts and the impact, and then solve it at that layer, without hiding an upper-layer conflict behind a local patch.

### Keeping Development Knowledge in the Project

When a meaningful change to the code or the real system makes documents inaccurate, update the affected descriptions in step. Check whether the architecture, the related design and implementation notes, the usage entry points and the evaluation criteria are still true, not just the notes near the file currently being edited.

Stable behavior goes into Design, stable internal mechanisms into System Design, and current engineering details into Implementation; the investigation process stays in Investigations and immature exploration in the Playground; judgments with no natural home that are worth remembering long term go into DECISION, main-line project results and turning points into DEVLOG, and decided next steps into TODO. Do not pile all of this knowledge into the development log or chat summaries.

Clearly distinguish what has been designed, what has been implemented and what has been verified. When summarizing work, state what actually changed, the verification evidence and the remaining uncertainty; do not treat a plan as done, and do not treat local verification as overall usability. When deciding whether to retain a piece of knowledge, consider whether an unfamiliar newcomer needs it to understand correctly or to continue the work, and whether the document gains real maintenance value from it.

## Evaluate

### Designing Evaluation From Commitments

Evaluation judges whether the commitments made at each layer of the project hold, and feeds the results back to the layer that actually needs adjusting. Evaluation goals come from `PHILOSOPHY → Design → System Design → Implementation`: the upper layers focus on ultimate value and core commitments, the lower layers on concrete behavior, system constraints and engineering properties.

Design top-down: derive observable, judgeable properties from the goals that truly matter, and avoid evaluating only what is easy to measure. When a new important commitment forms, consider at once how it will eventually be verified.

Execute bottom-up: do cheap, deterministic, local checks first, then move on to integration, system and higher-level judgments. Lower-level results provide evidence and help locate problems, but they cannot automatically replace higher-level conclusions. Choose verification according to the task and the commitment; there is no rule that all tasks run one uniform full process.

### Organizing Evaluation and Evidence

The project's own evaluations are placed under `docs/evaluation/philosophy/`, `design/`, `system_design/` and `implementation/` according to the source of the commitment. Each independent topic gets an `<layer>/<evaluation_name>/EVALUATION.md`, which states at least:

1. Claim: which commitment is being verified.
2. Scope: what range it covers.
3. Method: how the evidence is obtained.
4. Metric / Oracle: which metric or basis of judgment is used to judge the result.

The source of a commitment and the Scope are two independent dimensions. Scope may be Module, Integration, System / End-to-End or Long-term; a high-level commitment can be supported by low-level evidence, and a low-level problem may need a broad run to be found. Split scopes or scenarios only when there is a real difference; a simple Suite can stay in one file.

`docs/evaluation/` holds goals, methods, criteria and traceable judgments, while execution code goes in a natural engineering location, and may use tests, evals, benchmarks, scripts, CI, Agent tasks, human evaluation or real usage results. Results need to state the corresponding evidence, run conditions and scope of validity, and parts lacking evidence remain unverified.

The Playground is for exploring the unknown, Tests check behavior and implementation constraints that are already clear, and Evaluation combines tests, experiments, runs and other evidence to judge commitments. A passing test is only evidence for its corresponding scope and cannot directly replace the evaluation of value or long-term effect.

When an evaluation fails, use the evidence to locate whether the problem comes from the philosophy, the object design, the system mechanisms, the implementation or the knowledge records, and correct the corresponding layer and the affected content. The result that truly counts is that the documents can express the Human's intent, stay consistent with engineering facts, and let a person or Agent with no historical context continue the project.
