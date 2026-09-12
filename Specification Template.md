# `<PROJECT NAME>` — Specification

> **[STC template — delete this callout before use.]** The **first** document of a project and the only one its owner writes alone. It comes before `Logic.md` and it is deliberately non-technical: what you want and how you imagine it working — not how it will be built. A Polish twin lives beside this file as `Specification Template PL.md`; pick one language and write the content in that language. The structure is identical. The filled project file is always named `Specification.md`, whichever language you wrote it in.

**You write this. Not the agent.** An assistant may ask questions, point out where two of your sentences disagree, tell you when something is missing, warn you when §5 has drifted away from §2, and move a line to the section it actually belongs in. It must not design anything here, must not propose an architecture, and must not fill it in for you.

**Write the content in whatever language you think in.** Plain sentences beat technical ones. If you reach for a word you would have to look up, you are probably describing *how* instead of *what*.

**The one boundary that keeps this document useful:** no file names, no function names, no configuration flags, no library or engine names anywhere except **§6.3**. The test is simple — *could someone read this without opening the repository?* If not, you have crossed into `Logic.md`'s territory, and the agent should send you back.

**What happens to this file.** You write a first version, then talk it through in as many rounds as it takes. When **you** are satisfied that it describes the thing you actually want, work moves to `Logic.md`, where every technical decision is made. **From that day this file is frozen where it is — it stays in `codex/`, is never edited again, and is never consulted for building.** Its one remaining job is to answer *"how far has this drifted from what I originally asked for?"* — and it can only answer that if nobody tidied it up afterwards.

---

## 1. In one paragraph — what is this thing?

`<Describe it as you would to a colleague who has ninety seconds. If it will not fit in one paragraph, that is worth discovering now rather than after somebody builds it.>`

## 2. The premise — what I am trying to achieve, and in what direction

`<This is the reference point for the whole document. Not a feature list: the intent. What is this for, what should it feel like to have it, what is the general idea that holds all the parts together? Then the handful of rules that apply everywhere — "it must always answer quickly", "it must work with no internet", "it must remember what we already discussed", "it must never need me to be at my desk".>`

> **§4 and §5 are checked against this section, and that check is the point of putting it here.** If something in your feature list cannot be traced back to the premise, one of two things is true: the premise is incomplete, or that item does not belong to this project. **This is the earliest place a project can be seen going wrong**, and it costs nothing to catch it here — the same divergence found after `Logic.md` is written costs a Mod bump, and found after the code exists it costs a rebuild. The agent should say so out loud when it spots the gap; it should not quietly design around it.

## 3. A first sketch of the structure

`<This section is not optional. Draw the pieces you imagine, in the form below — that form is the point: later walkthroughs in §4 hang off these names, and Logic.md §2.1 reads this sketch as input. A nested tree with a one-line responsibility on each line is how the structure is introduced in this document. Replace the example names with yours; keep the shape.>`

```text
<root catalogue>
├─ <group of code files doing stuff in same area>  — <one line what this group does>
│   ├─ <component 1>                               — <one line what this file does>
│   └─ <component 2>                               — <one line what this file does>
├─ <group of code files doing stuff in other area> — <one line what this group does>
│   ├─ <component 3>                               — <one line what this file does>
│   └─ <component 4>                               — <one line what this file does>
├─ <the part that does the other work>             — <one line what this group does>
│   ├─ <…>
│   └─ <…>
└─ <pieces that exist but are empty for now>       — named so nobody invents them later; §6.2 is where they are explained
```

> **Nothing here is a decision.** This is your first map, and `Logic.md` may replace it entirely — a different split, different names, different number of pieces — without that being a failure of either document. Write each line as a *responsibility* ("the part that talks to people", "the part that remembers"), not as a file name, and if you already know something has to be a separate piece for a reason, say the reason on that line. Nesting is allowed and expected: a part that contains parts is how you show where something lives. Parts you draw but deliberately do not want yet stay on the tree *and* belong in §6.2.

## 4. How it should work

`<The heart of the document, and the place to be as detailed as you like. Group it whichever way you actually think — by part ("the bit that handles messages", "the bit that remembers") or by feature. Write each one as a numbered sequence in plain language: first this, then that, if X then Y, otherwise Z. A walkthrough may run to twenty steps if it has twenty steps. Where a step carries a real figure — how many arrive, how often, how big — write it into that step, because that is where it belongs; do not invent one: a missing figure is a question somebody will ask you, while a made-up figure becomes a frozen limit later.>`

### `<name of the part or the feature>`

1. `<what happens first — what arrives, or what starts it>`
2. `<...then what, including the branches: "if it is a command, do it and do not treat it as conversation">`
3. `<...through to what comes out, and what gets remembered>`

**In case of failure or error:** `<in your terms — retry quietly, tell me, stop everything, carry on without that part. This is a business decision, not a technical one, and if you do not make it here somebody makes it for you.>`

### `<next part>` `<...repeat>`

