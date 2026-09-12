# <PROJECT NAME> — pinned package-manager manifest
#
# [STC template — delete this block before use.] This file's ROLE, not its syntax, is what's standardized:
# a single pinned, dependency-manager-native manifest, grouped by the architectural role each package plays
# (per Logic.md's sections), each group commented with a §-reference back to the logic doc. Swap this actual
# file for your ecosystem's native format — package.json + lockfile, Cargo.toml + Cargo.lock, go.mod + go.sum,
# poetry.lock, Gemfile.lock, etc. — but keep the grouping-by-role convention: a reader should be able to
# answer "why is this dependency here" by reading the comment above it, not by grepping git blame.
#
# READY TO USE, ALWAYS. This file installs as-is — `pip install -r requirements.txt`, or your ecosystem's
# equivalent — with no edit first and nothing to strip out. Every non-package line is a comment, so the
# reasoning travels inside the manifest instead of in a prose document beside it.
#
# ONE pinned set for the whole project (and any sibling projects sharing an environment, per dependency.md).
# Versions are the RESOLVED set (<YYYY-MM-DD>, <runtime + version>) — not invented; every entry verified
# installable on the target runtime (dependency.md §4). Transitive deps are resolved by the package manager
# at install time. Non-package-manager dependencies (external tools, runtimes, git-vendored sources, runtime-
# downloaded artifacts) live in `dependency.md` (same directory). Adding a package here = a CONTRACT-GAP
# against Railroad.md §0 unless it's coordinated the way dependency.md's Rules section says.
#
# NOTE: anything your runtime's standard library already provides adds NOTHING here — don't pin a package
# for something already built in; note it in dependency.md instead so the decision is recorded once.

# The role names below are EXAMPLES of the grouping convention, and the §-refs point at the STC Logic
# section that justifies each group. Keep only the groups your project actually has — a group per profile
# row you answered NO is a group you delete, not one you leave empty.
#
# EVERY ENTRY CARRIES ONE LINE: why it is here, and the FIRST place in Logic.md or Railroad.md that uses
# it. One line, because a reason has to survive being read in a hurry. The first use rather than every
# use, because a reader who has the first one can follow the thread from there. An entry without that
# line is an entry nobody can justify deleting later — which is exactly how a manifest silently grows.

# ---- <Architectural role, e.g. "The work itself / core framework" — Logic.md §3, §8> ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- <Architectural role, e.g. "Data / persistence" — Logic.md §5>   [PROFILE P2] ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- <Architectural role, e.g. "External integrations / providers" — Logic.md §10>   [PROFILE P8] ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- <Architectural role, e.g. "Config / validation" — Logic.md §1 (principle 2), Appendix C> ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- <Architectural role, e.g. "Security" — Logic.md §12>   [PROFILE P10] ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- <Architectural role, e.g. "Interface layer / transport" — Logic.md §4>   [PROFILE P1b] ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- <Architectural role, e.g. "Resilience — retry/backoff" — Logic.md §9> ----
<package>==<pinned-version>    # <why this one> — first used: <Logic.md §3.3 / Railroad Step N.M>

# ---- Dev tooling ----
# NOTE: STC has no per-step test suite (Railroad.md §0.3 / Appendix R3). Verification is a printed
# checklist per step and a HUMAN-WALKED acceptance checklist per chapter. Do NOT pin a test
# framework here by reflex — add one ONLY if a chapter smoke script (R3.3) actually exists, and
# add it the same way as any other dependency: through the Step 0.0 freeze, never mid-build.
<type-checker>==<pinned-version>
<linter>==<pinned-version>
# <test-framework>==<pinned-version>    # only if an R3.3 smoke script exists
