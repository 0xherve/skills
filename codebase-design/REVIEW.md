# Architecture review

Surface architectural friction across a codebase and propose **deepening opportunities**: refactors that turn shallow modules into deep ones. Uses the vocabulary in [SKILL.md](SKILL.md) exactly in every suggestion. The project's domain glossary (`CONTEXT.md` or `GLOSSARY.md`) names good seams; ADRs in `docs/adr/` record decisions this review leaves settled.

## 1. Explore

**Scope before you scan: YAGNI.** Deepening pays off by making future changes easier, so weight the parts of the codebase that change most. Decide _where_ to look before you look:

- If the user named a direction (a module, a subsystem, a pain point), take it and skip the inference below.
- Otherwise, walk back a good stretch of `git log --oneline` to find the **hot spots**, the files and areas that keep coming up, and let those pull your attention first. If changes are scattered with no clear hot spot, widen the net.

Read the domain glossary and any ADRs in the area first. Then spawn a sub-agent to walk the codebase organically, noting where it hits friction:

- Where does understanding one concept require bouncing between many small modules?
- Where are modules **shallow**, with an interface nearly as complex as the implementation?
- Where were pure functions extracted just for testability, while the real bugs hide in how they're called (no **locality**)?
- Where do tightly-coupled modules leak across their seams?
- Which parts are untested, or hard to test through their current interface?

Apply the **deletion test** to anything that looks shallow: a "yes, concentrates" is the signal you want.

## 2. Present candidates as an HTML report

Write one self-contained HTML file to `${TMPDIR:-/tmp}/architecture-review-<timestamp>.html` so nothing lands in the repo, open it with `xdg-open`, and give the user the absolute path. Follow [HTML-REPORT.md](HTML-REPORT.md) for the scaffold, diagram patterns and styling.

Each candidate gets a card: **Files**, **Problem** (the mechanism or number that hurts, not the feeling), **Solution** (plain English, active voice with a named actor), **Benefits** (in locality and leverage terms, plus how tests improve), a side-by-side **Before / After diagram**, and a **Recommendation strength** badge (`Strong`, `Worth exploring`, `Speculative`). End with a **Top recommendation**: which candidate to tackle first and why.

Name modules in the domain glossary's words: if it defines "Order", say "the Order intake module", not "the FooBarHandler" or "the Order service".

Surface a candidate that contradicts an ADR only when the friction is real enough to reopen it, and mark it with a warning callout (_"contradicts ADR-0007, but worth reopening because…"_).

The report proposes candidates only; interfaces come later. After writing it, ask: "Which of these would you like to explore?"

## 3. Grill the chosen candidate

Once the user picks one, walk its design tree with them in rounds: constraints, dependencies, the shape of the deepened module, what sits behind the seam, which tests survive. Each round, ask every question whose prerequisites are settled, numbered, each with your recommended answer, then wait. Look facts up yourself; put decisions to the user. Done when no question is left open.

Keep the domain model current as decisions crystallise:

- **New concept named?** Add the term to the glossary (create `CONTEXT.md` lazily if neither file exists).
- **Fuzzy term sharpened?** Update the glossary right there.
- **Candidate rejected for a load-bearing reason?** Offer an ADR: _"Want me to record this as an ADR so future reviews don't re-suggest it?"_ Offer only when a future reviewer would need the reason; ephemeral ones ("not worth it right now") don't qualify.
- **Exploring alternative interfaces?** Use [DESIGN-IT-TWICE.md](DESIGN-IT-TWICE.md).
