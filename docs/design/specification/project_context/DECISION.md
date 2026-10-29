# DECISION Design

DECISION supplements the record with the few key decisions in a project that deserve long-term preservation. What it keeps is not "what was finally chosen" (the conclusion can usually be seen directly in the current system) but what problem was faced at the time, how it would have been answered by default, and why that default was ultimately not adopted.

What truly deserves to be left behind is **where it is easy to think wrongly**. One question can serve as the test: if this entry is not written, will a future person follow intuition back onto the path we abandoned? If so, there is a real default answer and a real cost, and it should be recorded. If both options were simply viable and one was picked arbitrarily, then however complete the reasons are written, it only leaves behind a personal preference and does not belong in DECISION.

A decision suited to recording usually meets these conditions:

1. There is a natural default answer that most people would adopt directly.
2. We departed from that default, and the reason for departing cannot be easily re-derived.
3. It has lasting influence on the future, and the future may still need to understand why the choice was made.
4. Even if the decision is later overturned, the reasoning at the time remains valuable.
5. This thinking has no more natural home in another document. Conclusions and arguments that fit naturally into Design, System Design or Implementation should stay in the corresponding document first, and DECISION does not duplicate them.

Among arbitrary choices there is one exception: the choice itself has no better answer, but it bears load, because other documents, paths, tools or interfaces depend on it. What is recorded in this case is not a preference but a constraint, explaining why it cannot be changed casually, so that a future person does not treat it as something to fix in passing.

DECISION is appended continuously in chronological order as an ordered list, using a multi-level list if it is more complex. Each entry centers on one complete judgment, concisely recording the problem or background, the key thinking, the final decision and, where necessary, the main impact and scope of applicability, generally within 200 words per entry. The emphasis is on "why this decision was reached", not on describing in detail how it is implemented afterward.

Record only the judgment that actually existed when the decision was made. If the reasons at the time were weak, merely followed another choice, or there was no clear reason at all, write it as it was; do not retroactively supply a more self-consistent explanation to make it look complete. An invented reason is more dangerous than an empty one, because it makes later people stop asking.

Ordinary implementation choices, temporary adjustments, development running-accounts, and plans that have not yet happened do not belong in DECISION.

When an existing decision is overturned, do not modify the original record; append a new decision and record what new fact or judgment drove the change, so the document preserves how the project's understanding evolved. When appending, state which entry it overturns or affects, so that someone reading in time order can judge whether the old record still holds.
