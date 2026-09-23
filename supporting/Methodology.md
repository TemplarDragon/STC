# How STC works — methodology and rationale

> Part of the [Standard Template Construct](../README.md). The templates are what a project copies; this document is why they are shaped the way they are — what the standard fixes and what it leaves alone, how it scales, how verification works, and the full procedure for starting a project. How the standard versions itself is at the end.

## Scope: what STC standardises, and what it deliberately does not

STC fixes **how** a project is specified and built — the four documents, the interface freeze, the railroad, the verification altitude, the version scheme. It does **not** prescribe **what kind of system** you are building.

That separation is enforced by two mechanisms. The first is the **Project Profile** (`Logic Template.md` §0.1): thirteen numbered yes/no rows — sixteen answers, since three of them split in two where one question was found to be carrying two different obligations. They ask about any dependency outside the process, two or more external surfaces, persistent state, a second store, an evolving core, operator-selected modes, self-detected modes, concurrency within a run, work on its own schedule, unattended survival, interchangeable backends, plugins, a real trust boundary, correctness that cannot be asserted exactly, an adopted framework, and prompts the project authors and tunes. **Every row defaults to NO.** Each NO names exactly which sections, appendices and directory blocks are **deleted** from that project's documents. The second is the **Pattern** (below), computed from those same answers, which decides how much of the standard's apparatus runs at all.

- Answer all NO and you get the **floor**: entry point, config, the work, its utilities, its data files, logs — plus a short logic doc and a short railroad. A single-purpose script or CLI tool looks exactly like this, and it should be *small*. **A ten-page logic doc for a three-file program is a failure of this template, not a success.**
- Answer some YES and the corresponding structures reappear, up to a multi-surface, multi-store, plugin-extensible system.

Deleting an inapplicable section is the standard working correctly — not cutting corners. The reverse is the expensive error: a data-layer facade over one CSV file, or a pipeline abstraction with a single stage, is indirection every future step must route through for no benefit. Turning a NO into a YES later is a **Mod bump** — a recorded, deliberate growth, and cheaper than carrying scaffolding nobody uses.

### Agent-assisted authoring

`AGENTS.md` governs authoring and maintenance of STC contract documents only.
It is not project law, is never read by Builder, and is not copied into a new
project. Tool-specific files such as `CLAUDE.md` are repository-maintenance
metadata under the same boundary.

### How the standard scales: the process is constant, the content is not

STC is meant to carry a fifty-line utility and a system of a hundred modules **without changing shape**. That works because the two are separated:

| Constant, whatever the project | Scales with the project |
|---|---|
| four documents | length of `Logic.md` §3.3 — one subsection per module, each as deep as its decisions genuinely are |
| the profile's rows, and the three Patterns | how many rows are YES, therefore how many concern sections survive, and which Pattern the project computes to |
| the seven rails and the step template | number of chapters, and number of steps per chapter |
| two verification artifacts per chapter — the checklist and the evidence artifact | number of entries in Appendix B.8 / C, and the length of the end-to-end flows |
| step size — always close to mechanical | total step count |

**Detail is depth, not layers.** A very complex system earns a very long logic doc: twenty-plus module subsections in §3.3, sub-flows numbered inside them, case tables, worked examples, a long interface freeze. What it does *not* earn is architecture nobody needs — extra indirection is not thoroughness, and a section describing a structure that was never built is worse than no section.

**A large railroad is expected, and harmless by construction.** More work means *more steps*, never bigger ones (rail 5). The reading order in §0 means a Builder loads one step plus the appendices it names — never the whole file — so a railroad of three hundred steps costs the same per step as one of twenty. Size is a navigation problem, and the numbering is the navigation.

**Under-specification is the expensive failure, not length.** Where a module's logic is written thinly, a Builder fills the gap by inventing — which is the one outcome every rail exists to prevent. Brevity is never the goal; *every paragraph carrying a decision or a reason* is.

---

## Patterns — the complexity class, and why the standard needs one

