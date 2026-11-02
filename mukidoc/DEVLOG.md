# Devlog

### 2026-09-13

1. Re-examined the software engineering documentation habits I have long used, starting from arc42. Concluded that arc42 is better suited as an architectural viewpoint and checking framework, whereas what we really need is a project knowledge system that better fits actual thinking and AI-driven development.

2. Took a first pass at the project-level document structure: README, OVERVIEW, PHILOSOPHY, ARCHITECTURE, ROADMAP, plus regions such as Information, Design, Implementation and Evaluation. Began making explicit that each kind of document should carry a different cognitive responsibility, rather than piling all project knowledge into one big document.

3. Made explicit that the role of documents has changed in AI development: the Human can express and modify intent mainly through documents, while the AI is responsible for turning that intent into code. Documents began to be seen as the main collaboration interface between Human and AI, not just an explanation written after the code is done.

### 2026-09-14

1. The original two layers, Design / Implementation, exposed a clear boundary problem when discussing things like Database: many stable internal system mechanisms belong neither to the Design of the object itself nor should be swallowed by concrete technical implementation. We finally added System Design, forming the core three-layer Design Chain: `Design → System Design → Implementation`.

2. Further clarified the meaning of the three layers: Design describes what the object itself should be, System Design describes how the internal system should work, and Implementation describes how the current engineering concretely implements it. Accepted the fact that "lower-level Design is also higher-level Implementation," and stopped pursuing a mechanical, absolute classification.

3. Completed the structural design of PHILOSOPHY, and wrote a full version using MukiDoc itself as the first real subject. PHILOSOPHY finally adopted a structure that derives step by step from situation and problem through the essential need, core idea, mode of operation and effectiveness to principles, rather than listing values directly.

4. Completed the basic design of OVERVIEW and ARCHITECTURE. ARCHITECTURE finally settled on a graphical reading style that zooms in continuously from coarse to fine, then observes the system from the Runtime angle, and finally lands via the architecture tree and file structure; this structure was validated in MukiDoc's own Architecture.

5. Project Context gradually stabilized into several distinct dimensions: OVERVIEW, PHILOSOPHY, ARCHITECTURE, ROADMAP, DECISION and the project's development history. README was repositioned as a user-facing GitHub homepage, so it stays in the repository root, and we decided to finish it once MukiDoc is actually usable.

6. ROADMAP originally considered maintaining past, present and future together; after discussion we found the cost of dynamic maintenance too high, and finally changed it into a static long-term capability roadmap. Stages are divided by "a qualitative change in capability or maturity," not by feature, version or time.

7. We had planned to record key architectural decisions with ADRs, but found that many decisions can already live naturally in the formal documents, and separate ADRs easily cause duplication. We finally switched to a single `DECISION.md`, keeping only the few key judgments that have no natural home but are worth remembering long-term, and focusing on recording "why this decision came about."

8. The root-level `IMPLEMENTATION.md` clearly conflicted semantically with `implementation/` in the Design Chain. After rethinking, we renamed the project-level timeline to `DEVLOG.md`: DEVLOG records what happened across the whole project, while a local Implementation keeps how a specific part is implemented, debugged and evolved.

9. Information gradually differentiated from a simple research directory into Raw Materials, External Information, Investigations and an experimentation area. Along the way we made explicit the boundary that "evidence stays in Information, and stable conclusions enter the formal Design Chain."

10. Evaluation expanded from the initial vague "test and performance results" into an independent system. Confirmed that Evaluation should derive directly from the commitments made by each layer: PHILOSOPHY, Design, System Design and Implementation; and distinguished two orthogonal dimensions: "which layer the commitment comes from" and the evaluation Scope such as Module / Integration / End-to-End.

11. Made explicit that Evaluation should be designed top-down and executed bottom-up: first decide from the highest-level goals what is really worth evaluating, then at run time prefer cheap, deterministic low-level checks first, and gradually use evidence to support high-level judgments. Also established that Playground is for exploration, Tests are for checking, and Evaluation is for judgment.

12. Started designing `AGENTS.md`. Finally abandoned restricting the Agent with fixed steps and reading orders, and instead "compiled" MukiDoc's detailed Design into a dense Agent protocol that keeps only the project map, knowledge semantics and the invariants that truly must not be broken, and explicitly made full use of trust in strong models' own judgment and execution.

### 2026-09-15

1. Applied the current MukiDoc system directly to an existing software project, and had the AI rewrite the original documents according to the new knowledge structure. The rewrite was clearly better than the original structure, preliminarily validating that the three-layer Design Chain, Project Context and the unified writing rules can be correctly understood by an AI and used to migrate a real legacy project.

2. This real migration made the goal of MukiDoc Evaluation more concrete: beyond format and consistency checks, what matters more is verifying whether a new Agent can rebuild context relying only on the current project, correctly locate design layers, and continue development. Legacy project migration and fresh-agent handoff thus became evaluation scenarios worth formalizing.

3. Information's original `test_playground/` could not hold a valuable meta-structure write-up that is neither an experiment, an investigation, external material, nor raw material. This conflict exposed that "internal knowledge that is not yet mature and temporarily has no formal home" is itself a real state, so the directory was renamed to the more honest `playground/`, allowing thinking, drafts, exploration and experiments to exist temporarily before they mature.

