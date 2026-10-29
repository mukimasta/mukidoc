# Global View Evaluation

### Claim

An AI that has a project's upper-layer documents (PHILOSOPHY, Design, System Design and DECISION) makes judgments that fit the project's intent better than an AI that sees only the code and the current conversation: its changes land in the right layer, do not contradict recorded decisions, and update the affected documents in the right places.

### Scope

System / End-to-End. Real or near-real project changes, comparing the same model with and without MukiDoc's upper-layer documents. Code style and single-shot generation speed are not evaluated.

### Method

Pick projects that already use MukiDoc and prepare a set of change tasks that can only be done correctly by understanding the design intent, including requests that conflict with recorded decisions. The same model completes each task under two conditions: the full MukiDoc documentation; and with the upper-layer documents under docs/ removed, keeping only the code and minimal instructions. The Human grades the results blind.

### Metric / Oracle

1. Whether the change fits the intent in PHILOSOPHY and Design, and whether, on conflict, it points out the contradiction with a recorded decision instead of silently overriding it.
2. Whether the problem is located at the right layer.
3. Whether the affected documents are updated in the right places, without duplicate or contradictory descriptions.

### Current Status

Unverified. There is only informal evidence so far: on 2026-09-15, after MukiDoc was applied to an existing project, the AI-rewritten documents were clearly better than the original structure; and during the Alibaba internship, one person built a system in two months while keeping context with this method. This shows the method is usable, but does not prove the Claim.
