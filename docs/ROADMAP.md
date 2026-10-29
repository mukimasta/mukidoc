# Roadmap

MukiDoc's roadmap revolves around one goal: to grow from a clear software engineering documentation method into a development system that humans and AI can use reliably, that maintains itself automatically, and that evolves over the long term.

## 1. Methodology

Establish MukiDoc's foundational methodology.

This stage clarifies the responsibilities, boundaries and layer relationships of the whole documentation system, and completes the Design of the main document types. The core is a stable structure of project understanding, and the decoupling between the three layers: Design, System Design and Implementation.

Once this stage is done, MukiDoc should be able to guide a project from high-level intent to concrete implementation using the documentation specification alone.

## 2. Documentation Specification

Turn the methodology into a complete, executable documentation specification.

This requires settling what each kind of document should express, how it is organized, what constraints it has, and how the different documents together form a complete software engineering context.

It also establishes unified writing and maintenance rules for all documents, so that documents produced by different projects, developers and AIs remain consistent.

## 3. Agent Workflow

Design how AI works in a MukiDoc project.

This stage clarifies how the AI reads project context, how it locates the documents affected by a requirement, how it completes design and implementation layer by layer, and how it keeps the related documents in sync when changing code.

The goal is to take MukiDoc from "humans write documents according to the specification" to "humans state requirements, and AI keeps maintaining the project according to the system."

## 4. Tooling

Gradually implement the stable methods and workflows as tool capabilities.

Tools help projects bootstrap MukiDoc, provide document templates and rules, help the AI obtain the right context, and check the structure, completeness and consistency of documents.

This stage does not change MukiDoc's method itself; it lowers the cost of using and maintaining it.

## 5. Validation

Continuously validate MukiDoc through real software projects.

The focus is on whether the system keeps context complete over long-term development, whether a new AI can take over a project quickly, whether the three design layers effectively reduce coupling, and whether document synchronization genuinely lowers human cognitive load.

Problems found in validation should in turn drive further adjustment of the method, specification and tools.

## 6. Reusable Development System

Ultimately, MukiDoc should become a human-AI collaborative development system that can be reused across projects.

Developers can create projects, express designs, state requirements and check results in a stable way; the AI can understand the project, keep developing it, and keep the context in sync. The project itself holds enough complete software engineering knowledge that it can continue to evolve without depending on a particular developer, a particular Agent, or past conversations.