The profile scales **breadth**: which structures exist. It does nothing about **ceremony** — how much apparatus is brought to bear on them. Without a second dial, a three-file tool and a system with every row YES run the identical process: full contract appendices, a chapter ladder, per-step decision lists, a per-chapter acceptance walk, an audit protocol. That is how a standard silently raises its own floor, and it is the failure this section exists to prevent.

**Patterns are derived from solutions, not declared for projects.** Each mechanism in this standard was placed by asking *at what minimum profile does this start paying for itself?* — and the class boundaries are where many mechanisms turned out to demand the same rows. The count was not chosen in advance; two clusters emerged above the floor, so there are three classes. (The word *tier* is deliberately avoided: this standard already uses it for an architectural layer, in the Mod-bump rule.)

**The class is computed, never chosen — and the rule lives in one place: `Logic Template.md` §0.1.** Three classes: **I** the floor (one process, its own disk, a human running it) · **II** a boundary exists (a service, a store, a provider, an extension, an untrusted party, overlapping work — failures are now partial and foreign, but somebody is watching) · **III** nobody is watching (the system degrades or schedules itself, and is expected to survive without a human present). The build-side apparatus each class runs is catalogued, numbered, in `Railroad Template.md` §0. **This section explains why the mechanism exists; it does not restate it.**

**Two profile rows deliberately never raise the class:** the one about correctness that cannot be asserted exactly, and the one about an adopted framework. Each switches on exactly one contract and says nothing about whether a boundary exists or whether anyone is watching. A locally-run, attended script whose output is *judged* rather than asserted is a Pattern I project and should read like one. Letting a technology — or a correctness shape — set the ceremony is precisely how a standard inherits the identity of whatever system it was extracted from.

Six properties the rule was built to satisfy, each of which rules out a tempting shortcut:

| Property | What it forbids |
|---|---|
| **Total** | every one of the 2¹² profiles resolves; no combination needs a human to arbitrate |
| **Deterministic** | no predicate requiring judgement — no "the project is complex", no "a significant number of modules" |
| **Monotone** | flipping any row NO→YES never *lowers* the class; a rule that relaxes rigour when a requirement is added is broken however well it scores on examples |
| **Technology-independent** | the same problem in two ecosystems computes the same class; no weight is a function of the stack |
| **Volume-independent** | no count of lines, files or modules enters the rule — volume is a *consequence* of complexity, not a measure of it (*detail is depth, not layers*) |
| **Floor-dominant** | the common tool must land in Pattern I; a floor nobody would use for a small tool is a dead letter, not a floor |

### The boundary between what a class may and may not touch

**Immovable at every Pattern:** the document set, the rails, the step template, human-walked chapter-altitude verification, and the freeze. **Movable by class:** the numbered apparatus catalogue in `Railroad Template.md` §0 — separate versus inline contract appendices (A1), the audit protocol (A2), and the per-chapter evidence artifact (A3). **A4 was the separate Pattern III probe and is retired in Mk II, folded into A3**; its number is kept and never reused, because `PATTERN-EXCESS` counts against these numbers and recycling one would silently invalidate every count already recorded.

The line sits there because the immovable set answers *what did this project decide, and how do we know it works* — the properties every STC project is supposed to share, and the reason a standard exists at all. Everything movable is **apparatus**: it changes how much machinery proves the same thing, never what is proven. The test for anything proposed for the movable list: *does changing it alter what a reader can learn about the system, or only how long it took to write down?* Only the second may move.

**Which sections exist is not the class's business — it is the profile's.** An earlier revision of this section listed sections per class ("Pattern I forbids §4, §5, §10…"), which was true but derived: §4 is gated by the surfaces row, and that row is itself a class trigger, so the prohibition was a second copy of a rule the profile already carries — two places to change, and a guaranteed drift. The class governs apparatus; the profile governs structure; the over-engineering prohibitions that belong to neither (a second entry point with no second reason, a role-grouped directory holding two things, an adapter in front of one surface, a facade over one file) live in `Logic Template.md` §2.1, where the rest of the tree's rules are.

### Where a class cannot help, and the one artifact that fills the gap

