# MukiDoc Single Document Design

Documents in MukiDoc should first of all aim at clarity, naturalness and high information density. A document serves understanding first: it should not add structure to look formal, nor sacrifice necessary context and reasoning for brevity.

Content should stay within the current document's responsibility and abstraction level. Questions of different levels should be expressed separately, so that high-level design, system mechanisms and concrete implementation are not mixed together.

Body text defaults to natural paragraphs. Where there is continuous derivation, causation, explanation or a complete argument, prefer paragraphs; use subheadings or itemized expression only when several items are parallel, sit at the same level, and are clearer read or checked one by one.

Writing follows these constraints by default:

1. Use direct, natural, concrete language; avoid boilerplate, repeated explanation and pointless lead-ins.
2. Without a genuine contrast, do not use opposition patterns such as "not X but Y" or "rather than X, Y".
3. Do not overuse bold. Emphasize only where a visual anchor is really needed.
4. Do not create unnecessary multi-level headings. Use heading levels continuously according to the document's actual structure: with one level, use level-3 headings; with two, levels 2 and 3; with three, levels 2, 3 and 4.
5. Do not force lists for the sake of tidiness; use lists only for genuinely parallel information.
6. Where a list is appropriate, prefer ordered lists over unordered lists.
7. Avoid cross-document references as far as possible. Each document should be self-contained within its responsibility, so readers need not jump between files and editors need not depend on too many; reference only when the content genuinely belongs to another document, or when maintaining it twice would cause a clear consistency problem.
8. When modifying an existing document, integrate new content into the most natural place instead of continually appending patches at the end.
9. Avoid examples where possible. A document should describe real rules and states directly and completely; use a concrete example only when the scenario is itself the needed information, or when the abstract content cannot be expressed without distortion.
10. Document naming: all caps, with words joined by underscores.

The base skeleton must exist: the repository root README.md and AGENTS.md, and OVERVIEW.md, PHILOSOPHY.md, ARCHITECTURE.md, ROADMAP.md, DECISION.md, DEVLOG.md and TODO.md under docs/ are all fixed documents. During bootstrap or migration, fill in what is missing and keep existing content; when there is no content yet, only the title may be kept, and no body is invented. A file existing does not mean its content is complete.

Fixed directories include docs/, the three design-chain layers, Information and its four category directories, and Evaluation and its four commitment-source directories, to be kept even when empty. Git projects keep empty directories with `.gitkeep`. Areas, concrete design documents, Evaluation Suites, and optional documents such as DATA_MODEL.md, RUNTIME.md, TECH_STACK.md and API.md are still created on demand.

Specific document types may further define their own structure, length and writing style, but inherit these principles by default.
