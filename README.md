# MukiDoc

> 中文原版 / Chinese original: [mukidoc-zh](https://github.com/mukimasta/mukidoc-zh)

**A structured documentation protocol designed for large projects.**

MukiDoc uses structured documents to keep a project's high-level context, such as its philosophy, architecture and roadmap, together with the core design-chain documents across three layers: Design → System Design → Implementation. The MukiDoc protocol gives these documents a clear structure; following it, AI grasps the project as a whole and maintains the documents as it writes code, keeping them clear, elegant and tidy.

### Initializing a Project

The repository provides `skills/mukidoc-init/`, containing the initialization Skill, scripts and the complete protocol template. The current version of both the Skill and the protocol is **0.2.0**.

To run directly from this repository (requires Python 3.9+, no third-party dependencies):

```sh
python3 skills/mukidoc-init/scripts/init_mukidoc.py /path/to/project
```

Add `--dry-run` to preview. The script creates the fixed directories and skeleton documents and keeps existing content; if it finds an older AGENTS.md, it reports that an update is available and leaves the decision to the user. A confirmed update fully backs up the original protocol. Initialization only builds the structure; it does not fill in project knowledge or migrate old documents automatically.

You can also hand the whole `skills/mukidoc-init/` directory to an Agent that supports Skills and have it follow the [Skill description](skills/mukidoc-init/SKILL.md). The directory can be copied and used independently; this repository has no step for automatically installing a personal Skill.

### Learning and Developing

1. [Project overview](mukidoc/OVERVIEW.md), [core philosophy](mukidoc/PHILOSOPHY.md), [overall architecture](mukidoc/ARCHITECTURE.md).
2. Initialization design chain: [Design](mukidoc/design/deliverable/BOOTSTRAP.md) → [System Design](mukidoc/system_design/BOOTSTRAP.md) → [Implementation](mukidoc/implementation/BOOTSTRAP.md).
3. [Initialization evaluation and verification](mukidoc/evaluation/design/bootstrap/EVALUATION.md), [development history](mukidoc/DEVLOG.md).

Maintain the protocol and verify the resource bundle:

```sh
python3 scripts/sync_skill_assets.py --check
python3 -B -m unittest discover -s tests -v
```

When updating the protocol, first bump the version marker in the root AGENTS.md, then run `python3 scripts/sync_skill_assets.py` to export it to the Skill.
