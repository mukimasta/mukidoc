# Bootstrap System Design

Bootstrap is carried out by four cooperating parts: an entry point, a versioned resource bundle, a bootstrap executor and a result report. The entry point turns user intent into a target project and operation choices; the bundle defines the fixed directories, skeleton files, the full protocol and the version; the executor inspects the target and produces deterministic file changes; the result report lets humans and Agents judge the scope of completion and the follow-up choices.

### Resources and Plan

The fixed skeleton is driven by a resource manifest and is not inferred by the model on the fly. The bundle stores the full content of every file together with a consistency checksum, and before execution it verifies resource integrity and protocol version consistency. The exported protocol comes from the authoritative protocol maintained by the MukiDoc project; when the released content changes, the version must be raised, so that one version never stands for different rules.

The executor first inspects the type of every managed path, distinguishing missing directories, missing files, existing files and path conflicts. When a managed location turns out to be a symbolic link or a type mismatch, it reports a conflict and does not rewrite other locations by following the link. After inspection it forms a plan of what to create, preserve and replace; a preview returns only the plan.

Fixed directories may be empty, and are kept under version control with a placeholder marker. Existing files are not written by default; missing files are created from templates. Content outside the skeleton is not managed, and is not deleted just because its directory is not in the manifest.

### Protocol States

Protocol judgment uses both the version and a full content comparison:

| State | Default action | Condition for replacement |
|---|---|---|
| Missing | Install the built-in protocol | No overwrite needed |
| Content identical | Preserve | No update needed |
| Recognizable older version | Preserve and prompt for a version update | Explicit consent to update |
| Same version, different content | Preserve and point out the local differences | Explicit consent to full replacement |
| No unique version | Preserve, do not guess | Explicit consent to full replacement |
| Newer than the built-in version | Preserve | The current executor does not downgrade |

Versions are compared numerically. Version judgment applies only to the current resource bundle; it neither looks up nor claims a globally latest version.

### Replacement and Preservation

A protocol that needs confirmation may be preserved first while the rest of the skeleton is filled in normally. The entry point inspects the actual differences and obtains the user's decision; the authorization is tied to the content fingerprint of the file to be replaced. The fingerprint is checked again before execution, and if it has changed, replacement stops and the changes must be re-inspected.

Replacement first writes a uniquely named backup of the original file, then writes the complete new protocol to a temporary file, and finally replaces the target. The backup preserves the original bytes, and a new bootstrap must not overwrite an older backup. Explicit authorization is the caller's responsibility; the executor's explicit replace parameter means the caller has already completed confirmation, and the executor does not handle the conversation.

Creating directories and new files is not a global transaction. When an actual write hits an I/O error, it reports failure; the skeleton or backups already created may remain, and rerunning can continue filling in. A failure must not be described as success, nor rolled back automatically.

### Results and Scope

The result includes the bundle version, the target path, the lists of created and preserved items, the original protocol version and content fingerprint, the protocol action, whether a user decision is needed, and the actual backup location. Structure creation, protocol upgrade and knowledge migration are reported separately, and success of one does not stand in for completion of another.
