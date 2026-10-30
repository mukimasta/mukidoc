# Bootstrap Implementation

The current bootstrap deliverable is `skills/mukidoc-init/` in the repository; both the Skill version and the protocol version are `0.2.0`. The runtime program uses only the Python 3.9+ standard library, with no third-party runtime dependencies; this repository stores the source files and does not install them automatically into a personal Skill directory.

### Code and Resources

1. `skills/mukidoc-init/SKILL.md` defines the trigger scope, the run entry point, result interpretation and user confirmation rules; `agents/openai.yaml` provides display metadata.
2. `skills/mukidoc-init/scripts/init_mukidoc.py` provides the only bootstrap implementation, shared by the Skill and the command line.
3. `skills/mukidoc-init/assets/manifest.json` stores the schema version, Skill version, protocol version, all fixed directories and the SHA-256 of the template files.
4. `skills/mukidoc-init/assets/template/` stores the full AGENTS.md and eight skeleton documents containing only a title. The templates contain no knowledge from the current MukiDoc project.
5. The root `AGENTS.md` is the maintained authoritative protocol; `scripts/sync_skill_assets.py` exports it verbatim into the Skill and updates the template checksums; the target project does not depend on this export script or the source repository at runtime.

### Commands and Output

```sh
python3 skills/mukidoc-init/scripts/init_mukidoc.py /path/to/project
python3 skills/mukidoc-init/scripts/init_mukidoc.py /path/to/project --dry-run
```

The target path may not exist yet, and may contain spaces and Chinese characters. By default it fills in 9 files and 14 directories; the 11 leaf directories, when empty, get a `.gitkeep`, and `git init` is not required to have been run. A directory that already has content gets no marker added. An existing file is preserved as is, even when empty.

The version marker is `<!-- MukiDoc protocol version: 0.2.0 -->`; only a single three-part numeric version is recognized, compared as a numeric tuple. `agent.state` returns `missing`, `current`, `older`, `unversioned`, `same_version_modified` or `newer`. The marker is for compatibility recognition and is not authentication of the file's origin.

After confirming an older-version update, pass `--update-agent --expected-agent-sha256 HASH`; after confirming a full replacement of an unversioned or same-version-modified file, pass `--replace-agent --expected-agent-sha256 HASH`. HASH must come from the report at review time. Replacement is refused when the target is a newer version. The backup is saved in the target root as `AGENTS.md.bak.<UTC timestamp>.<random suffix>`, preserving the original bytes and permissions; the temporary file replaces the target via `os.replace`.

The program outputs JSON, containing the plan or actual file list, the version judgment, the state needing confirmation and the backup path. Normal completion returns 0; preserving a protocol that awaits confirmation still returns 0, with the status `initialized_agent_preserved`, which does not mean the protocol has been updated. `--dry-run` returns the planned status without creating the target directory. Execution errors return 1, and argument errors are returned by the command-line parser as 2.

Manifest verification and path-conflict checks complete before any writes; new files are created exclusively to prevent overwriting. The content fingerprint is checked before protocol replacement and again just before the replacing action. After an I/O failure there may be some new files or a backup; there is no project-wide transactional rollback, and no locking guarantee is provided against concurrent writing processes.

### Version Maintenance

When changing the protocol, first edit the root AGENTS.md and raise the version marker, then run:

```sh
python3 scripts/sync_skill_assets.py
python3 scripts/sync_skill_assets.py --check
```

If the content of an already packaged protocol changes without a version bump, the exporter refuses to sync. When the script or skeleton templates change, update the Skill version in the manifest and SKILL.md; a change to the executor alone does not require raising the protocol version. Template checksums are recomputed by the exporter. The bootstrap package version and the protocol version are conceptually separate and do not depend on being released under the same number.

### Verification

```sh
python3 -B -m unittest discover -s tests -v
python3 scripts/sync_skill_assets.py --check
```

`tests/test_bootstrap.py` verifies in a temporary directory the complete skeleton, repeated runs, preservation of existing files, version judgment, explicit update and backup, stale fingerprints, preview and path conflicts, and also verifies that the Skill still runs when detached from the source repository. The Skill format is separately checked with the Skill Creator's `quick_validate.py`. The concrete evaluation commitments and this round's evidence are kept in `mukidoc/evaluation/design/bootstrap/EVALUATION.md`.