**A human walk cannot see a race, a lost write, a duplicated external effect after a restart, or a loop that is alive but starved.** No amount of checklist discipline fixes this: those failures do not appear on the path a person follows. That is a real hole in chapter-altitude verification, and it is exactly the hole Pattern III projects fall into.

The answer is **not** to reintroduce a per-step suite, and not to declare a happy-path re-walk sufficient — it walks the same path the human just walked. (Nor is the answer to avoid anything test-*shaped*: the artifact below is executable and looks like a test, and what makes it legitimate is its altitude and whose criteria it serves — see the three clauses in `Railroad Template.md` §0.) It is the **provocation job of the chapter's evidence artifact** (apparatus A3, `Railroad Template.md` R3.3): two concurrent writers, then count the records; kill mid-effect, then assert the effect happened once; hold the loop busy, then assert the beat still advances. One artifact, chapter altitude, and — the constraint that keeps rail 2 intact — **every provocation traces to a `V#` the Architect wrote**, so the Builder decides how the property is provoked and never which property matters.

> **Mk I made this a separate artifact (A4) and Mk II folded it into A3.** Splitting them cost a second write event and bought no second kind of proof: both files boot the same system, both are read by the same person at the same gate, and both are stale the moment the criteria move. The failures listed above are still exactly what a human walk cannot see — that argument was right and is unchanged. What was wrong was believing it needed its own file.

### Crossing a class boundary is a Mod, not a new Mark

A class crossing is a **Mod bump**; `Mk` is reserved for a change of *purpose*, which is defined independently of complexity: **a `Mk` bump is warranted when the end-to-end flow in Appendix D is *replaced* rather than *extended*** — when "what does running this do?" gets a different answer, not a larger one. Adding a surface, a store, a provider or unattended operation extends the flow; turning a report generator into an interactive service replaces it. Put the old Appendix D beside the new one: if the old flow still runs, unchanged in intent, it is a Mod.

The reasoning is not aesthetic. Treating a class crossing as a new Mark would discard the Revision History — the project's only defence against reconstructing decisions from memory — and, worse, it would make honest profile answers costly: if raising a row can end the project's identity, the profile stops being answered truthfully, and a mechanism that rewards lying on its own input destroys itself.

### The four ways out, kept deliberately separate

**`PATTERN-WAIVER`** — omitting something your class requires: recorded in `Logic.md` §14 with **what covers the risk instead**, because a waiver naming no compensation is a shrug with a reference number. Uncounted, non-blocking, re-read at every Mod. **`PATTERN-EXCESS`** — adopting one **numbered** apparatus item from the class above: allowed three times, counted against the catalogue in `Railroad Template.md` §0 so that "one structure" is enumerable rather than arguable; the third means the class is wrong, so the project is promoted as a Mod. **`STC-GAP`** — the standard has no rubric for a decision already made: **do not halt**, record it in `Logic.md` §14, and copy it to the register at the end of this document. **Version pinning** — every `Logic.md` declares `Built against STC Mk … Mod … A…`.

The asymmetry between `STC-GAP` and `CONTRACT-GAP` is deliberate and worth stating plainly: a `CONTRACT-GAP` means the decision itself is missing, so improvising produces the wrong program and the Builder must stop. An `STC-GAP` means the decision exists and only its *form* is missing — halting there would charge a project for the standard's incompleteness.

---

## The six documents (`codex/`)

**Four documents are law. Two more exist, and neither is.**

`AGENTS.md` and `CLAUDE.md` are not STC lifecycle documents. They are
repository-maintenance metadata used only while authoring or maintaining the
standard. They are not project inputs, outputs, law, logs, companion
artifacts, or Builder-readable documents.

The law is written *from* something and executed *with* something, and pretending otherwise is how both of those turn into folklore:

| Artifact | Phase | Who writes it | Standing |
|---|---|---|---|
| **`Specification.md`** | **before** the law | the **owner**, alone, in plain language (English template or Polish twin — pick one) | an **input**. **Frozen in place** the day `Logic.md` opens — it stays in `codex/`, unedited, and is never consulted to build anything. Its only later job is to answer *"how far have we drifted from what was originally asked for?"* |

