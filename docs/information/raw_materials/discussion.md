# MukiDoc

MukiDoc is a documentation architecture method for software projects.

What it cares about is not "which standard documents should be written," nor "how to do software development," but:

> How should the knowledge in a software project be organized by different levels of abstraction and responsibility, so that humans can keep expressing design intent through documents, and implementers, especially AI Agents, can complete actual development based on those documents.

MukiDoc's core starting point is to lift documents from "explanatory material after the code is done" to the main carrier of knowledge in a project.

In traditional development, humans usually operate directly on code, and documents mostly explain and supplement.

In AI-assisted / agentic development, another way of working is possible:

> Humans mainly maintain intent, design, constraints and judgment;  
> Agents mainly translate these step by step into concrete implementation and code.

In this mode, documents are no longer just documentation, but become the main interface between humans and implementation.

---

## Core Idea

MukiDoc emphasizes a knowledge structure that refines layer by layer.

A project usually starts from very high-level intent, and then converges continuously toward concrete implementation:

```text
Intent
  ↓
Design
  ↓
System Design
  ↓
Implementation Design
  ↓
Code
```

There is no absolute boundary between "design" and "implementation" among these layers.

More precisely:

> Lower-level Design is often the Implementation of higher-level Design.

For example, in a bookstore system:

- "Users can search, buy and manage books" belongs to a higher-level design;
- "The system consists of modules such as Catalog, Order, Inventory and Account, which cooperate according to some flow" belongs to System Design;
- "Using some database, framework, protocol and code structure to land these modules" belongs to Implementation Design;
- and the final code is the concrete realization of these designs.

So MukiDoc does not try to find an absolute Design / Implementation boundary.

What it cares about more is:

> Which level of abstraction does this piece of knowledge sit at?

---

## Four Main Knowledge Areas

MukiDoc's core document structure is built around four areas:

```text
design/
system_design/
implementation/
evaluation/
```

### Design

Design describes:

> What the thing being built should be like.

It concerns functions, rules, behavior, domain logic, interaction, experience and so on.

This layer should be as independent as possible from concrete technical implementation.

If the underlying technology were replaced and this knowledge should still hold, it usually belongs to Design.

---

### System Design

System Design describes:

> How the software system should be organized and run internally to realize the Design.

Here internal modules, data models, state, lifecycle, runtime flow and the cooperation between modules begin to appear.

It has entered the internal structure of the software, but should still not bind too early to a specific framework, database, protocol or code form.

It is the important intermediate layer between domain design and engineering implementation.

---

### Implementation

Implementation in MukiDoc is more precisely Implementation Design.

It describes:

> What technical and engineering approach this current version of the software concretely chooses to implement the System Design.

Here specific tech stacks, frameworks, protocols, code structure, data structures, storage schemes, serialization formats and other engineering details can appear.

It is still a kind of design, only the object being designed has become the concrete implementation.

The true final implementation lives in the code.

---

### Evaluation

Evaluation is not just testing.

It answers:

> On what basis do we believe the preceding design and implementation are correct, effective, or good enough?

Evaluation can target any of Design, System Design and Implementation.

Different projects may evaluate in completely different ways, so MukiDoc does not force Evaluation into a unified classification.

It may focus on correctness, performance, system behavior, model validity, usability, experience, or other problems the project itself cares about.

The results of Evaluation should be able to push design changes in return, so the whole process is not one-directional:

```text
Design
   ↓
System Design
   ↓
Implementation
   ↓
Code
   ↓
Evaluation
   └────────→ feedback → Design
```

---

## Project-Level Knowledge and Local Knowledge

Besides the four main areas above, MukiDoc also distinguishes project-level knowledge from local knowledge.

Some information does not naturally belong to any specific module, but is needed to understand the whole project.

For example:

- What the project is from the outside;
- The project's long-term philosophy and principles;
- What parts the system as a whole consists of;
- What stage the project has reached;
- What key changes occurred during development;
- What decisions are worth remembering long-term.

These contents suit existing as project-level documents.

Their role is not to replace the concrete Design or Implementation documents, but to provide a global cognitive framework for the whole project.

An important principle of MukiDoc is:

> Documents should stay where the knowledge most naturally belongs, rather than being forcibly classified to fit a template.

So the directory is a tool for organizing cognition, not a strict ontological classification.

---

## Information and Experimental Knowledge

MukiDoc also allows an auxiliary information area.

It can hold:

- Feasibility studies;
- Investigations of tool and dependency capabilities;
- External material;
- Algorithm or technology notes;
- Knowledge that has not yet entered the formal design.

