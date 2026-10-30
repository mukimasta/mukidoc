# How Many Layers Is This Thing, Anyway

Writing MukiDoc feels a bit strange. You write the rules while discovering you're obeying them; you describe this repo while what you're describing is the description itself. A mirror facing a mirror: easy to get dizzy.

After getting thoroughly muddled, I split it into three axes, and the dizziness went away.

## Three Axes

**The vertical one goes down, not deeper.**

```
design/          Design
system_design/   System Design
implementation/  Implementation
src/             Code
```

Layer-by-layer refinement, with a direction and an end: it stops when it reaches code. It doesn't recurse; it just walks down the stairs.

**The horizontal one is side by side, not above and below.**

OVERVIEW, PHILOSOPHY, ARCHITECTURE, ROADMAP, DECISION, DEVLOG: six facets of the same project, none leading the others.

**The third one is a loop, not a tower.**

```
design/project_context/OVERVIEW.md   specifies  how docs/OVERVIEW.md is written
design/project_context/DEVLOG.md     specifies  how docs/DEVLOG.md is written
```

And `design/project_context/` happens to be exactly the crossing point of the vertical and the horizontal: using the Design layer to design the set of Project Context documents. This is where the mirror faces the mirror.

## Not Infinite Recursion, but Bootstrapping

Recursion diverges. Bootstrapping stops.

```
design/DOC.md  ← is specified by design/DOC.md
```

And here it closes. The floor is natural language: you can't write yet another "Design of DOC.md", because the rules themselves are human language, and human language is the bottom. A compiler compiles itself, and nobody asks for a "compiler that compiles the compiler."

So the depth is finite: one loop, one self-referential point. Nothing scary.

## Why Changing design Changes the Whole Project

In an ordinary project this causality exists too, just slowly: change the design → write code → a few days later the project has changed.

Here the thing being designed is the documents themselves, so design and product coincide, and the compile distance is zero. So one edit to `docs/design/` and the whole project changes on the spot.

It's not a new kind of causality; it's that the distance between design and product has been squeezed to nothing.

## The Loop That Really Keeps Turning

```
design/project_context/AGENTS.md.md ──specifies──▶ AGENTS.md
AGENTS.md ──guides──▶ Agent
Agent ──modifies──▶ docs/design/**
docs/design/** ──recompiles──▶ AGENTS.md   ← and we're back
```

A runtime control loop. The Agent works by AGENTS.md, and the work is maintaining the very documents that define AGENTS.md.

When I came in, the root `AGENTS.md` was 0 bytes: the moment the loop was just being connected.

## When You're Lost, Ask Three Questions

1. Is this **content**, or a **rule specifying what content should look like**?
2. Does it specify **shape** or **content**? (This distinction is the key; otherwise the loop smears into one blob.)
3. Which **axis** is it standing on?

## Incidentally, This Directory Is Also a Case in Point

It used to be called `test_playground`, a name that presupposed "experiments to be verified go here." Then a structural write-up got stuffed in: not an experiment, producing no facts, so the name didn't fit.

Renaming it `playground` fixed it. The problem was never which category it belongs in; it's that there was originally no slot for "uncategorized" at all.

Now there is. So what lies here is a bootstrapping sample, a set of rules not yet acknowledged, and a vacant policy slot.

The loop has turned another round, more slowly this time.

## In One Sentence

A tower has only a few floors, a loop has only one, and the floor is human language.
