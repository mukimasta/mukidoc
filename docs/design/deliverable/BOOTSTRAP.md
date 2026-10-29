# Bootstrap Design

Bootstrap establishes MukiDoc's fixed knowledge entry points for a new or existing project. Once the user names a target project, it provides the complete directory skeleton, the skeleton documents and a self-contained Agent protocol; project knowledge can then form in these places step by step.

### Bootstrap result

The root README.md and AGENTS.md, the seven Project Context documents under docs, and the directories for the three design-chain layers, the four Information categories and the four Evaluation commitment sources must all exist. A fixed document with no content yet keeps only its title, and empty directories must be preservable with the project. Areas, concrete design documents, Evaluation Suites and optional files are not pre-created; MukiCheck, which has not landed, is not part of bootstrap.

Existing files are kept as they are, including skeleton documents that exist but are empty. Repeated bootstrap only fills in what is missing; it does not rewrite bodies or clean up existing content. Bootstrap does not generate project facts, infer intent, or automatically turn existing code into design commitments.

### Usage

The user can request the skeleton through the bootstrap Skill, or run the same bootstrap program directly. Both entry points have identical file behavior. The Skill determines the target, explains the result and handles the protocol-update choice; the program performs the file operations reliably. Preview mode only shows the plan and does not change the project.

The bootstrap package is usable as a whole: it does not require the target project to have access to MukiDoc's source specifications, nor does it depend on downloading the current protocol from the network. The user can see which version the package provides, and what was actually created, preserved and still left to decide.

### Protocol version

AGENTS.md carries its own protocol version, and the bootstrap package has a version of its own. The two can evolve independently: a change in bootstrap behavior does not necessarily change the protocol, while a change in protocol rules requires raising the protocol version.

When the target has no AGENTS.md, the bundled protocol is installed. When the target is identical to the bundled protocol, it is kept; when an older version can be recognized, the user is asked whether to update. Same version with different content, no recognizable version, and a higher target version are each expressed separately, rather than all being treated as outdated.

Overwriting an existing protocol requires explicit authorization for that specific replacement. First explain the actual differences and their effect on project-specific rules, then let the user decide; when authorization is already explicit, do not ask again. After the replacement is confirmed, back up the original file in full, then write the bundled protocol. Declining or not confirming does not affect completing the rest of the skeleton. When the target version is higher than the bundled one, it is kept and not downgraded.

An update replaces the complete protocol by default and does not automatically merge project-specific rules. An early protocol without a version cannot have a version guessed from content similarity; after explicit confirmation it may be handled as a replacement. If the original file changes between review and execution, the actual differences must be re-checked, and unreviewed new content must not be overwritten.

### Boundary with migration

An existing project can have its structure completed, but classifying, rewriting, archiving and supplementing knowledge in old documents is migration. A protocol update likewise does not mean the project documents already conform to the new specification. A finished bootstrap only means that the fixed skeleton is established, existing content has been preserved, and the status of protocol installation or retention is clear.
