# RGit - Build Git From First Principles

`RGit` is an educational, Git-like version control system implemented in Python.
The mission is to deeply understand Git internals by building core behavior from
scratch with clear architecture, clear documentation, and testable milestones.

## Vision

This project is designed to do two things at once:

1. Build a working Git-like system step-by-step.
2. Capture the learning process in a way that is explainable and showcase-ready.

The emphasis is on internals, algorithms, data structures, architecture, and
engineering discipline, not feature velocity.

## Core Objectives

- Learn and implement Git fundamentals (objects, refs, index, history, checkout).
- Build strong intuition for data structures and algorithmic trade-offs.
- Develop clean Python architecture with explicit module boundaries.
- Compare each implemented behavior against real Git semantics.
- Prepare a future React UI layer to visualize internals (DAG, objects, refs).

## Learning Sources (Mandatory Coverage)

This project intentionally tracks concepts from:

- [Write Yourself a Git](https://wyag.thb.lt/)
- [A Visual Guide to Git Internals (freeCodeCamp)](https://www.freecodecamp.org/news/git-internals-objects-branches-create-repo/)
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)

These are treated as conceptual baselines, not copy/paste templates.

## Scope

### In Scope

- Local repository internals from init to commit workflows.
- Object model (`blob`, `tree`, `commit`, optional `tag`) and object database.
- Reference resolution (`HEAD`, branches, tags).
- Index/staging mechanics and working tree comparisons.
- Commit graph traversal and history reasoning.
- Test-driven milestone implementation.

### Out of Scope (Early Phases)

- Full Git parity.
- Distributed/network commands (`fetch`, `push`, `pull`) before local core is stable.
- Performance optimization before correctness and clarity are validated.

## Project Principles

- **Learning-first:** understand before abstracting.
- **Small increments:** one validated step at a time.
- **Architecture-first:** separate parsing, domain logic, storage, and orchestration.
- **Correctness-first:** tests and docs are required for "done."
- **Transparency:** all simplifications vs real Git are explicitly documented.

## Proposed Repository Structure

```text
.
|- .claude/
|  |- instructions.md
|- docs/
|  |- architecture/
|  |- internals/
|  |- milestones/
|- src/
|  |- rgit/
|     |- cli/
|     |- core/
|     |- storage/
|     |- services/
|     |- models/
|     |- utils/
|- tests/
|  |- unit/
|  |- integration/
|  |- fixtures/
|- README.md
```

## Architecture Rules

- CLI layer only parses commands and delegates.
- Core/domain layer contains object/ref/index logic.
- Storage layer handles filesystem, serialization, compression.
- Services orchestrate multi-step flows (`status`, `add`, `commit`).
- Models represent typed domain data.
- Utilities stay minimal and generic; no "misc dumping."

## Coding Standards

Python code follows Google Python Style Guide conventions for:

- naming, imports, and formatting;
- docstrings and comments;
- explicit error handling;
- type hints on public/non-trivial interfaces;
- context managers for file/resource handling;
- no mutable default args;
- no broad catch-all exceptions without justification.

## Milestone Plan

1. Repository initialization and `.git`-like directory layout.
2. Loose object read/write (`hash-object`, `cat-file`).
3. Commit parsing and history traversal (`log`).
4. Trees and checkout behavior.
5. Refs, tags, branch naming, `HEAD` resolution.
6. Index read/write and status-like comparisons.
7. Add/remove/commit workflows.
8. Merge strategy progression (basic to three-way).
9. Packfile/performance exploration (optional advanced layer).
10. Visualization API and React integration.

## Milestone Completion Criteria

Each milestone is complete only when it has:

- a clear objective and boundaries;
- implementation with documented data structures;
- complexity notes and trade-offs;
- tests (unit + integration where relevant);
- docs that explain behavior and known differences from real Git.

## Development Workflow

- Work in small, reviewable increments.
- Prefer design discussion before major implementation changes.
- Ask clarifying questions before coding when requirements are ambiguous.
- Document assumptions and decisions in `docs/architecture/`.
- Record milestone progress in `docs/milestones/`.

## Quality Gates

Before expanding scope:

- existing tests pass;
- behavior is documented;
- public interfaces are stable enough;
- known deviations from Git are tracked.

## Current Status

Project setup and governance definition in progress.

### Next Suggested Step

Scaffold the Python package layout and implement `init` as the first executable
milestone with tests and docs.
