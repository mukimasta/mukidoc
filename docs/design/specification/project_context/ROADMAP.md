# ROADMAP Design

ROADMAP describes the main stages of the project's long-term development and how these stages step by step bring the project to its final goal. It concerns the evolution of the project's capability and maturity, and does not maintain current progress.

ROADMAP should stay relatively static. Modify it only when the overall development path changes; what was actually completed and what happened during development are recorded continuously by DEVLOG.

Stages should be divided by **qualitative shifts in capability or maturity**, not by features, components, tasks or version names. On completing each stage, the project should gain an important capability it did not have before, and that naturally becomes the foundation for the next stage.

Each stage mainly states:

1. The core problem this stage is to solve.
2. What new capability or state the project gains after this stage.
3. Why this change can carry the project into the next stage.

The stages should form a clear progression. From the stage titles alone, one should be able to roughly understand how the project develops and matures; if stages could be reordered at will without affecting the logic, they are more likely a task list than a Roadmap.

A good stage division usually looks like:

`Methodology → Specification → Agent Workflow → Tooling → Validation → Reusable System`

From the titles alone one sees the project's evolution from forming a method, to becoming executable and automatable, to being validated in reality, and finally to becoming a reusable system.

Bad stage divisions commonly come in several kinds:

`Documentation → CLI → Plugin → Website → Demo → Release`

This divides by the products to build; it is essentially a list of features or deliverables, with no clear capability progression among the stages.

`Frontend → Backend → Database → API → Deployment → Monitoring`

This divides by system module or engineering domain; it is more like a work breakdown structure than a path of project maturity.

`Prototype → MVP → Alpha → Beta → Release → Future`

This divides by version name. The titles themselves give almost no sense of what qualitative shift the project undergoes, and one cannot see why each stage must exist.

`Q1 → Q2 → Q3 → Q4`

This slices by time; it describes scheduling, not how the project's capability evolves.

To judge whether a stage division is sound, try removing the concrete tasks and time information and look only at the stage names and stage results. Only if one can still see how the project gains new capability step by step, and each later stage clearly depends on the previous one, is it closer to a true Roadmap.

The format is fixed:

`# Roadmap`

Open with a short paragraph summarizing what state the whole route ultimately hopes to bring the project to.

Each stage uses a numbered level-2 heading:

`## 1. Stage Name`

`## 2. Stage Name`

`## 3. Stage Name`

Each stage uses 1–3 natural paragraphs, focusing on the stage's problem, the capability change and the push toward the next stage, without expanding on concrete tasks and implementation detail.

The last stage describes the complete state the project ultimately hopes to reach, giving the whole route a clear end point.

The number of stages is usually kept to 4–8; if a complex project cannot be explained at a single level, two levels may be used as appropriate. The whole text is no more than 2000 words.
