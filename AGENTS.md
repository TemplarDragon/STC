# STC Authoring Contract

## Standing

This file governs only the authoring and maintenance of the STC standard and
STC contract documents.

It applies when the Architect:

- creates or corrects `Logic.md`;
- creates or corrects `Railroad.md`;
- synchronizes requirements, interfaces, acceptance criteria, and references;
- maintains the STC templates and standard documentation;
- reviews an unresolved `CONTRACT-GAP`.

This file does not govern Builder execution.

Builder is governed exclusively by `Logic.md`, `Railroad.md §0`, and the
current Railroad step. Builder must not load this file as an additional source
of construction instructions.

This file is repository-maintenance metadata. It is not:

- project law;
- a document in a project's `codex/`;
- a project input or output;
- a companion artifact;
- part of Builder reading order;
- copied into a generated project.

A tool-specific adapter that imports this file — `CLAUDE.md` — shares this
standing. It adds tool habits only: never a rule of its own, and never an
instruction to Builder execution.

## Authority boundary

Use only the authority model defined by STC.

This file does not create an additional authority hierarchy and does not change
the standing of any STC document.

In particular:

- `Specification.md` is an authoring input only;
- after the STC-defined freeze, `codex/Specification.md` is frozen in place and never edited again;
- after that freeze, `Specification.md` is not project law and is never
  consulted for building;
- `Logic.md` owns frozen project law;
- `Railroad.md §0` owns the Builder contract;
- the current Railroad step owns the immediate construction scope and its
  printed acceptance list;
- external knowledge and reference bases are reference only, never law.

If an instruction in this file conflicts with STC, STC controls and the
conflict must be reported.

## Authoring boundary

Before editing an STC contract document:

1. Identify the authoring outcome.
2. Identify which STC artifact owns the affected information.
3. Identify affected cross-references.
4. Check whether the proposed change alters project law, an interface,
   acceptance ownership, verification height, or Builder behavior.
5. Stop if the change requires an authority decision that has not been made.

Do not resolve a missing freeze decision in implementation code, DevLog,
comments, tests, or auxiliary documentation.

## Specification freeze

Never edit `Specification.md` after its STC-defined freeze.

A post-freeze change to project behavior, requirements, or interfaces must be
resolved in the owning section of `Logic.md`, including Appendix B where
applicable.

Apply the STC-required revision bump and Revision History entry. Synchronize
affected Railroad provisions through the STC authoring process.

Do not create or update a generic parallel specification.

## Acceptance authorship

Builder never authors acceptance criteria.

During authoring:

- place every criterion at the verification height required by STC;
- preserve the single chapter-gate observation defined by the standard;
- do not introduce step-local test files, fixtures, harnesses, or temporary
  verification scripts forbidden by the Railroad clauses;
- ensure that each Railroad step contains only criteria the Architect has
  authored and frozen.

This section governs authoring only. It creates no additional Builder
verification obligations.

## Authoring checks

Before closing an authoring change, check:

- ownership of each changed requirement;
- consistency between `Logic.md` and `Railroad.md`;
- traceability between project law and Railroad execution;
- compliance with STC verification-height clauses;
- acceptance authorship;
- normative file-tree consistency;
- section numbers and cross-references;
- required revision bump and Revision History entry;
- absence of new Builder obligations outside `Railroad.md §0`.

These are authoring consistency checks, not additional runtime verification
artifacts.

## DevLog boundary

`codex/DevLog.md` is never law, never a source of truth, and never a
substitute for a decision missing from the freeze.

Do not use DevLog:

- to establish or amend a requirement;
- to establish an interface decision;
- to repair a contract gap;
- as evidence for a V#;
- as a verification artifact.

Write to `codex/DevLog.md` only when an existing STC rule requires an entry.
This file creates no additional DevLog obligation.

## Failure boundary

This file defines no Builder retry or code-revision limit.

During construction, the applicable limit and response are defined exclusively
by `Railroad.md §0`.

An unresolved contract defect is a `CONTRACT-GAP`. Halt and return it to the
Architect. Do not replace that response with re-planning, a fresh session, or
another implementation attempt.

During authoring, stop when the gap cannot be resolved without an authority
decision.

## External reference boundary

External knowledge, skills, examples, and reference bases may inform
authoring, but they never become project law.

They do not:

- enter the STC authority hierarchy;
- override the freeze;
- override `Logic.md`;
- extend Builder reading order;
- create acceptance criteria;
- add project artifacts.

## Completion

An authoring change is complete only when:

1. The owning STC documents contain the decision.
2. Affected cross-references are synchronized.
3. No Builder obligation has been duplicated outside `Railroad.md §0`.
4. The verification-height and acceptance-authorship clauses remain intact.
5. The required standard or project revision has been applied.
6. Revision History has been updated.
7. Remaining `CONTRACT-GAP`s are reported explicitly.

Report:

1. Authoring outcome.
2. STC documents changed.
3. Consistency checks performed.
4. Revision applied.
5. Remaining contract gaps.
6. Whether the contract is ready for Builder.
