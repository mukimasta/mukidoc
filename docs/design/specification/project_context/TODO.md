# TODO Design

TODO records the concrete items the project has currently decided to do, keeping only the current action surface. TODO.md belongs to the fixed skeleton: even with nothing to do, the file and its title are kept and no tasks are invented; after all items are done, this entry point is still kept.

The format stays simple:

```markdown
# TODO

- [ ] ...
- [ ] ...
- [ ] ...

### Waiting

- [ ] ... — waiting on some prerequisite
```

TODO should satisfy:

1. Each item is a clear, executable action, starting with a verb where possible.
2. By default, items are ordered by priority from top to bottom, with no further Now / Next distinction.
3. Items that have been decided but cannot currently proceed go under `Waiting`.
4. Long-term direction belongs in ROADMAP.
5. Delete items directly once done and keep no history; what has happened is recorded by DEVLOG.
6. Keep it short; do not expand background, design or discussion in TODO.

A good TODO lets anyone entering the project at any time know immediately what the project most needs next, without digging through code and history.
