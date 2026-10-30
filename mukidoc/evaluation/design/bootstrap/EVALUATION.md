# Bootstrap Evaluation

### Claim

Bootstrap deterministically establishes the fixed skeleton and preserves existing project content; protocol differences are classified accurately, replacement happens only through an explicit choice, and a recoverable copy of the original file is kept. The standalone-distributed Skill does not depend on the MukiDoc source repository.

### Scope

Covers local file bootstrap, version comparison, backup and replacement, resource bundle integrity and standalone script execution. It does not verify old-document migration or real business operation, and does not treat program-parameter tests as evidence that an Agent correctly asks the user in conversation.

### Method

Run the real commands in an isolated temporary project, compare the complete file contents before and after the operation, and check the fixed directories, skeleton documents and the optional items that were not created. Construct older-version, same-version-modified, unversioned and newer-version protocols, covering default preservation and explicit replacement. Copy the whole Skill to a separate location and run it again. Resource export consistency and Skill structure are checked separately.

### Oracle

1. A new project has the complete fixed skeleton, with no optional empty documents or MukiCheck; AGENTS.md is byte-identical to the built-in protocol.
2. Repeated runs do not modify existing files, including user content and empty documents; a missing skeleton is filled in.
3. An existing protocol is not overwritten by default, and version and content states are distinguished correctly; downgrading from a future version is refused.
4. An explicit update keeps a complete backup of the old file and leaves other documents unchanged; replacement is refused if the original file has changed since review.
5. Preview writes nothing; path conflicts and a corrupted resource bundle raise errors before any write, and nothing can be written elsewhere through a managed symbolic link.
6. A standalone Skill directory can run bootstrap, without runtime dependencies on the source repository.

### Evidence This Round

On 2026-09-25, Skill 0.1.0 / protocol 0.1.0 ran `python3 -B -m unittest discover -s tests -v` in a local temporary directory, and all 18 tests passed. They cover first and repeated bootstrap, partially existing projects, preview without writes, the six protocol states, numeric version comparison, backup and replacement, stale content fingerprints, refusing downgrade, path type conflicts, managed symbolic links, resource corruption, and running a standalone Skill copy. Preservation of existing files was checked by bytes and modification time; backups were compared by bytes.

`scripts/sync_skill_assets.py --check` passed, with the root protocol, the packaged protocol and all template checksums consistent. The Skill Creator's `quick_validate.py` passed; the default Python on this machine lacks the PyYAML that the validator depends on, so the validator was run in a temporary uv environment, while the bootstrap script itself still uses only the standard library.

The behavior of the Skill in a real conversation, discovering an older protocol, showing the actual differences and waiting for the user's choice, still needs independent verification. This round did not install a personal Skill, modify an external project or perform a document migration.
