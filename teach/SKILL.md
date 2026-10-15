---
name: teach
description: Teach me how and why something in this codebase works, as a page I can read and come back to.
disable-model-invocation: true
argument-hint: "What do you want to understand?"
---

Teach me the thing I named until I understand it. Leave the code as it is. The lesson is one HTML page I can come back to.

## 1. Pick the takeaways

Decide the two to four things I should walk away understanding. Choose them from why I'm asking (about to change it, reviewing it, debugging it, new to it) and what I already know, both read from the conversation. Done when each takeaway is a one-line claim about this code.

## 2. Dig the how

Trace the flow in the code: what triggers it, each step, where data goes, the decision points, and where it connects to the rest of the codebase. Trace a single module or narrow question yourself. For a subsystem spanning several files or services, use parallel explorers per [EXPLORE.md](EXPLORE.md). Done when every takeaway has its mechanism located in named files and functions.

## 3. Dig the why

Code shows what it does, never why it exists, so the why comes from the record: `git blame -L`, `git log --follow -- <file>` traced back past the latest commit, the PR behind each substantive change (`gh pr view <n> --comments`), linked issues, ADRs, comments. Search Sentry, Slack or ClickUp too when those tools are connected and the code looks defensive (retries, guards, limits, flags).

Sort every reason into a **tier**, and phrase it to match:

- **Found**: someone wrote the reason down. State it plainly, with the citation beside it (PR, commit, issue, `file:line`).
- **Inferred**: no one wrote it, but the evidence points there. Hedge it ("likely", "seems to") and show the chain: "given A and B, C is likely".
- **Unknown**: you looked and it isn't there. Say what you searched and where, and who would know.

When my question carries a guess ("why do we have X? it's not needed"), treat the guess as one candidate and check it against the record. When sources disagree, show both. Done when every why sits in a tier and every Found claim has its citation.

## 4. Write the page

Save it to `~/Documents/postplan/teach-<slug>.html`. One file, inline CSS, no JavaScript, system fonts. It should read like a well-set article: a clear type scale, generous spacing, a restrained palette, and enough width for code. Write file paths as `<code>`.

Sections, dropping any with nothing real to say:

1. **Overview.** What it is in general terms, with its common name if it has one. Then "here we use it to ...". Someone who reads only this knows what the thing is.
2. **Key concepts.** The few types, modules or ideas the rest depends on, one line each. Give each one name and keep it.
3. **How it works.** The longest section, one part per takeaway. Say the problem it solves, then the mechanism step by step.
4. **Why it's like this.** Found, then Inferred, then Unknown.
5. **Where things live.** The files I'd open first.
6. **Gotchas.** What looks like it works one way but works another.
7. **Keep / Change / Avoid / Risk.** Only when I'm asking because I want to change it.
8. **Next questions.** Two or three threads worth pulling, one line each.

Write it the way you'd explain it to me out loud. Keep each sentence to one or two commas and split clauses that pile up. Use periods and commas, no em dashes. Use concrete names: "`UserService` calls `AuthClient.refresh()`", not "the service delegates to the client". When something is complex, say why. Aim for this density: "Virtualization runs in two parts, one for rendering and one for loading from disk. When an item scrolls out past the buffer, both its DOM node and its in-memory data are evicted."

Draw a diagram when a picture lands faster than words. Pick the view that fits: a call tree for runtime flow, a file tree for where things live, pseudocode for logic, a sequence for parts talking to each other, a diff for what changes. Draw them as inline SVG or `<pre>` blocks. For three or more moving parts, draw a short series where each diagram redraws the last and adds one part, so I watch it assemble.

## 5. Hand it over

Check the page parses and has no external loads or scripts:

```sh
python3 -c "import sys;from html.parser import HTMLParser;HTMLParser().feed(open(sys.argv[1]).read())" <file>
grep -niE "<link|<script|<iframe|on(click|load|error)=|javascript:|file:///" <file>
```

The parser finishes and the grep finds nothing. Then `xdg-open` the page and reply with the path, the main point in two sentences, and the next questions. When I follow up, revise the same page.