**What the specification is shaped like, and why it is not a questionnaire.** It asks for a premise, **a nested tree of the parts** (required: that tree is how the structure is introduced in the text, not an optional sketch), then — the part that carries the most — **plain-language walkthroughs of how they imagine each part working**, branches included, as long as they need to be, and only then a numbered list of what they want. **That order is deliberate.** The walkthrough is what most owners actually produce first when left alone, and a template that has no room for it gets one written anyway, in the margins of something else; the feature list is an index, and an index is written last — by reading the walkthroughs back and naming what each one delivers. Every `F#` names the walkthrough that delivers it, which makes coverage a property of the writing order rather than a check somebody has to remember. The **premise is the reference point**: every item is checked against it, and a divergence between the two is the earliest visible sign that a project is going wrong — cheap to fix there, a Mod bump once the law is written, a rebuild once code exists. The mapping from the owner's answers onto profile rows lives in `Logic Template.md` §0, not in the specification: the owner answers plain questions and never has to learn what a profile row is.
| the four below | the law | the Architect, with the owner | **normative** |
| **`codex/DevLog.md`** | **during** the build | the **Builder**, every session | a **journal**. Never law, never a decision, never evidence for a `V#`. Lives in the built project's repository, because its whole job is continuity across sessions and machines |

Neither of the two is a fifth or sixth "document" in the sense the next table means, and neither may drift into one: a specification that keeps being edited after the freeze stops being a record of intent, and a dev log that accumulates decisions becomes a shadow standard nobody froze. Both templates state their own hard rules; the rules are the point of them.

All six live in **`codex/`**, inside the project's own repository, beside an append-only `ARCH/` for superseded versions. The four that are law:

| File | Role | Analogous to |
|---|---|---|
| **`Logic.md`** | the **law** — *what* the system does and **why**: principles, the file architecture, the application's own logic module by module, then contracts and frozen interfaces. No implementation code. | a constitution / RFC |
| **`Railroad.md`** | the **build order** — sequences construction of the thing `Logic.md` describes into small steps, gated by acceptance criteria. Adds no new decisions of its own. | a project plan with acceptance criteria baked in |
| **`dependency.md`** | everything **outside** the package manager: external tools/runtimes, git-sourced or vendored repos, runtime-downloaded artifacts. | an infra/ops manifest |
| **`requirements.<ext>`** | the pinned, resolved package-manager manifest (`requirements.txt`, `package.json`, `Cargo.toml`, …). | `package-lock.json` / `poetry.lock` |

Repository-maintenance files — `AGENTS.md` and tool-specific configuration such as `CLAUDE.md` — belong to this standard's own repository and are never copied into a generated project.

**The documents live in the repository they describe** (`Logic Template.md` §2.10). `Logic.md` §2.1 is the layout of that same repository, `codex/` included — not of a separate folder somewhere else. A project whose law lives in another directory can be cloned without the reason it is shaped the way it is, and its code then has to be read as though it had no intent; that is the condition this standard exists to prevent. The trade is that the documents ship with the code — into the image, the archive, anything built from the repo — and a deployment that must not carry them excludes `codex/` at packaging time and records that it does.

### The division of labour between the two main documents

This is the distinction the whole standard rests on, and the one most often blurred:

| | `Logic.md` | `Railroad.md` |
|---|---|---|
| Answers | **WHY** it is built this way, and **WHAT** it decides | **WHAT to generate, step by step** |
| Contains | the reasoning, the rules of the problem, the file architecture, the module-by-module logic, the frozen contracts | ordered steps, verbatim signatures to implement, MUST-NOTs, acceptance criteria |
| Never contains | implementation code, ready-to-paste files, prompts for a code generator | a new decision of any kind |
| Read by | a human reviewer first, an agent second | the Builder, one step at a time |