4. Made explicit that content in Playground can "graduate": when a kind of knowledge recurs and takes on stable meaning, it should move into the formal Design Chain, a new Information category, or another more natural place, rather than letting Playground become a permanent catch-all directory.

### 2026-09-16

1. Added `TODO.md` as the current action surface of Project Context. TODO records only actionable items already decided, and allows a separately maintained Waiting list; long-term direction continues to be managed by ROADMAP, and the history of completed work by DEVLOG.

2. Added the design of `README.md`, making explicit that README is the user-facing entry point of the repository, responsible only for presentation and navigation and not holding formal project knowledge. Also clarified its division of labor with OVERVIEW: README helps a stranger quickly judge and get started, while OVERVIEW helps someone about to develop build an accurate understanding; and stipulated that for an existing project, a still-valid README is not forcibly rewritten just to unify format.

3. Distinguished two kinds of Evaluation that are easily conflated: a MukiDoc project's own evaluation of its product and business, and the built-in evaluation that ships with every MukiDoc project to judge whether the project knowledge system is healthy, naming the latter MukiCheck. In a meta project like this repository the two almost coincide on the surface, which is exactly why the boundary needs to be drawn explicitly, to avoid merging them again in the future.

4. Completed the design of MukiCheck, divided into three layers: static document checks, joint document-code checks, and dynamic comprehension checks, gradually adding real engineering and real usage on top of read-only knowledge. The static layer's Philosophy alignment only checks whether the current design deviates from the project's own declared Philosophy, while "can an unfamiliar Agent rebuild context from the documents alone" is left to the dynamic layer, verified with a fresh Agent that has no history, turning the previously proposed fresh-agent handoff goal into a concrete evaluation.

5. Re-examined MukiDoc from the deliverables perspective, identifying deliverables such as Specification, AGENTS.md, MukiCheck, Bootstrap and Migration, and accordingly added a "Deliverables" section to OVERVIEW's fixed structure.

6. Found that each layer of the Design Chain still lacked an internal organizing dimension, and finally abstracted it as "fixed Layer, free Area": the three vertical layers are unchanged, horizontal Areas form naturally from the project, with no mirroring, growth on demand, and cross-cutting concerns at the layer root. On this basis we reorganized design/, splitting it into specification/ (the definition of the method itself) and deliverable/ (capabilities built on top of it), with the designs of the Project Context documents placed under specification/.

### 2026-09-25

1. Made explicit that AGENTS.md must be deliverable on its own to other projects that cannot access MukiDoc's source specification, so the compilation target converged from a short summary to retaining the complete rules that affect understanding, judgment and execution, with no preset line limit. Necessary structural constraints, boundaries, design rationale and examples should all be kept.
2. Wrote the first version of the root AGENTS.md, covering Role, MukiDoc, Design, Develop and Evaluate, compiling the specifications of each document type, the knowledge-maintenance relationships and the MukiCheck checking requirements into a single protocol. An unfamiliar Agent's independent understanding and real-project effectiveness remain to be verified.
3. The current protocol does not yet include the not-yet-built MukiCheck: its checking section and directory conventions were removed, keeping the project's own Evaluation rules; the delivery scope of AGENTS.md was also made explicit.
4. A real-project review exposed that the protocol's skeleton requirements did not match expected usage: the original "create on demand" let a missing Information category directory and TODO still be judged normal. Made explicit that base directories and skeleton documents must exist even when temporarily empty, while Areas, Evaluation Suites and optional documents continue to be created on demand; the specification and protocol were corrected accordingly.
5. Implemented the in-repo `mukidoc-init` Skill, version 0.1.0, with a standalone bootstrap script, skeleton templates and a versioned AGENTS.md. Completed the Design, System Design, Implementation and evaluation definitions of Bootstrap; bootstrap preserves existing files, an older protocol is backed up and then replaced only after explicit confirmation, and unversioned, same-version-modified and newer-version cases are handled separately.
6. The bootstrap deliverable passed 18 temporary-project tests, a resource export consistency check and a Skill structure validation, verifying the complete skeleton, repeated runs, version recognition, backup and standalone distribution. The update-confirmation behavior in real conversations remains to be verified; this round did not install a personal Skill or migrate an external project.

### 2026-10-29

1. Re-stated MukiDoc's positioning: a structured documentation protocol designed for large projects. AI makes code cheap, and what really matters is holding on to a project's vision, decisions and direction; MukiDoc hands these to AI in layers, giving it a global view rather than scattered memories.

2. Made the human-to-AI authorship gradient explicit: the higher the layer, the more humans design and write it themselves; the lower, the more it is handed to AI. PHILOSOPHY, OVERVIEW and README were updated accordingly.

3. Published the Chinese repo mukidoc-zh and the English repo mukidoc as v0.1.0, with the Chinese version as the single source.

4. Changed the documentation root from `docs/` to `mukidoc/` and bumped the protocol and Skill to 0.2.0. `docs/` is left for the project's own user documentation and articles. No legacy-layout detection or automatic migration; projects already on 0.1.0 stay as they are.

### 2026-11-01

1. Changed the positioning to "a structured documentation protocol designed for Agent-Native large projects", making clear that MukiDoc targets projects built jointly by humans and agents, not just projects of large scale. README and OVERVIEW were updated accordingly.
