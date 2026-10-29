# DESIGN CHAIN Design

The Design Chain splits software design into three connected, as-decoupled-as-possible layers:

**Design → System Design → Implementation**

The reason for three layers is that development always involves three different questions: what exactly are we trying to design; for it to hold, how should the internal system work; and under current engineering conditions, how exactly do we build it.

When these three questions are mixed, the upper-level design is easily bound to one version of a technical solution, and the structure that truly matters inside the system is easily buried in code and implementation detail. With three layers, the upper layer defines stable semantics and constraints, the lower layers have freedom of implementation within them, and each layer can evolve independently.

## Design

Design describes what the designed object itself should be like.

It is concerned with "what we ultimately want to get". It does not consider how the software is organized internally and does not decide ahead of time which technology to use. As long as the object itself does not change, this layer should stay largely stable even if the whole system is reimplemented.

Typically it covers:

* Features and capabilities.
* What users or other participants can do.
* Core behavior and rules.
* Interaction and experience.
* Core concepts of the domain and their relationships.
* Important properties the object must maintain.
* The main trade-offs and rationale behind the design.

Without this layer, a project easily jumps straight from requirements to a technical solution. Over time, "it happens to be implemented this way now" gradually turns into "it was always meant to be this way", and the implementation starts to constrain the design in return.

## System Design

System Design describes how the internal system should be organized and run in order to realize the Design.

This layer begins to enter the software's interior but still avoids binding to specific technology. It translates the object-level design into an internal system that can actually run.

Typically it covers:

* Which modules the system consists of.
* The responsibility and boundary of each module.
* How modules cooperate.
* Core state and state changes.
* The logical data model and data relationships.
* Lifecycles.
* Key business flows and runtime flows.
* System-level mechanisms such as concurrency, synchronization and error recovery.
* Constraints that stay stable across modules over the long term.

Many System Designs persist across several generations of technical implementation, so they should not be tied to a particular framework, database or code structure.

Cross-module data relationships can be gathered in `DATA_MODEL.md` as needed, and important dynamic processes in `RUNTIME.md` as needed.

## Implementation

Implementation describes how the current engineering concretely realizes the System Design.

Only at this layer do we actually enter the technology and engineering solution currently adopted. Implementation can change quickly with the technical environment; as long as the upper design is unchanged, changing the tech stack or refactoring the engineering structure should affect only this layer as far as possible.

Typically it covers:

* Programming languages, frameworks and runtime environments.
* Databases, caches and messaging systems.
* APIs, protocols and interface contracts.
* Concrete data structures and storage structures.
* Dependency libraries and third-party services.
* Concrete implementation of concurrency, threading and task scheduling.
* Serialization, configuration and deployment.
* Performance optimizations.
* Important technical constraints and conventions in the current engineering.

Project-level technology choices can be gathered in `TECH_STACK.md` as needed, and concrete interface contracts in `API.md` as needed.

## Why three layers

Only two layers, Design and Implementation, are usually not enough, because "how the internal system should work" is itself an important and relatively stable layer of design. Place it too high and Design enters the software's interior too early; place it too low and the long-term stable system mechanisms get mixed with the current technical solution.

As the common spine of the whole project, the three layers answer, in turn:

**What the object is → How the system works → How it is implemented now**

Projects can of course subdivide further within each layer, but there is no need to add more fixed top-level layers.

## Layer boundaries

To decide which layer an item belongs to, look at what changing it would mean:

1. If the object's own behavior, rules or properties change, it belongs to Design.
2. If the object is unchanged but the internal structure, state, data relationships or runtime mechanism change, it belongs to System Design.
3. If the system mechanism is unchanged and only the engineering and technical solution changes, it belongs to Implementation.

The boundary need not be mechanically exact. What matters is keeping a document at one abstraction level as far as possible, so that lower-level detail does not gradually seep in and bind the upper-level design.

## Area

The three layers are the fixed vertical dimension; within each layer a horizontal dimension is also needed to organize documents, and it is called Area. An Area is a problem space that forms naturally in a project and is relatively stable; it can be a deliverable, a product capability, a domain or a class of system concerns, as the project itself decides.

This gives the organizing principle of the Design Chain: fixed Layers, free Areas. The three layer directories `design/`, `system_design/` and `implementation/` must be created and kept even when empty; Git projects keep empty directories with `.gitkeep`. Horizontal Areas grow with the project, are not prescribed in advance, and do not follow a uniform template.

Areas follow three rules:

1. No mirroring. An Area existing under `design/` does not require a same-named Area under `system_design/` and `implementation/`; each layer has documents for an Area only when knowledge of that layer has actually arisen.
2. Grow on demand. An Area with only one document is simply a flat file, with no folder pre-built for structural completeness; when the same problem space naturally accumulates several documents, upgrade it to a directory, and inside an Area sub-Areas can nest in the same way.
3. Cross-cutting content goes at the layer root. Concerns that span several Areas, such as the logical data model, runtime flows, tech stack and interface contracts, go directly at the root of their layer and are not squeezed into one Area.

The fixed layers provide a stable knowledge entry point, while the Areas and concrete documents within a layer reflect the knowledge boundaries and volume the project has actually formed. Empty base directories are allowed, and no content should be invented for them; optional files such as DATA_MODEL.md, RUNTIME.md, TECH_STACK.md and API.md are still created on demand.

## Examples

Imagine an ordinary "login".

At the Design layer, we care only that a user can log in after entering credentials, that the login state persists afterward, and that different identities see different permissions.

At System Design, the questions become: how does the system know who you are? After authentication succeeds, how is the login state established? How is it confirmed on each request that this person still has permission? Internal mechanisms such as authentication, session and authorization may appear here, yet we have still not decided between Redis and a database, nor which framework.

At Implementation, the solutions are finally chosen: which algorithm for passwords, whether sessions live in Redis or a database, how cookies are set, how the endpoints are written, and which libraries implement the code. If Redis is replaced in the second year, usually only this layer is touched; if the internal authentication mechanism is redone entirely, the change rises to System Design; only if the product decides "there will be no login at all" has Design changed.

Now imagine a file upload feature.

Design may be just: users can upload files, see upload progress, retry after failure, and use the uploaded file in later features once the upload completes.

System Design continues to consider: does an upload task have state? Are large files split into chunks? Where does recovery resume after a failure? When does a file count as truly complete? Who manages metadata and who manages file content? These already determine how the system works, but do not yet dictate which cloud storage to use.

Implementation decides last: the file actually goes in S3, what the chunk size is, which SDK handles uploading, which table holds task state, and which queue performs retries. If S3 is later swapped for another object store, as long as the system mechanism is unchanged, Design and System Design can stay largely untouched.

The goal of the Design Chain is to let "what we really want", "how the inside makes it hold" and "what we use to build it today" each stay in the right place, so that both people and AI can tell clearly at which layer a problem should be solved.