Among these there can be a `test_playground/`, dedicated to exploratory experiments.

It can hold:

- benchmarks;
- feasibility tests;
- algorithm correctness experiments;
- performance experiments;
- library / API capability tests;
- temporary verification.

The difference from Evaluation is:

> `test_playground/` is for exploring and discovering;  
> `evaluation/` is for forming relatively formal judgments and conclusions.

---

## The Role of Architecture

MukiDoc holds that a project needs a global Architecture view.

Architecture is not simply the sum of Design, System Design and Implementation.

Its role is:

> Before entering local details, to provide a stable map of the system.

Architecture should help the reader understand:

- What the main parts of the system are;
- What each part is responsible for;
- Where the boundaries lie;
- What relationships exist between them.

It is a project-level navigation structure, and important context before a human or Agent dives into concrete documents.

---

## Decisions and Development History

MukiDoc does not require a complex ADR system.

Design decisions should live as naturally as possible in the corresponding documents:

```text
Background
→ Constraints
→ Problem
→ Reasoning
→ Design
→ Impact
```

Readers should be able to understand why a plan was reached by reading the design itself.

For key decisions that deserve to be remembered separately over the long term but need not be written up as full documents, a concise supplementary decision document can be used.

Its role is only supplementary, not to become the sole home of all design reasoning.

Beyond that, MukiDoc also values the project's development history. A chronologically maintained development record can hold:

- What was done at a given stage;
- What was discovered;
- What was solved;
- Why important adjustments happened.

This differs from Git history.

Git history records code changes, whereas what is kept here is the development history at the level of project cognition.

---

## MukiDoc and AI Agents

MukiDoc is not a system that can serve only AI development.

But it is very well suited to Agent-driven software development.

The reason is:

> The project's key knowledge does not depend on a single chat, a single developer's brain, or a single Agent's temporary context, but is explicitly kept in the project's own documents.

So when a new Agent takes over a project, it can rebuild its understanding of the project by reading the documents.

In the ideal state:

```text
Human Intent
    ↓
Documentation
    ↓
Agent
    ↓
Code
```

When the implementation result does not match the intent, the human first modifies the design or constraints in the documents, rather than making lots of local patches directly in the code.

This reduces the long-term drift of:

```text
The docs say A
The code implements B
The human's real intent is C
```

From this angle, MukiDoc can treat documents as:

> the control surface of human–agent collaboration.

---

## Don't Manufacture Documents for Completeness

MukiDoc is not checklist-driven documentation.

A project does not need to create every possible document in order to "conform to MukiDoc."

If a project has no complex data model, there is no need to create a dedicated data model document.

If there is no API, an empty API document should not be created just to make the directory look nice.

If a piece of knowledge is simple enough, it can just live in the corresponding module document.

The core principle is:

> Structure should serve knowledge, not the other way around.

MukiDoc provides a documentation architecture and levels of abstraction, rather than requiring a project to fill in a template.

---

# The MukiDoc Repository Itself

MukiDoc's open-source repository should be a Meta project.

That is to say:

> This repository not only explains MukiDoc; it itself uses MukiDoc to describe MukiDoc.

So the repository itself is a real instance of this system.

Note a structural convention:

```text
README.md
docs/
```

The root `README.md` is the GitHub / repository entry page.

It does not belong to the MukiDoc documentation system itself, and is responsible only for:

- Explaining in a minimal amount of text what this repository is;
- Guiding readers into `docs/`;
- Saying where to start reading.

What truly belongs to the MukiDoc method system all lives inside:

```text
docs/
```

In other words, this repository itself forms a kind of recursive structure:

> MukiDoc uses MukiDoc to describe and organize MukiDoc.

This is not an extra example project; it is the design of the project itself.

---

## Final Goal

What MukiDoc hopes to become is not a heavy software engineering specification, but a lightweight, clear, evolvable documentation architecture for software projects.

It should help people keep answering:

> What are we building?  
> Why is it designed this way?  
> How should the system work internally?  
> How is it concretely implemented now?  
> How do we know it is right?  
> How did the project get to where it is today?

And let these answers live long-term in the project itself, rather than scattering across human heads, chat logs or code details.

MukiDoc's core value can be summarized as:

> **Organize a software project's intent, design, implementation knowledge and evaluation basis by level of abstraction, so that documents become a long-term inheritable knowledge structure of the project.**

In Agent-driven development, this further means:

> **Humans maintain the project's knowledge; Agents implement it.**