> **Stay above the code line.** Sequences like "check whether the sender is on my list, and if not, ignore it" are exactly right. "Load the IDs into a set at startup for fast lookup" is one level too deep — that is a decision, and decisions belong to `Logic.md`. When you catch yourself naming a mechanism instead of a behaviour, describe what you would *observe* instead.

## 5. What it should do

`<A list derived from §4: read back your own walkthroughs and name, one by one, what each of them delivers. One numbered item per thing this must be able to do — keep them short, because all the detail already stands above. Number them F1, F2, … and never renumber, even if you delete one: Logic.md will cite these numbers, and so will every later question about drift.>`

**F1 — `<short name>`**
- **Definition:** `<one or two sentences — what it is and what it does>`
- **Expected result:** `<what you would see, read, receive, or measure, such that someone else could check it without asking you. "It sends me the report by eight" is checkable. "It works correctly" is not.>`
- **Delivered by:** `<the names of the §4 walkthroughs that deliver it — or "—" if this is a property or a capability rather than a sequence>`

**F2 — `<short name>`** `<...repeat. An item may be a capability, a behaviour, an experience, or a question the thing should be able to answer.>`

> **Three habits.** If describing an item needs the word "and", it is probably two items — they will be built and accepted separately. If you cannot write the expected result, it is not yet an item; it is a wish, and it will be built as somebody's guess. *If the honest answer is "I would have to look at the results and judge them", write exactly that* — it is a legitimate answer, and it tells the technical document that this part needs a written rule for what counts as good enough. And if "delivered by" stays empty and you cannot say that the item is a property, that is not a gap in the line — it is a missing walkthrough in §4.
>
> **Nothing here is more important than anything else.** Everything on this list is in this version, in full. A thing you want "one day" or "if it works out" is not an item at half weight — it is an entry in §6.2, and that is the only honest place for it to stand. This file does not set the build order, and do not try to smuggle one in: that order comes from the dependencies between the parts, and `Railroad.md` sets it.

## 6. Rules of Engagement

`<Three short lists of flat bullets. No prose, no paragraphs — this is the one section where a blunt sentence beats a careful one. The examples below show the length and tone to aim for; replace them.>`

### 6.1 Must never

*Rules the finished thing obeys on every run, forever. Nobody trades one of these away for a deadline.*

- `<never send anything to a customer before I have seen it>`
- `<never delete or change the file it was given — always work on a copy>`
- `<never let one person's data show up in another person's view>`

### 6.2 Not in this version

*Things you can imagine wanting and are deliberately not asking for yet. **This list should not be empty** — everything named here is something nobody will quietly build "while they were in there", and something you will not be surprised is missing.*

- `<no phone version — I will be at a desk when I use it>`
- `<no second user this year; it is only me>`
- `<no automatic sending — I press the button, always>`

### 6.3 Imposed anyway

*Your own constraints on the **how**, each with the reason. **This is the only list in the whole document allowed to name a technology, a machine or a place** — and because each line is a choice rather than a requirement of the problem, each one can be challenged with a price attached. Nobody removes one without asking you; they may tell you what it costs.*

- `<it runs on my own machine, not a rented one — I do not want this data leaving the building>`
- `<it uses the database we already pay for — a second one is a second thing to maintain>`
- `<it is written in the language the team already reads — I want to be able to fix it without you>`

> **If you cannot tell which list a line belongs to, ask who could break it.** The **running program**, on any given Tuesday → **6.1**. Only **building it wrong**, and *you* chose it → **6.3**. Only building it wrong, and *nobody* chose it — it is simply true of the place it runs → that is not a limit at all, it is terrain, and it goes in §7. Nothing at all breaks 6.2, which is why that list is scope rather than a rule.
>
> The case that catches everyone: *"it must not need the internet"*. If there is no connection where it runs, that is **§7**. If there is one and you would rather it did not depend on it, that is **6.3** — and the *why* is the half worth writing down.

## 7. Target Rules of Engagement

`<Seven questions. Answer each one in a sentence of your own, in the slot after it; the italic line underneath is a hint about the kind of answer, not a menu to pick from. **"I do not know" is a complete answer** — an honest gap gets resolved later, an invented one gets frozen into the design.>`

**The shape, so there is no doubt:** for *"what starts it?"*, a finished answer reads `I start it myself, usually late evening when I get back from a delivery round.` A plain sentence, no mechanism, and it happens to answer the third question too.

- **What starts it?** `<...>`
  *me by hand · another program · a clock, on a schedule · an event arriving · a device*
- **Who or what receives the result?** `<...>`
  *me · a person who is not me · another program · a screen nobody watches · a machine*
- **Should it run by itself?** `<...>`
  *"I start it when I need it" · "it should just happen, without me". Answer this one even if you answer nothing else here — it is the single question that changes the most about how the thing has to be built.*
- **What information does it touch?** `<...>`
  *my own notes · other people's personal data · money · someone else's system of record · nothing that matters if it leaks*
- **When something fails, what do you prefer?** `<...>`
  *wait and try again quietly · tell me immediately · stop and change nothing · carry on with the part that still works*
