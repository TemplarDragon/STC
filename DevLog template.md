# `<PROJECT NAME>` — Dev Log

> **[STC template — delete this callout before use.]** The Builder's own notebook. Every other document in this project is **read-only law** for the Builder (`Railroad.md` §0); this is the one file it writes freely. Keep it short, append-only, and honest — including about what went wrong.

**Lives here:** in the **built project's** repository, at `manuals/DevLog.md` — *not* in the design workspace. Its entire job is continuity across sessions and machines, so it has to travel in the same repository as the code it describes. If the design documents live in a separate repo, this file does not follow them there.

**Written by:** the Builder, every session, without being asked. **Read by:** the next session (whoever or whatever it is), and the Architect. **Never** cited as a reason for anything.

---

## The four rules that keep this from becoming a second standard

These are not stylistic. A journal that accumulates authority is worse than no journal, because it produces a project whose real specification is spread across a log nobody froze.

1. **It is never law, and never a source of truth.** No step is ever justified by "the Dev Log says". If something written here turns out to matter — a constraint discovered, an assumption that proved false — it is **promoted** by the Architect into `Logic.md` (as an amendment) or into `Railroad.md` (as a step), and only then does it bind anything. Until promoted, it is a note.
2. **It never holds a decision the freeze failed to make.** That is a `CONTRACT-GAP`, and the reaction is to HALT and report it (rail 4) — not to write the missing decision down here and carry on. This file may record **that** a gap was raised and how it was resolved *upstream*; it may never *be* the resolution. The same applies to an `STC-GAP`: it is recorded in `Logic.md` §14, and this file may only point at it.
3. **It is not a verification artifact.** It never replaces the printed ✓/✗ checklist a step closes on (§0.3), never contains a test, and never becomes the evidence for a `V#`. A one-line "step 2.3 closed, checklist green" is a diary entry; the checklist itself was the deliverable.
4. **The next session loads the tail, not the file.** Read the **latest handoff block plus the open queue** — nothing older. The reading order in `Railroad.md` §0 exists to keep a step's context bounded, and a growing log is exactly the kind of thing that quietly unbounds it. Which is why the log is compacted at every chapter gate (below).

---

## What goes in, and what does not

| Goes in | Does not |
|---|---|
| what was actually done this session, per step number | anything the step's own checklist already proves |
| what broke, what was tried, what the fix was | a decision that belongs in `Logic.md` |
| environment quirks, per machine (a path that differs, a tool version, a permission) | credentials, tokens, personal data — ever |
| gaps raised, with a pointer to where they were resolved | the resolution itself |
| what is half-finished and what state the tree is in | speculation about future architecture |
| what is queued, and why it is queued rather than done | a queued *design* choice (that is a gap, not a queue item) |

> **On queuing.** A queue item is always *work*, never *a decision*. "Retry the flaky install on the laptop" is a queue item. "Decide whether the retry limit is 3 or 5" is a `CONTRACT-GAP`, because rail 6 says an unpinned parameter is a defect. If you cannot tell which one you are writing, it is the second one.

---

## Session entries — newest at the bottom, append-only

`<One block per session. Keep each to a handful of lines; if a session needs an essay, most of it belongs in a gap report or in a step's completion note.>`

### `<YYYY-MM-DD>` · `<machine label>` · steps `<N.M – N.M>`

- **Done:** `<step N.M — one line each, referring to the step number, not re-describing it>`
- **Problems:** `<what failed, what it turned out to be, what fixed it. "Still unexplained" is a valid and useful entry.>`
- **Gaps raised:** `<CONTRACT-GAP / STC-GAP → where it was resolved (Logic A-bump §x, Logic §14, still open)>`
- **Queued:** `<work deferred, and why now was the wrong time for it>`
- **Handoff:** `<the state of the tree at the moment you stopped: what builds, what boots, which stubs are still standing, what the very next action is. Write this as if the next session is on a different machine and cannot ask you anything — because that is the case this file exists for.>`

---

## Open queue

`<A live list, not a history. An item leaves this table by being done, by being promoted into a step, or by being dropped with a reason. It never leaves silently.>`

| # | Item | Raised | Why not done then | Blocked by |
|---|---|---|---|---|
| 1 | `<...>` | `<date>` | `<...>` | `<nothing / step N.M / an open gap>` |

## Machine notes

`<Only what differs between the machines this project is built on, and only what has actually bitten. This table is the reason a multi-machine build stops re-discovering the same three things.>`

| Machine | What is different here | Consequence |
|---|---|---|
| `<label>` | `<path / runtime version / tool absent / permission>` | `<what to do about it>` |

## Gaps raised in this project

`<A pointer index, not a record of resolutions. It exists so a later reader can see how often the freeze had to be amended and where — a genuinely useful signal about which parts of the spec were thin.>`

| # | Kind | Step | One-line summary | Resolved where |
|---|---|---|---|---|
| 1 | `<CONTRACT-GAP \| STC-GAP>` | `<N.M>` | `<...>` | `<Logic Mk I Mod 1 A3 §7.2 / Logic §14 / OPEN>` |

---

## Compaction at every chapter gate

**When a chapter is accepted, that chapter's session entries are compacted into one short retrospective and the detail is deleted.** Three or four lines: what the chapter cost more than expected, what broke twice, which gaps it raised, which machine notes turned out to be permanent. The open queue, the machine notes and the gap index survive compaction; the session narrative does not.

This is the same discipline as emptying `directorium_temporarium/` at a gate (`Logic.md` §2.4), and for the same reason: an artifact that only grows will eventually be loaded by someone, and then it is context nobody budgeted for. **If something in a session entry deserves to survive compaction, it deserves to be promoted into a document that binds** — a machine note, a step, or an amendment. Anything else was a diary, and a closed chapter's diary has done its job.

### Chapter retrospectives

* **Chapter `<n>` — `<name>`, accepted `<date>`:** `<what it actually cost · what broke more than once · gaps raised · what changed in the documents because of it>`
