# MukiDoc

> 中文原版 / Chinese original: [mukidoc-zh](https://github.com/mukimasta/mukidoc-zh)

A documentation protocol for long-lived, complex projects: the project itself keeps its vision, decisions and design, so that humans and AI can keep collaborating.

AI is making code cheap; what stays scarce is a project's vision, decisions and direction. MukiDoc keeps them in the repo in layers, Design → System Design → Implementation: the higher the layer, the more it is designed by humans; the lower, the more it is handed to AI. The AI therefore holds a global view of the project, not scattered memories, and the protocol tells it where each kind of knowledge belongs, so the docs stay clear and tidy over time.

### How It Differs

1. **Memory systems** (e.g. Cline Memory Bank) let AI remember what happened; MukiDoc lets AI understand what the project is, why it is designed this way and where it stands now.
2. **Spec-driven development** (e.g. GitHub Spec Kit, Kiro) works feature by feature and prescribes a spec → plan → implement workflow; MukiDoc manages the long-term knowledge of the whole project, prescribes no fixed workflow, and only constrains what each kind of knowledge means, where it lives and how it relates.
3. **Convention files** such as AGENTS.md / CLAUDE.md usually record commands and code style; MukiDoc uses AGENTS.md as the protocol entry point and keeps project knowledge in the layered structure under `docs/`.

### Initializing a Project

The repository provides `skills/mukidoc-init/`, containing the initialization Skill, scripts and the complete protocol template. The first version of both the Skill and the protocol is **0.1.0**.

To run directly from this repository (requires Python 3.9+, no third-party dependencies):

```sh
python3 skills/mukidoc-init/scripts/init_mukidoc.py /path/to/project
```

Add `--dry-run` to preview. The script creates the fixed directories and skeleton documents and keeps existing content; if it finds an older AGENTS.md, it reports that an update is available and leaves the decision to the user. A confirmed update fully backs up the original protocol. Initialization only builds the structure; it does not fill in project knowledge or migrate old documents automatically.

You can also hand the whole `skills/mukidoc-init/` directory to an Agent that supports Skills and have it follow the [Skill description](skills/mukidoc-init/SKILL.md). The directory can be copied and used independently; this repository has no step for automatically installing a personal Skill.

### Learning and Developing

1. [Project overview](docs/OVERVIEW.md), [core philosophy](docs/PHILOSOPHY.md), [overall architecture](docs/ARCHITECTURE.md).
2. Initialization design chain: [Design](docs/design/deliverable/BOOTSTRAP.md) → [System Design](docs/system_design/BOOTSTRAP.md) → [Implementation](docs/implementation/BOOTSTRAP.md).
3. [Initialization evaluation and verification](docs/evaluation/design/bootstrap/EVALUATION.md), [development history](docs/DEVLOG.md).

Maintain the protocol and verify the resource bundle:

```sh
python3 scripts/sync_skill_assets.py --check
python3 -B -m unittest discover -s tests -v
```

When updating the protocol, first bump the version marker in the root AGENTS.md, then run `python3 scripts/sync_skill_assets.py` to export it to the Skill.