**`Logic.md` §3 (Application Logic) is the longest section of the standard for a reason** — it is the business analysis: the domain vocabulary, the rules with their stated goals, one logic subsection per module (purpose, what it is *not* responsible for, its sequence, its decisions **and the reasoning behind each**, its failure behaviour), and the end-to-end flows. A document of contracts alone specifies a shape nobody can evaluate: a Builder can satisfy every signature and still write the wrong program, because "wrong" is only definable against intent.

**The file architecture lives in `Logic.md` §2.1, not in the railroad.** Where a responsibility lives is a design decision with a why — that is what keeps a project modular — so it belongs in the law. `Railroad.md` §0.5 is that same tree seen from the build side, annotated with stub and build-order rules. That section states the precedence between the two and owns the rule; this document does not restate it.

**The machinery lives in one place, and the bin is per agent.** Everything that exists only because the project is being built sits under `construction/`: the bookkeeping in `construction/ledger/` (`stub_registry.md` and the gate records, committed, shared by every agent), the verification artifacts in `construction/acceptance/`, and the throwaway bin in `construction/<XX>_workspace/` — one per agent, `CC_workspace/` beside `CX_workspace/`, so two of them never share a scratch area. The bin takes spikes, probes, one-off scripts, sample data and temporary output; it is gitignored, product code never imports from it, and it is **emptied at every chapter gate**, with anything that turned out to matter promoted into the real tree by a step that owns it *before* the emptying. With `codex/` these are the root's only two process entries, so a reader can tell the program from the scaffolding at a glance.

**Naming convention:** `Logic.md` carries its version in the filename once versioning starts (see *How the standard versions itself*, below), e.g. `codex/Logic Mk I Mod 1 A1.md`; superseded versions move to `codex/ARCH/` rather than being deleted, so a revision history is never fabricated from memory. Nothing in `ARCH/` is ever edited and nothing in it is law.

---

## The core methodology (`Railroad Template.md` §0) — keep this almost verbatim

`Railroad Template.md` §0 is pure process, with zero domain content — a general contract for turning a frozen spec into working code via small, non-improvised steps under a fixed verification budget. Highlights, so you know what you're buying into before you adopt it:

1. **Seven rails** — frozen public surface, frozen *acceptance criteria*, a MUST-NOT list per step, HALT-on-gap (`CONTRACT-GAP`) instead of improvising, small steps, frozen parameters (a bare adjective like "reasonable timeout" is a gap, not a spec — pin the number or the formula), and a provisioned surface (a frozen name also needs a **source** that fills it and a **path** the caller can reach it by — otherwise it is specified and unbuildable).
2. **Stub protocol** — the entire target tree is scaffolded first, every file a stub with a typed canned return; each phase *fills* stubs, never adds or moves files.
3. **`CONTRACT-GAP`** — the single escape hatch when the spec is wrong, missing, or ambiguous. The builder halts and reports it precisely instead of guessing; the architect resolves it with a `Logic.md` amendment (an A-bump, usually).
4. **Verification at chapter altitude, executed by a human** — see below. One altitude, Architect-authored criteria, two files per chapter; a step closes on a *printed checklist*.

### Where testing lives (and why it is not where you expect)

**The rule is three clauses, and it is stated positively on purpose** — `Railroad Template.md` §0 owns it: executable observation exists at exactly **one altitude** (the chapter gate); **what** is proven is always the Architect's, written as a `V#` before any code exists; and the whole budget is **two files per chapter**. Everything that sounds like a prohibition in this standard — no per-step test file, no fixtures module, no mock library, no `tests/` tree — is a *consequence* of those three, and none of them is a rule you could break independently.

That ordering matters, and Mk I got it backwards. It led with the prohibition, which reads as a taboo on a *kind of file*; and a taboo on a kind of file is obeyed in letter and routed around in fact. The proof is in this standard's own history: rail 6 requires pinned mechanisms to be exact, a human walk cannot observe one, Mk I had nowhere to put that observation, and the project riding it grew per-step evidence files to hold it. The need was legitimate and the rule had made it unspeakable. **So judge any proposed artifact by altitude and authorship, never by its filename or its imports** — the chapter evidence artifact is an executable file that boots the system, provokes races, prints `PASS`/`FAIL` and may pull a testing dependency, and it is permitted for exactly two reasons: where it sits, and whose criteria it serves.

