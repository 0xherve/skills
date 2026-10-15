---
name: postplan
description: Write a standalone HTML report for a plan, report or task an agent carried out.
disable-model-invocation: true
---

## Write a report

Create one standalone HTML file directly in `~/Documents/postplan/`:

```sh
mkdir -p ~/Documents/postplan
touch ~/Documents/postplan/<report-slug>.html
```

Reuse the same filename for revisions so a later upload updates the existing draft.

The file must include:

- A valid HTML document with `<title>` and one `<h1>`.
- A concise description written for someone who was not in the room.
- Only the sections needed to explain the work.
- Inline CSS only. The file must work when opened locally and remain useful without JavaScript.
- Semantic HTML, readable contrast, responsive layout, and a print-friendly presentation.

### Visual baseline

Design the report as a polished editorial document, not a generic dashboard. Establish a small set of CSS custom properties for the page background, surface, text, muted text, border, and semantic status colors. Use a strong type scale, generous spacing, restrained use of borders and shadows, and cards only when they improve grouping. Keep the palette restrained, reserve color for information, success, warning, and blocker states, and avoid gradients, decorative noise, and empty UI chrome. Make sure you use enough width for the content.

Keep reports concise. Lead with the outcome and skip restating the prompt. Write in active voice with a named actor, one idea per sentence. Link every file, PR, issue, and document you name. Local paths are the exception. Write them as `<code>` spans, because the upload rejects the `file:` protocol.

## Validate before reporting done

```sh
grep -niE "<link|<form|<iframe|<object|<embed|<base|on(click|load|error)=|javascript:|file:///" <file>
grep -n "REPLACE ME\|Supporting line\|path/to/file\|Opening paragraph" <file>
python3 -c "s=open('<file>').read();print(s[s.index('<body>'):].count(chr(8212)),'em dashes in body')"
python3 -c "import sys;from html.parser import HTMLParser;HTMLParser().feed(open(sys.argv[1]).read())" <file>
```

Both greps must find nothing, the em-dash count must be 0, and the HTML parser must complete. Then open it with `xdg-open <file>` and tell the user the path. Upload only when asked.

## Publishing (only when asked)

```sh
npx postplan upload <file>              # first upload, or update the draft for this path
npx postplan upload <file> --new        # force a separate draft
npx postplan upload <file> --description "<text>"
npx postplan list --json                #  list all uploaded plans 
```

Assume authenticated. If it fails on auth, say so and point at `npx postplan auth` / `npx postplan whoami`.

Path-to-draft mappings live in `~/.postplan/drafts.json`; the same file path updates the same draft. The CLI prints a draft URL and a `Raw HTML` URL. Hosted documents disallow web fonts and JavaScript, so use system fonts and CSS media queries. Documents cap at 512 KB.

## Read a Postplan URL

Fetch with the shell, not web search or a browser. Strip a trailing slash, append `/raw` unless already present:

```sh
curl --fail --silent --show-error --location --max-time 30 --output /tmp/postplan.html '<raw-url>'
```

Read `/tmp/postplan.html` and continue. A web-search refusal is not a Postplan rejection. If `curl` fails, report its actual error.
