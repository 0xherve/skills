---
name: to-spec
description: Turn the current conversation into a short, product-focused spec (PRD) for my team or for another agent to build from.
disable-model-invocation: true
---

Synthesise what we've already discussed into a spec. The spec says _what_ we're building and _why_, in product language a teammate can skim in two minutes.

## 1. Find the house style

Look for the repo's own spec conventions before writing: templates and writing rules in `.agents/references/`, `AGENTS.md` / `CLAUDE.md`, `docs/`, and existing PRDs or specs. When the repo has them, they win over the defaults below; follow their template, numbering, file location and naming exactly.

## 2. Pick the reader

- **Team spec**: a PRD or plan the team reviews. Product-focused; the implementation plan lives in a separate doc if at all.
- **Build spec**: a handoff another model builds from without this chat. Self-contained: it adds the design decisions (modules, interfaces, data shapes) a builder needs.

If the conversation doesn't make it clear, ask which.

## 3. Unblock, briefly

List the unsettled decisions the spec depends on. Ask only those, in one numbered round, each with your recommended answer. Look up every fact yourself. Zero questions is fine when nothing is open.

## 4. Write it

Default shape when the repo has none:

```
# <Feature name>

<2-4 lines: the problem, from the user's side, and the solution in one sentence.>

## Scope
In: ...  Out: ...

## Functional requirements
### FR-01 <name>
<One or two sentences: what the product does.>
- AC-01-01 <checkable outcome>

## Non-functional requirements   (only when one actually surfaced)

## Design decisions               (build specs only)

## Open items
<Gaps flagged as gaps, with who can close them.>
```

Rules every spec follows:

- **Short and skimmable.** Tables, bullets and bold lead-ins over paragraphs. Cut any section with nothing real to say.
- **Product language.** Full words, no abbreviations or internal shorthand. Describe behaviour the user sees, in present tense and active voice with a named actor ("an admin can", "the system sends"), with "must" for requirements.
- **Product, not provenance.** The body carries the product only. Issue numbers, change-request references, "verified by" lines, evidence notes, environment details and permission codes stay out.
- **Requirement hygiene.** Each requirement lives in exactly one place. A role or permission check is an acceptance criterion of the feature it guards, not its own FR. Keep FRs and NFRs apart. Cite by number (`FR-03`), never by title. After removing one, renumber everything after it.
- **Testable.** Every AC is a checkable outcome. List gaps under Open items instead of filling them with guesses.
- **Builds stay lean.** Tests and docs are out of scope unless I asked for them. File paths and code snippets stay out; they go stale.

## 5. Land it

Save it where the house style says. Otherwise: a build spec goes to `SPEC.md` at the repo root; a team spec goes to `docs/specs/<slug>.md`. When it replaces an older spec, delete the old one. Publish to an issue tracker only when I ask.

Show me the path and a three-line summary for review.
