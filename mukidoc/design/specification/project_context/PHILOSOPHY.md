# PHILOSOPHY Design

PHILOSOPHY answers the project's topmost "why". Starting from a real problem, need or initial idea, it keeps asking about its essence, and from that derives the project's core ideas, how those ideas operate, and why they work.

It does not introduce the whole project, nor describe concrete features, modules, directories, technical solutions or implementation detail. What it provides is the intellectual foundation that later design depends on. After reading it, the reader should understand why the project took its current direction, and be able to use these ideas to judge whether a future new proposal fits the project itself.

The whole text should form one continuous chain of derivation:

**Situation and problem → Needs and ideas → The essence of the need → Core approach → How it operates → Why it works → Principles and approach**

**Situation and problem.** Establish the starting point from a real scene or background, and state what problem originally existed. 1–2 paragraphs are recommended.

**Needs and ideas.** State what need arises naturally from this and what was initially hoped to change. 1–2 paragraphs are recommended.

**The essence of the need.** Keep asking downward and state the problem that truly needs solving behind the surface need. 1–2 paragraphs are recommended.

**Core approach.** This is the main body of the text; it should be derived naturally from the essential problem above, explaining the project's most important ideas, methods and relationships. 3–6 paragraphs are recommended, taking the most space of the whole text. The core ideas must stay at the Philosophy level and not enter concrete design and implementation.

**How it operates.** Use one typical scenario to show how these ideas actually play out, especially suited to describing collaboration among people, systems or other participants. Fixed at 1 paragraph.

**Why it works.** Return to the original problem and explain why the core ideas above can solve it. Fixed at 1 paragraph, with no new core concepts introduced.

**Principles and approach.** Compress the key ideas derived in the text into a few principles, only summarizing and adding no new design. Close the whole text with one sentence. Fewer than 8 items is recommended; if the ideas are complex, nested lists may be used, but the outer level has no more than 8 items.

The body is mainly continuous argument. Each part uses `**Subheading.**` followed directly by the text, with no multi-level Markdown headings. Only the final "Principles" uses an ordered list; the other parts default to natural paragraphs.

The parts must follow one another, each arising naturally from the previous. Principles should be a result of the derivation, not the starting point of the text. If a core claim can only be accepted as a conclusion and cannot be naturally reached from the preceding text, the reasoning needs to be filled in.

The whole text is no more than 2000 words. The core ideas may be developed fully; the rest stays restrained.

A well-finished PHILOSOPHY achieves three things: it lets the reader understand how the core ideas came about; it lets these ideas guide later design judgments; and even if the concrete architecture, technology and implementation change, its main content still holds.