A build step's proof of correctness is therefore a **printed ✓/✗ checklist**: each frozen decision (`D#`) and each observable criterion (`V#`) with a one-line proof — a value seen, a log line, an exit code. Nothing is written to disk for verification purposes.

Real verification happens at **chapter** boundaries. A chapter = one phase = one row of the milestone ladder = **a user-testable MVP increment**. Its gate is a short **Acceptance Checklist** written in the owner's language (*do this → expect to see that*), walked **by a human**, together with a re-walk of every earlier chapter's checklist.

Beside it sits the chapter's **one evidence artifact** (`Railroad Template.md` R3.3), written by the Builder at the chapter's last step against code that has stopped moving. It exists because a human walk, by construction, cannot see everything the rails pin: a person driving the system by hand cannot observe a bucket depth, a refill interval, an ordered effect trace, or the fact that a gate was *never consulted* — yet **rail 6 requires exactly those to be exact**. That gap is real, and Mk I had nowhere to put it, so projects grew per-step evidence files to fill it. Mk II names the need and gives it one artifact with three jobs: re-walk tripwire, mechanism observation, and provocation of the invisible properties (a race, a lost write, a duplicated effect after restart, a starved loop) that Mk I handled with a separate Pattern III probe.

**Verification artifacts are capped at two per chapter — the checklist and the evidence artifact.** If a project ever holds more verification files than twice its chapter count, the standard has been violated.

**Written at the end of the chapter, never step by step**, and that is a measured position rather than a taste. A Pattern III project built one evidence file per step and ended with **1929 lines of evidence against 1414 lines of the product code it observed**, the same scaffolding written six times. Running them was never the cost — a full re-walk of 41 criteria prints six lines. **Re-cutting them was:** one amendment moved a gate mid-chapter and four of six files had to be rewritten. What protects the window between a chapter's first and last step is not an artifact at all; it is the **re-cut** (R3.1) — the Architect reading each step's `V#` against that step's frozen surface before any code exists.

**When a chapter genuinely cannot be small**, the railroad has one narrow siding: the **LONG CHAPTER protocol** (`Railroad Template.md` §0.3). It is declared with a written reason — *"no intermediate state of this is observable"*, never *"this is a lot of work"* — and its checklist is segmented into at most five checkpoints, each walked as it is reached, closing with one end-to-end pass. Later chapters re-walk only that final pass, so the regression walk stays bounded.

Three reasons this is the design, not a shortcut:

- **Token economy.** A per-step suite is written, run, re-run for every later step (quadratically), and repaired when it breaks. For an AI Builder that cost dominates the actual code generation — and it buys a fourth restatement of a constraint rails 1, 3, 4 and 6 already enforce.
- **Legibility.** A check the project owner cannot read is not verification; it is a second unreviewed artifact that has to be trusted on faith.
- **Sequencing.** Tests before a working proof of concept protect an interface that has not been demonstrated yet. STC's answer is: demonstrate the chapter, *then* decide what deserves automation.

The cost is named openly in `Railroad Template.md` §0.3: between two chapter gates, a silent regression can go undetected. That window is bounded by the chapter, and it is the price paid for the budget. **Adopting a real automated suite later is a legitimate decision** — the owner's, taken once there is something worth protecting, and planned as its own chapter. It is never something a coding agent starts on its own.

If you only take one thing from STC without reading further, take this: **freeze the interface before generating any code**, and **treat every unpinned parameter as a defect**, not a detail to improvise later.

---

## Using this template for a new project

Do not copy repository-maintenance files such as `AGENTS.md` or `CLAUDE.md`
into the new project.

