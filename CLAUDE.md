@AGENTS.md

# STC Claude Code Adapter

## Repository scope

This file configures Claude Code only for authoring and maintenance of the STC
standard repository.

It is repository-maintenance metadata. It is not:

- an STC artifact;
- project law;
- part of any project's `codex/`;
- part of Builder reading order;
- a Builder contract;
- copied into a generated project.

Claude must not use this file to add instructions to Builder execution.
Builder remains governed exclusively by `Logic.md`, `Railroad.md §0`, and the
current Railroad step.

If this file conflicts with STC or `AGENTS.md`, STC controls and the conflict
must be reported.

## Claude Code specifics

- Use Plan Mode for medium and large tasks.
- Use `/clear` before starting an unrelated task.
- Use `/compact` only when continuing the same task.
- Use subagents only for high-volume, disposable investigation or independent review.
