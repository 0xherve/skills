---
name: to-tickets
description: Break a spec, plan, or the current conversation into short, ordered tickets, published as GitHub issues or a local task list.
disable-model-invocation: true
---

Break the work into **tickets**: tracer-bullet slices, each a narrow but complete path through every layer it touches, each demoable or checkable on its own, each small enough for one agent session.

## 1. Gather

Work from the conversation. If I pass a spec path, issue number or URL, read it in full (`gh issue view <n> --comments` for GitHub). Use the repo's domain words (`CONTEXT.md` / `GLOSSARY.md`) in every title.

Check the tracker for open issues that already cover part of this work (`gh issue list --search`). Plan to absorb them. Fold overlapping and stale ones into the new tickets and close them with a link, rather than creating duplicates.

## 2. Slice

- Only the work that's left. Done work stays out.
- Order the tickets so each can start once the ones before it land. Note a dependency only where the order isn't obvious.
- Put any prefactoring first: make the change easy, then make the easy change.
- Large efforts go in **phases** with a review gate between them.
- A wide mechanical change (a rename across the codebase) goes expand, migrate in batches, contract, so every batch lands green.
- Tests and test tooling are out unless I asked for them.

## 3. Review with me

Show the breakdown as a numbered list: **title**, **what it delivers** (one line, from the user's side), and the issues it absorbs. Add a rough duration per ticket when I ask for estimates. Iterate until I approve.

## 4. Publish

**GitHub** (default when the repo has a remote and I didn't say otherwise):

- Use the repo's issue template from `.github/ISSUE_TEMPLATE/`; fill every section it has.
- Title describes the work ("Address anti-slop rules in full"), not the area.
- Use only labels that already exist. Assign to whoever I name.
- Environment details go in the template's environment field and nowhere else.
- Close absorbed issues with a comment linking the ticket that replaces them.

**Local** (no tracker, or I ask): one `TASKS.md` at the repo root, a checklist in ticket order, unless the repo already keeps tasks somewhere.

Ticket body when there's no template:

```
## What to build
<The behaviour this ticket makes work, from the user's side.>

## Acceptance criteria
- [ ] <checkable outcome>

## After
<Tickets that must land first, only when the order isn't obvious.>
```

Write every ticket in product language, in active voice, one idea per sentence. File paths and code snippets stay out; they go stale.