0. **The owner writes `Specification.md` first**, from `Specification Template.md` **or** `Specification Template PL.md` (pick one language and stay in it), alone and in plain language — what the thing should do, how they will know each feature worked, what it must never do, what it is deliberately not doing. Then they talk it through with the agent, in rounds, until *they* are satisfied. The agent asks, contradicts and points at gaps; it does not design here. **Nothing below starts until the readiness list at the end of that template passes.** Skipping this step does not save time: it moves the same conversation into `Logic.md`, where it gets held in technical vocabulary the owner never agreed to. The filled file is always named `Specification.md`, whichever template language was used.
1. Create `<new-project>/codex/` and copy into it: `Logic Template.md` → `codex/Logic Mk I Mod 1 A0.md`, `Railroad Template.md` → `codex/Railroad.md`, `supporting/Dependency Template.md` → `codex/dependency.md`, `supporting/Requirements Template.md` → `codex/requirements.<ext>` (pick the extension for your stack), and `supporting/DevLog Template.md` → `codex/DevLog.md`. The owner's `Specification.md` moves into `codex/` as well and is **frozen there the same day** — not archived, not edited again; the features keep their `F#` numbers so `Logic.md` §3 can cite them. Create `codex/ARCH/` empty; the first superseded logic version will be the first thing in it.
2. **Fill in the Project Profile (`Logic.md` §0.1) before writing anything else, compute the Pattern from it, then delete every section its NOs and its class point at** — in `Logic.md` and in `Railroad.md`'s file tree and appendices alike. Do this *first*: it is far easier to delete twelve rows' worth of structure from an empty skeleton than to notice, six chapters in, that you have been maintaining a persistence layer for a program that persists nothing.
3. **Write §2 (architecture) and §3 (application logic) before anything else in the document, and give §3 the most time.** §2.1 fixes where every responsibility lives; §3.3 says what each module does, in what order, and *why*. The later sections and the appendices are derived from these two — written in the other order, they become contracts nobody can justify.
4. Work through what remains of `Logic.md` top to bottom, replacing every `<...>` placeholder and `[STC: ...]` instruction comment with real content. Don't delete a section your profile says applies just because filling it out is effortful; that effort is exactly what the freeze buys later.
5. Freeze Appendix B (Contract / Ownership Map) and Appendix C (Config Keys) — these two are what let a coding agent (or a new teammate) build without guessing. Nothing in the prose above them may name an identifier absent from these appendices.
6. Only then write `Railroad.md`: walk the dependency graph from `Logic.md` Appendix A, decide build order (definition order ≠ build order — see Railroad Template §1), draw the chapter ladder so that **each chapter is a capability the owner can exercise by hand**, and author Phase 0 in full `Step N.M` detail before writing any code.
7. Every `Logic.md` revision from here on is a version bump with a Revision History entry — never a silent edit. Turning a profile NO into a YES is a **Mod** bump.

**Two sanity checks before you start generating code.** First: could someone tell what this program *does* from your `Logic.md` section list alone, or only that it was built from a template? Headings surviving with unfilled placeholders under them are the visible symptom of a profile nobody answered. Second: is §3 the longest part of the document? If the appendices outweigh the reasoning, you have written a specification of a shape rather than of a program — and the most expensive review comments will all arrive after the code exists.

---

## How the standard versions itself

> Superseded Marks of the standard are not kept here as files — **this standard's archive is its git history**, which begins at `Mk II Mod 1 A2`, and the commit closing each Mark from Mk II onward is tagged. Mk I predates this repository and is not in it in any form. A change to STC is never retroactive: a project pinned to `Mk II Mod 5 A0` stays correct against Mk II until its owner decides otherwise, as a Mod bump of that project.
>
> *(Numbering note, about **this standard's own** history: a Mark's baseline here is **Mod 0**. STC's Mk I began at Mod 1 before that was settled, and is left as written — a revision history that gets retrofitted stops being one. Projects are unaffected: a project's first logic document is `Mk I Mod 1 A0`, exactly as the template ships it.)*

### The versioning scheme (Mark / Mod / A)

`Logic.md` is a living document, so it needs a version scheme that says *how much changed*, not just *that* something changed:

- **Mark (`Mk`)** — the project's fundamental generation. Fixed once chosen; changing it means starting a new project, not revising this one.
- **Mod (Modification)** — bumped on a **fundamental change in logic**: architecture, a tier being added/removed, a core invariant reversed.
- **A (Alteration)** — bumped on a **smaller change within the same logic**: a clarification, a missing contract filled in, a parameter pinned, a contradiction resolved.

