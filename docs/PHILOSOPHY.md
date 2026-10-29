# MukiDoc Philosophy

**Situation and problem.** In traditional software development, much important knowledge never really lives in the project; it is scattered across people's heads, code, meetings and ad-hoc conversations. Requirements, design, system structure and concrete implementation also blur together easily: an idea lands quickly in code, and an implementation choice gradually comes to define the system itself. The larger and longer-lived a project, the more understanding it turns into understanding the code; individuals forget their earlier judgments over time, and different people on a team hold different information.

AI changes this relationship. Once code can be generated, modified and refactored quickly, code itself becomes cheap, and what is truly scarce is the project's vision, decisions and direction: understanding the problem, forming the design, building structure, making trade-offs, and judging whether the result matches the original intent. In the past these were held mainly by people, while AI saw only the code and conversation in front of it.

**Needs and ideas.** We therefore want a method built from the start for humans and AI developing together. People no longer control a project mainly by operating on code directly, but express intent, design and judgment through more stable documents; AI refines and implements from this context while keeping code and documents consistent.

If vision, decisions and direction are what matter most in a project, they should be given to AI as well. An AI that can see the whole understands not only the code in front of it but also why that code exists and where it should evolve, and so has a chance to make better judgments.

**The essence of the need.** The real problem is not how to make AI better at writing code, but how to keep a software project's important knowledge from depending on any one person, any one conversation or any one version of the code, and to have it held by humans and AI together.

Memory is not mastery. Remembering what was said and done before is not the same as understanding what the project is, why it is designed this way and what state it is in now. A project needs to keep its goals, design rationale, implementation state, key decisions and evolution, so that new developers or new AIs can re-enter it without excavating code and chat logs.

This knowledge also cannot be collapsed into a single layer, still less left without structure. What we want, how the internal system works and how it is currently implemented are three different questions; mixing them binds upper-layer design to lower-layer technology too early. Without a clear structure, AI cannot maintain these documents over time either: it does not know where a piece of knowledge belongs, and the documents soon become duplicated, contradictory and messy.

**Core approach.** This method is first a software engineering method designed for human–AI collaboration. Documents sit between humans and AI as the shared context and main collaboration interface, and keep the project's core understanding inside the project itself: code can change, AIs can be swapped, conversations can end, and the project's understanding still carries on.

The heart of the concrete design is three successive but decoupled layers: Design, System Design and Implementation. Design describes what the created thing itself should be, concerned with its functions, rules, behavior and domain properties; System Design describes how the internal system should be organized and run to realize that design; Implementation then lands the system design in the current concrete engineering environment. Each upper layer defines what must hold, and the layer below decides how to make it hold; one Design can have different System Designs, and one System Design can have different Implementations. The point of layering is not to draw absolute boundaries, but to decouple decisions at different levels of abstraction, so that upper-layer intent stays stable while the structure and implementation below evolve freely.

The three layers also map onto the division of work between humans and AI. The higher the layer, the closer it is to the project's vision and direction, and the more it needs humans to think it through and write it themselves rather than handing it all to AI; the lower the layer, the closer it is to concrete engineering, and the more it can be done by AI. Humans own PHILOSOPHY and Design, work through System Design together with AI, and hand Implementation mainly to AI.

Structure is likewise the precondition for AI to maintain the documents. The protocol makes clear what each kind of knowledge means, where it lives and how it relates, so AI can tell which layer a change belongs to and which documents to update, keeping the documents clear, accurate and tidy over long-term development.

**How it operates.** When a new requirement appears, a person first clarifies what they really want and writes or revises the upper-layer intent and design, then refines it layer by layer with AI into a system design and implementation plan; once the information is clear enough, AI writes the code and, following the protocol, updates the affected documents, while the person mainly checks that those documents still express the project accurately. Running the system and Evaluation produce new facts; if the results fall short, the person decides whether the problem belongs to design, system design or implementation, fixes that layer, and syncs downward again, forming a continuously iterating loop.

**Why it works.** This approach splits a problem that would otherwise have to be held all at once across different levels of abstraction, so people only need to focus on the judgments that matter right now; as the upper-layer design becomes clearer layer by layer, AI has less and less to guess, and can judge from the whole project rather than local code alone. Context is kept inside the project, so individuals need not rely on memory, and teammates and new AIs can build understanding from the same documents; clear structure in turn lets AI maintain those documents over time. People can therefore focus on vision and trade-offs while always keeping control of the project.

**Principles and approach.**

1. Code is getting cheaper; a project's vision, decisions and direction are what is scarce, and they should be recorded explicitly and given to both humans and AI.
2. A project's important context should live in the project itself as far as possible, not in people's memories, ad-hoc conversations or one version of the code; memory is not mastery.
3. Design, System Design and Implementation should keep clear levels of abstraction and stay decoupled: upper layers define semantics, lower layers decide how they are realized.
4. The higher the layer, the more it is designed and written by humans; the lower, the more it is handed to AI. Humans own problems, intent, judgment and trade-offs; AI owns refinement, implementation, syncing and execution.
5. Documents need a clear structure and protocol so AI knows where knowledge belongs and can keep the documents clear and tidy over time.
6. Documents and code should evolve together, and new facts from running the system and from Evaluation should keep flowing back to the right design layer.

Ultimately, this method aims to keep a project's intent, structure and knowledge in human hands, while letting an AI with a global view take on more and more of the work between clear design and concrete implementation.
