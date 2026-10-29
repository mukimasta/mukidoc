# INFORMATION Design

Information holds the context and evidence that sit outside the formal design but are valuable for understanding, designing and verifying the project.

It sits alongside Project Context and is not part of it. The two are divided by nature rather than scope: Project Context is the project's own authoritative description, and Information is the material and evidence on which those descriptions rest. To decide which side an item belongs to, look at whether it has entered the project's formal description, regardless of when it was produced.

By the nature of the content there are four categories. These four category directories belong to the fixed skeleton and must be created and kept during bootstrap or migration, even when there is no material yet; the specific files inside are produced on demand. Git projects keep empty directories with `.gitkeep`:

```text
information/
├── raw_materials/
├── external_information/
├── investigations/
└── playground/
```

### Raw Materials

Holds original context produced by the project itself, such as early discussions, original requirements, historical inputs and existing material.

In principle it is kept as it was and not continually rewritten to fit the current design. Its value is to let future people or AI re-understand where the project first started from and what context it went through.

### External Information

Holds information obtained from outside the project.

It usually comes from original sources, excerpts, copied and organized material, or topical summaries produced by AI research. The source and the boundary between fact and inference should be preserved as far as possible.

This holds information provided by the outside world, not the project's own formal design conclusions.

### Investigations

Holds investigations and troubleshooting carried out during development on real problems.

When a bug, abnormal behavior, performance problem or other phenomenon takes a long process to understand, record the reproduction, the troubleshooting process, key findings, the root cause and necessary conclusions here.

The focus of an Investigation is to answer:

> What problem has already happened, and how did we finally figure it out?

This kind of information usually has strong historical value and can save future people from troubleshooting the same problem again.

### Playground

For actively exploring questions not yet settled, and for holding loose thinking that the formal categories cannot yet accommodate.

It can hold feasibility experiments, performance tests, algorithm verification, tool capability tests and other quick trials. Failures, temporary results and experiments with no conclusion are allowed, as are casual notes that produce no facts and serve no conclusion.

Playground answers:

> We do not know the result yet, so let us actively try and see what happens.

Or:

> This is somewhat interesting, but we do not yet know whether it counts as formal knowledge.

Investigation, by contrast, faces a real problem that has already appeared:

> The problem has happened, and now the cause must be found.

Content in Playground need not conform to the structural constraints of other formal documents and carries no responsibility for describing current state. It is a buffer between evidence and formal design.

If content of the same kind keeps accumulating, it has formed a genuine knowledge need, and a formal home should be considered for it rather than letting Playground grow without bound.
