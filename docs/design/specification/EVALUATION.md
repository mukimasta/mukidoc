# EVALUATION Design

Evaluation judges whether the commitments a project makes at different layers actually hold, and feeds the results back to the corresponding layers to drive later iteration.

Evaluation's core principle is:

**Designed top-down, executed bottom-up.**

When designing Evaluation, start from upper-level commitments and turn abstract goals step by step into properties that can be observed and judged. Evaluation targets typically come from:

**PHILOSOPHY → Design → System Design → Implementation**

The higher the layer, the more it concerns final value and core commitments; the lower, the closer to concrete behavior, engineering constraints and specification conformance. This avoids evaluating only "what is easy to test" while neglecting the goals that matter most.

In actual execution one starts from the low layers. First verify cheap, deterministic, local properties, then move on to Integration, System and higher-level commitments. Low-layer results both provide evidence for high-layer judgments and help locate the problem when a high-layer Evaluation fails.

Evaluation is organized by commitment source. `evaluation/` and the four commitment-source directories `philosophy/`, `design/`, `system_design/` and `implementation/` belong to the fixed skeleton and must be created even when there is no evaluation yet; in Git projects empty directories are kept with `.gitkeep`. A concrete Evaluation Suite is created once an evaluation topic takes shape. MukiCheck has not landed; the current bootstrap skeleton does not require creating `mukicheck/`, and the diagram below keeps its designed position:

```text
evaluation/
├── mukicheck/
├── philosophy/
├── design/
├── system_design/
└── implementation/
```

`mukicheck/` holds MukiCheck, the standard evaluation shipped with every MukiDoc project, used to judge whether the project's knowledge system is healthy, consistent with the code, and still able to support an unfamiliar Agent taking over; the rest holds the concrete project's own Evaluation.

### Evaluation Suite

Each independent evaluation topic gets one Evaluation Suite:

```text
<layer>/
└── <evaluation_name>/
    ├── EVALUATION.md
    └── ...
```

`EVALUATION.md` defines at least:

1. Claim: which commitment is being verified.
2. Scope: how wide the evaluation covers.
3. Method: by what means evidence is obtained.
4. Metric / Oracle: how results are judged.

A complex Suite can be split further into different Scopes or evaluation scenarios; a simple one can stay a single file.

### Evaluation Scope

The layer where a commitment lives and the scope an evaluation covers are two independent dimensions.

The same Claim can be verified under different Scopes:

**Module → Integration → System / End-to-End → Long-term**

High-level commitments can also be supported by low-level evidence, and low-level problems may only surface within a larger system scope.

Split further only when different evaluation scopes genuinely exist; do not add levels artificially for structural completeness.

### Evaluation and execution

`docs/evaluation/` holds evaluation goals, methods and criteria; the execution code need not live alongside the documents.

What actually produces evidence should sit in the most natural engineering location, which can be tests, evals, benchmarks, scripts, CI, an Agent task, human evaluation or real-use results.

Evaluation defines "why test, what to test, and how to judge"; the concrete tools produce the evidence.

### Differences from Playground and Tests

`information/playground/` is for exploring questions not yet settled, and can hold thinking, drafts, experiments, failed results and knowledge that temporarily has no formal home.

The project's `tests/` check behaviors and implementation constraints that are already clear, and can usually be run repeatedly with definite results.

Evaluation combines Tests, experiments, run results and other evidence to judge whether the project's commitments actually hold.

Put simply:

**Playground is for exploring, Tests are for checking, Evaluation is for judging.**

Evaluation should grow together with the project's design. When a new important commitment forms, consider how it will eventually be verified; when an evaluation exposes a problem, feed the result back to the layer that actually needs adjusting.
