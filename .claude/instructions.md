# LLM Operating Instructions for This Project

You are helping build a custom Git-like version control system from scratch.
This is a learning-first, architecture-first, correctness-first project.

The goal is not only to "finish a clone," but to deeply understand Git internals,
data structures, algorithms, design trade-offs, and implementation patterns.

## 1) Project Scope and Mission

Primary goals:
- Learn Git internals thoroughly by implementing core behavior from first principles.
- Build a clean Python codebase that demonstrates strong architecture and code patterns.
- Track progress clearly so the project can be showcased as a learning artifact.
- Prepare for a future React visualization interface over Python-exposed state.

Out of scope for early phases:
- Full production parity with Git.
- Networking features before local object/ref/index fundamentals are solid.
- Optimizing prematurely over clarity.

## 2) Mandatory Learning Coverage

When planning and implementing, ensure coverage of concepts emphasized in:
- Write Yourself a Git (WYAG): init, objects, log, tree/checkout, refs, index, add/rm/commit.
- freeCodeCamp internals article: objects model, snapshots, branch/HEAD mechanics,
  staging/index mental model, plumbing-level understanding.

Treat these sources as conceptual baselines and checkpoints, not copy/paste templates.

## 3) Interaction Protocol (Strict)

Do NOT jump straight to full solutions.

For any non-trivial task, follow this loop:
1. Clarify objective with 2-5 targeted questions.
2. Propose 1-3 possible approaches with trade-offs.
3. Ask user to choose an approach.
4. Implement only the smallest next step.
5. Ask for confirmation before continuing to next step.

Required communication behavior:
- Be engaging, collaborative, and iterative.
- Prefer "question-first coaching" over "answer-dump mode."
- Explain decisions and alternatives before coding when there are trade-offs.
- Surface assumptions explicitly.

If user asks for immediate implementation, still provide a very short alignment check
question first, unless the task is trivial.

## 4) Engineering and Architecture Principles

Non-negotiable principles:
- Keep modules small, focused, and composable.
- Make data flow explicit; avoid hidden magic.
- Preserve deterministic behavior where possible.
- Document binary/text formats that are parsed or serialized.
- Use typed interfaces where practical.
- Prioritize readability over cleverness.
- Avoid global mutable state unless justified and documented.

Implementation policy:
- No high-level Git wrapper libraries for core internals.
- Re-implement core mechanisms manually in Python.
- If a temporary shortcut is used, mark it with:
  - Why it exists
  - Exit criteria
  - Planned replacement milestone

## 5) Project Evolution Rules

Every milestone must define:
- Objective
- Inputs/outputs
- Data structures used
- Algorithmic complexity notes
- Mapping to real Git behavior
- Known simplifications/deviations
- Tests added

Before extending scope, confirm:
- Existing milestone tests pass.
- Docs for current behavior are updated.
- Public interfaces are stable enough for extension.

No major refactor without:
- Reason for change
- Impacted modules
- Migration plan

## 6) File and Folder Structure Rules (Strict)

Use and evolve this baseline structure:

- `README.md` - project overview, roadmap, status.
- `.claude/instructions.md` - these model operating rules.
- `docs/`
  - `architecture/` - design notes and decisions.
  - `internals/` - object formats, index format, refs, DAG notes.
  - `milestones/` - per-milestone plans and completion notes.
- `src/rgit/`
  - `cli/` - CLI command wiring only.
  - `core/` - domain logic (objects, refs, index, graph, repo).
  - `storage/` - serialization/compression/fs persistence.
  - `services/` - orchestrations (status, add, commit flows).
  - `models/` - dataclasses/domain models.
  - `utils/` - small shared helpers.
- `tests/`
  - `unit/`
  - `integration/`
  - `fixtures/`

Folder constraints:
- Keep CLI parsing separate from domain logic.
- Keep filesystem IO separate from pure data transformations.
- Prefer one module responsibility per file.
- Avoid dumping unrelated logic into `utils`.

File naming rules:
- Python filenames must be `lower_with_underscores.py`.
- Test files: `test_<feature>.py`.
- No ambiguous names like `helpers.py`, `misc.py`, `temp.py`.

## 7) Coding Style Rules (Google Python Style Guide Aligned)

Follow Google Python Style Guide conventions for all new Python code.

Core rules to enforce:
- 4-space indentation, no tabs.
- Max line length target: 80 (use clean line breaks when needed).
- Meaningful names; avoid obscure abbreviations.
- Imports at top, grouped and sorted.
- Use docstrings for public/non-trivial modules, classes, and functions.
- Prefer explicit error handling; no broad `except:` unless justified.
- Avoid mutable default arguments.
- Avoid unnecessary global mutable state.
- Keep functions focused and reasonably short.
- Use type hints on public interfaces and non-trivial functions.
- Use context managers for files/resources.
- Keep comments high-signal (explain why, not what).

If style constraints conflict with existing code, improve consistency incrementally
and note deviations.

## 8) Command and Feature Progression

Default implementation order:
1. `init` and repository layout
2. loose object read/write (`hash-object`, `cat-file`)
3. commit object parsing + log graph walk
4. trees and checkout
5. refs, tags, branch/HEAD resolution
6. index read/write, status, ignore handling
7. add/rm/commit
8. merge strategy progression
9. performance/packfile explorations
10. visualization API for React frontend

Do not begin advanced features before proving correctness in preceding layers.

## 9) Testing and Verification Rules

For each feature:
- Add unit tests for pure logic.
- Add integration tests for filesystem/repository behavior.
- Include edge cases and malformed input tests for parsers.
- Compare behavior with real Git where feasible and document differences.

No feature is "done" without:
- Tests
- Minimal docs update
- Example usage

## 10) Required Response Format for Model Outputs

After any implementation step, report:
1. What changed
2. Why this design
3. What to test now
4. What edge cases remain
5. What the next smallest step is

When blocked or uncertain:
- Ask focused questions.
- Offer alternatives.
- Recommend the safest incremental path.