- **Where will it end up running?** `<...>`
  *my own laptop · a machine at work someone else administers · a server · a small device somewhere physical · a phone · "wherever, I do not mind". Add what you know about that place: is there internet, is it always on, does it reboot on its own, does anyone else log into it, do you have admin rights.*
- **Where will it be built, and is that the same place?** `<...>`
  *if you or an agent will work on this across more than one machine — desktop and laptop, work and home, one with the tools and one without — say so. A build that moves between machines needs that written down before the first session, not discovered in the third.*

> **Why the last two questions are here and not in §6.3.** Same subject, opposite standing. An environment you **chose** is a §6.3 constraint and can be costed and revisited. An environment that simply **is** — the machine that reboots at midnight, the laptop with no admin rights — is terrain: you did not pick it and you cannot buy your way out of it, so it can only be designed around.
>
> **Still belonging in neither:** a toolchain. *"It must work offline on a small device"* is terrain. *"Use this framework and that database"* is a decision, and it stays in `Logic.md` — made against everything written here, rather than picked before anyone knew what the thing had to do.

## 8. Current status at the time of writing the documentation **[OPTIONAL — delete this section if the thing does not exist in any form yet]**

`<Only if there is a current way of doing this: the manual steps, the spreadsheet, the copy-paste, the "I remember to do it on Fridays". If the project is new and there is no predecessor, delete the section — an empty section is worse than an absent one.>`

## 9. My open questions

`<Things you have not decided, in your own words. A visible undecided question gets resolved; an invisible one gets decided for you by whoever builds that part.>`

## 10. Clarifications from the conversations

`<Write the answers back into this file, in your own words rather than the agent's — a chat window scrolls away. And if you are asked the same question twice, do not just answer again: the section it refers to is unclear, so fix the section.>`

| # | The question | My answer | What it changed |
|---|---|---|---|
| 1 | `<...>` | `<...>` | `<F3 / §2 / §6>` |

## 11. Further development plans — a heads-up, not a request

`<Directions you are already fairly sure about and are deliberately not specifying: "eventually this serves the whole team, not just me", "at some point the data will have to sit somewhere other people can read it", "I expect I will want it running on a schedule one day". Say what you expect, and roughly when if you have a rough when. Do **not** describe how it should work — that is the part that turns this section from useful into harmful.>`

> **How this differs from §6.2.** That list is a **no**: something you want, are not asking for now, and the technical document records as deferred work. This section is a **yes, eventually**: a direction you already believe in, which nobody is being asked to build, plan or accommodate. Both sit outside this version — the difference is that one was declined and the other was foreseen. One catch worth knowing: a line here that names a specific engine or machine is not a direction, it is a constraint you have already chosen, and it belongs in §6.3 where it can be costed.

> **The one rule that stops this section doing damage — it may break a tie, it may never buy a structure.** Where two designs are otherwise equal, the one that does not foreclose something named here is the better choice, and that is the entire value of writing it down. Nothing on this list may be cited as the reason an abstraction, a configuration flag, an extension point or a spare layer exists **today**. A plugin system built because this section mentions plugins is precisely the failure the technical document's over-engineering rules exist to prevent — and this section makes that failure easier to reach, which is why the rule is written here rather than left to good judgement. The same applies to you: if you catch yourself writing steps, branches or shapes for something on this list, it has stopped being a heads-up and become a §5 item you never decided to ask for. Move it or cut it.

---

## 12. Am I ready to move on to `Logic.md`?

Not a formality — passing this list is what makes the technical document writable without guessing.

- [ ] **Every item in §5 can be traced back to the premise in §2**, and §2 does not promise a direction that §5 ignores.
- [ ] Every item in §5 has an **expected result** that someone else could check without asking me.
- [ ] **Every item in §5 names the §4 walkthrough that delivers it** — or says outright that it is a property rather than a sequence; and every §4 walkthrough delivers at least one item.
- [ ] Every part in §4 has its **"In case of failure or error"** line filled in.
- [ ] **§6.1, §6.2 and §6.3 all have entries**, and §6.2 in particular is not empty.
- [ ] **Every question in §7 has an answer in my own words** — no hint left standing in place of an answer, and "I do not know" written where that is the truth.
- [ ] **§7's "should it run by itself?" is answered** — or the fact that I do not know is written in §9.
- [ ] **§3 has a filled tree** in the form the template shows — parts nested under parts, a one-line responsibility on each, not left as placeholders, and not written as file names.
- [ ] Nothing outside **§6.3** names a technology, a library, a file or a function, and every line in §6.3 carries its reason.
- [ ] **§11 describes no mechanism** — every line on it says *what* is coming, never *how* it would work.
- [ ] Items are numbered `F#` and I have not renumbered them.
- [ ] I could walk another person through this document **in one sitting**, and they could tell me back what the thing does.

**When those hold, `Logic.md` opens** — and every further refinement of the business logic happens *there*, including the parts you have not thought about yet. This file stops being edited the same day, without exception: it is now the record of what you originally asked for, and that record is worth exactly as much as its resistance to being tidied up later.

`Specification frozen: <date> · kept at codex/Specification.md · Logic.md Mk <N> Mod <M> A<K> opened from it · not edited after this line was written`