Every version bump is recorded in `Logic.md`'s **Document Revision History** (own section, append-only, oldest first) — never overwritten, never silently squashed. A bump's entry states *what changed and why*, not just *that* it changed; "why" is what lets a future reader judge whether a since-surfaced problem is already covered.

**Rule of thumb:** if the change would make an already-approved `Railroad.md` step wrong, it's at least a Mod. If it only fills a gap the railroad already assumed was filled, it's an A.

#### The standard versions itself, and every project pins the version it was built against

STC applies the same scheme to itself: **Mod** for a structural change (a rail, an invariant, a section, a Pattern rule), **A** for a clarification that changes nothing structural. Every bump is recorded in the commit that makes it: the git history is the standard's revision history, and the commit closing each Mark is tagged.

**And a `Mk` bump for the standard itself — defined in Mk II, because Mk I never was.** Mk I gave itself Mod and A and defined `Mk` only *for projects* (Appendix D's flow replaced rather than extended), so the question "what would justify a new Mark of STC?" had no rubric anywhere in the standard — the first genuine `STC-GAP` about STC, now registered below. The rule: **a `Mk` bump of the standard is warranted when what a project must PRODUCE changes, or when the altitude at which it is PROVEN changes.** A rail, a section, a Pattern rule, an appendix — those reshape how the work is done and are Mods however large they read. The artifact set and the verification altitude are what a reader of any STC project can see from the outside, and changing either means projects written before and after are no longer the same kind of object. That is a Mark.

Every project declares in `Logic.md` §0: `Built against STC Mk III Mod 1 A0`. This is not bookkeeping. Without it, "the project follows STC" means "it follows whatever STC happens to be today", and every later edit to the standard silently invalidates every document written before it — a moving target that no project can be audited against. **A change to STC is never retroactive.** Migrating a project onto a newer version of the standard is a decision its owner takes deliberately and records as a Mod bump of that project.

### `STC-GAP` register — the one piece of state the standard keeps across projects

The three-projects rule cannot enforce itself from inside the projects: entries scattered across three `Logic.md` §14 sections never meet, so nobody ever notices the third. It therefore needs a home here, and that home is a genuine concession — the four documents are per project and the standard is otherwise templates only, so this register is the sole mutable, cross-project artifact STC owns. It is small on purpose: one line per gap, one increment per project that hits it.

| Gap (what the standard had no rubric for) | Projects that hit it | Outcome |
|---|---|---|
| What justifies a **`Mk` bump of the standard itself**? STC defined `Mod` and `A` for itself and `Mk` only for projects, so a proposal to start a new Mark of STC had no rubric to be judged against. | `AID4` | **adopted in Mk II** — a `Mk` bump of the standard is warranted when what a project must *produce* changes, or the altitude at which it is *proven* changes. See the versioning section above. |
| Where does a project record the **observation of a pinned mechanism** — a threshold, a refill rate, an ordered effect trace — when rail 6 requires it exact and the human walk cannot see it? | `AID4` | **adopted in Mk II** — job 2 of the chapter evidence artifact (A3, `Railroad Template.md` R3.3). Before this the need was real and unhoused, so the project grew per-step evidence files, breaching the artifact cap for a legitimate reason. |
| `<one line>` | `<project A, project B>` | `<open · adopted in Mod N · rejected because …>` |

**A rejection is written down once, with its reason, and that is the point.** An unrecorded rejection is re-proposed by the next project, and the standard re-litigates a settled question every time it is used.

---

## What was deliberately left generic

Anything that would have named a specific technology, library, storage engine, or domain concept was replaced with a placeholder or an instruction comment. What survives is the *pattern*: layered sections with a consistent internal shape (goal → mechanism → invariants → open questions), NORMATIVE appendices as the single source of truth for identifiers, a step template that leaves no interpretation room, and a stub-first build order. Fill the placeholders with your project's actual technology choices — the standard doesn't prescribe any.
