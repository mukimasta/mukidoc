---
name: mukidoc-init
description: Bootstrap or complete a project's fixed MukiDoc directories and skeleton documents, install the bundled AGENTS.md, and detect older protocol versions so the user can decide whether to update. Use when the user asks to bootstrap, adopt, or complete the MukiDoc skeleton, or to update the MukiDoc protocol; it does not rewrite project knowledge, migrate old documents, or handle day-to-day development.
metadata:
  version: "0.1.0"
---

# MukiDoc Init

Build the structure with the bundled script. Do not have the model regenerate AGENTS.md or invent a separate bootstrap routine. This Skill, its script and its assets can be copied as a unit and do not depend on the MukiDoc source repository or any online service. Requires Python 3.9 or newer; no third-party runtime dependencies.

## Bootstrap

1. Determine the target project directory from the user's request; when the user means the current project, use the current working directory. If the target is still ambiguous, clarify first, and never mistake the Skill's install directory for the project directory.
2. Locate `scripts/init_mukidoc.py` next to this SKILL.md and call it with the absolute target path:

   ```sh
   python3 /absolute/path/to/mukidoc-init/scripts/init_mukidoc.py /absolute/path/to/project
   ```

   If the user only wants a preview, add `--dry-run`; nothing is bootstrapped. Quote paths that contain spaces.
3. Read the script's JSON result and report what was created, preserved, and still needs a decision. If the script fails, diagnose the actual error; do not work around the safeguards with an overwriting write. An I/O error may leave a partially created skeleton or a backup, so never claim an automatic rollback.

The script creates the fixed directories and skeleton documents, puts `.gitkeep` in empty directories, gives skeleton documents only a title, and copies the complete AGENTS.md template. Existing documents and code are preserved. It does not write product facts, create optional documents, Areas, Evaluation Suites or MukiCheck, and it does not migrate documents.

## Protocol version and updates

`assets/manifest.json` holds the Skill version, protocol version, skeleton manifest and template checksum; the complete protocol is in `assets/template/AGENTS.md`. The comparison is against the version shipped with this Skill, not the latest version on the internet.

By default the script only fills in what is missing, and an existing AGENTS.md is left untouched. Handle it according to `agent.state` in the result:

| State | Behavior |
|---|---|
| `missing` | The bundled protocol is copied in this run; dry-run only previews |
| `current` | Version and full content match; keep it and do not ask about updating |
| `older` | Explain the old and bundled versions, and ask whether to update |
| `same_version_modified` | Same version but different content; keep it, explain the differences, and do not call it outdated |
| `unversioned` | No single recognizable version, including early protocols without a version marker; keep it and do not guess a version |
| `newer` | Keep the higher version and do not downgrade; a newer Skill is needed to provide that version |

When a replacement is needed, first read the differences between the target AGENTS.md and the bundled template, briefly describe what would actually change, and point out any project-specific rules the replacement would affect. The default update installs the complete bundled protocol and does not semantically merge. Tell the user the original file will be backed up in full and ask whether to replace it; if the user has already explicitly authorized this replacement, proceed without asking again. If the user declines or does not answer, keep the original file; the skeleton completion remains valid.

After an older version is confirmed, use `--update-agent`; after an unversioned or same-version-modified file is explicitly confirmed for replacement, use `--replace-agent`. Both must carry the original file's `agent.sha256` from the review report:

```sh
python3 /absolute/path/to/mukidoc-init/scripts/init_mukidoc.py /absolute/path/to/project --update-agent --expected-agent-sha256 ORIGINAL_SHA256
```

"Bootstrap the project" is not by itself authorization to overwrite an existing AGENTS.md. If the file changed after the review, re-check the actual differences; do not simply take the new hash to get past the check. The script saves an `AGENTS.md.bak.*` with a timestamp and unique suffix in the target root, then replaces the protocol. When done, report the actual old version, new version and backup path; a replacement only updates the protocol and does not mean the project documents have been migrated or conform to the new specification.

## Completion boundary

Bootstrap is complete when the fixed skeleton exists, existing content is preserved, and the protocol outcome is clear. Bodies may contain only titles; when AGENTS.md is kept, state whether an update is still pending the user's decision. Do not describe a complete skeleton as complete project knowledge, a verified running system, or migrated old documents.
