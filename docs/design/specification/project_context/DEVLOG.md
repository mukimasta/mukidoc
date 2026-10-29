# DEVLOG Design

DEVLOG is the project-level development timeline, continuously appended in chronological order. It records how the project actually got to where it is, so that future people or AI can quickly see what important things happened during development, what problems were met, and where the project took clear turns.

It concerns the whole project, not the complete technical process inside a single module. One round of development may change many modules, but DEVLOG keeps only the parts worth entering the project's main timeline.

Typically worth recording:

* A key new capability or milestone result was completed.
* An important problem arose that affected progress.
* Actual development or testing exposed previously unknown facts, limits or risks.
* An existing approach was clearly adjusted because of real-world feedback.
* A debugging session ultimately exposed a deeper system problem.
* Evaluation produced an important result that affects later development.
* The project's implementation direction, development focus or next stage changed as a result.

DEVLOG need not record all work. Ordinary file edits, simple refactors, small bugs, dependency upgrades, mechanical development steps, and changes Git already expresses fully need not be saved again.

### Format

DEVLOG is appended by date; after each round of development, record what is truly worth entering the project's history from that round.

The format is fixed:

```markdown
### YYYY-MM-DD

1. ...
2. ...
3. ...
```

Content from the same day goes under the same date as an ordered list. Each entry is usually 1–3 sentences, first saying what happened; if the cause, finding or impact is important for understanding it, write that in as well.

A good record lets someone who did not take part in that day's development understand why this was worth remembering.

For example:

```markdown
### 2026-09-14

1. Completed the first version of the upload pipeline and got large-file upload working. Real testing showed that routing files through the application server holds connections and bandwidth for a long time, so it was changed to direct client upload to object storage.
2. Resumable-upload testing found that client state cannot be reliably restored after a browser refresh, so upload state is now maintained by the server. This also confirmed that client-side progress cannot be the only source of truth.
3. The upload flow is basically stable; the next stage can start on failure recovery and cleanup.
```

This kind of record preserves results, real-world feedback and the changes the project underwent because of them.

A bad record looks more like:

```markdown
### 2026-09-14

1. Added UploadController.
2. Modified UploadService.
3. Added 3 APIs.
4. Fixed an upload bug.
5. Tests pass.
```

Git and the code already express this content, and it cannot tell a future reader why these changes mattered.

Another bad record is an overly detailed debug log. If a problem takes several hundred words to explain, put the full process in the corresponding information document, and leave in DEVLOG only the outcome it had for the project's main line.

### Historical nature

DEVLOG is, in general, append-only, and the past is not rewritten to match the current state. When a past understanding is later overturned, keep recording the change under a new date, so the timeline itself preserves how the project's understanding and implementation evolved.

It also does not carry the current-state description. What the current system looks like should be described by the corresponding formal documents; DEVLOG explains how it got here step by step.

It likewise records only what has already happened, and does not arrange plans, priorities or next tasks not yet executed: those belong in TODO, and long-term direction belongs in ROADMAP. When describing the significance of a completed result, it may say that it unlocked or changed the next stage, but that explains what happened and does not schedule future work in DEVLOG.

A good DEVLOG need not record much, but reading along its dates should quickly show the key results, problems, findings and turning points the project has been through.
