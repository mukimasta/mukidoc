# README Design

README is the project's Human-facing entry point in the repository, letting someone who opens the project for the first time quickly learn what it is, whether it is worth reading on, how to start, and where to go next.

It handles presentation and navigation and does not carry the formal storage of Project Context knowledge. README may reference or summarize the project's important information, but content that truly needs long-term maintenance should live in the corresponding formal documents.

README usually contains:

* The project name and a one-sentence value description.
* A short project introduction so the reader quickly understands what it can do.
* Screenshots, a demo, diagrams or other showcase content where helpful.
* When the project is already usable, the shortest possible Quick Start.
* A Documentation entry point guiding developers to the formal documents such as OVERVIEW, PHILOSOPHY and ARCHITECTURE.
* Any other outward-facing information the project really needs, such as status, installation, usage, contribution or License.

README may be more presentational than other MukiDoc documents but should still stay concise. Detailed design, architecture, development history and methodology should not be expanded in README.

README and OVERVIEW have different responsibilities: README is for people first entering the repository, helping them judge and start quickly; OVERVIEW is for people preparing to understand and develop the project, and builds an accurate understanding of it.

For an existing project, MukiDoc should not forcibly rewrite an already effective README just to unify the format. Prefer keeping the original outward entry point, and only where necessary tidy the structure, fill in missing information and add MukiDoc document navigation.

A good README lets a stranger know within a short time: **what this is, why it is worth a look, how to start, and where to go next.**
