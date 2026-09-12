# `<PROJECT NAME>` — Non-Package-Manager Dependencies & Sources

> **[STC template — delete this callout before use.]** Companion to **`requirements.<ext>`** (same directory; the package-manager-installable set). This file lists everything the package manager does **not** handle: **external tools/runtimes**, **git-sourced or vendored repositories**, and **runtime-downloaded artifacts** — plus the resolution findings (§4).

Target runtime: `<e.g. "Node 22 LTS" / "Python 3.14 standard" / "Go 1.23">`. `<State your environment-sharing policy if it matters — e.g. "one shared environment, no per-component drift" — and cross-reference Railroad.md §0 if adding a dependency requires coordination across sibling projects/components.>`

---

## 1. External tools / runtimes (installed outside the package manager)

| Tool | Why / logic ref | Install (illustrative) | Required? |
|---|---|---|---|
| `<runtime, e.g. "Node 22">` | `<why this project needs it>` | `<OS installer / version manager>` | **REQUIRED** |
| `<external service with a GUI/manual step, e.g. a desktop database app>` | `<Logic.md §ref>` | `<...>` | **REQUIRED for `<mode>`**; degrades gracefully without it |
| `<build toolchain, if any native deps exist>` | `<only if something must build from source>` | `<...>` | **NOT NEEDED currently** — keep as a fallback note if you've verified everything installs from prebuilt artifacts |

> **[STC: if any dependency needs a manual step to start (a desktop app's GUI "Start" button, a service that isn't auto-started by the OS), call it out explicitly here — this is exactly the kind of thing that silently breaks unattended/CI runs months later.]**

## 2. Git-sourced / referenced repositories (NOT installed via the package manager)

| Repo | Role | Handling |
|---|---|---|
| `<owner/repo>` | `<why it's referenced — concepts mined, code vendored, or pure reference reading>` | `<"Reference-only, do NOT install/import" / "vendored under /vendor, pinned to commit X" / "git submodule">` |

*(Add future vendored/git sources here — each with role + whether cloned/vendored/reference-only.)*

## 3. Runtime-downloaded artifacts (fetched on first use, not by the package manager)

| Artifact | Fetched by | Note |
|---|---|---|
| `<model weights / dataset / cache>` | `<the library that auto-downloads it>` | `<sizing/version note>` |

> **[STC: if this project needs to run fully offline at some tier, note here what must be pre-cached — both these artifacts and the package-manager wheels/modules — so that tier can be provisioned with no network.]**

## 4. Resolution status (package set) — `<YYYY-MM-DD>`, `<runtime + version>`

> **[STC: re-date this section every time the pinned set changes.** A resolution note that outlives the set it describes is worse than no note, because it reads as a verification somebody performed on today's manifest when in fact it was performed on a different one. The date and the runtime **are** the claim; if either moved, the claim has to be made again.**]**

`<Record HOW the set was resolved (lockfile tool + command) and confirm it installs clean on the target runtime with no compiler / no native build step, if that's a goal. Note any package that had no compatible prebuilt artifact and what replaced it, with the reason — this is exactly the kind of decision that gets silently re-made differently by someone else later if it isn't written down once, here.>`

**Packages with no compatible prebuilt artifact → intentionally replaced:**

| Wanted | Status | Replacement (in `requirements.<ext>`) |
|---|---|---|
| `<package>` | `<why it doesn't fit — needs a compiler, pulls an unwanted heavy transitive dep, etc.>` | `<what you use instead>` |

## Re-verify

```text
<the exact command(s) to install the pinned set into the target environment, and a separate dry-run /
consistency-check command if your package manager supports one>
```

## Rules

- **When this list is written: while authoring, before the freeze.** The natural moment is between `Logic.md` closing and `Railroad.md` being written — whoever plans the build walks the dependency graph and can already see what each chapter will need. **Step 0.0 then resolves and pins what authoring listed.** After that step, adding anything here or to `requirements.<ext>` is a `CONTRACT-GAP` and an amendment, never a step's own decision (rail 3).
- **`requirements.<ext>`** = the pinned package-manager set (versions resolved, not invented).
- **This file** = the non-package-manager sources (tools / git / runtimes / artifacts).
- `<If this project shares its dependency set with sibling projects, say so and name the coordination rule — e.g. "adding a dependency here is coordinated across siblings; an uncoordinated addition is a CONTRACT-GAP against Railroad.md §0.">`
- `<Note any language/runtime-version features that are stdlib-only and therefore add nothing to either manifest — worth stating once so nobody "adds a dependency" for something already built in.>`
