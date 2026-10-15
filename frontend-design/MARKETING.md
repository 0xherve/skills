# Marketing pages

Landing pages, portfolios, marketing and editorial pages. They live on the first impression, not the full read, so every section earns its place in a glance. Applies on top of [SKILL.md](SKILL.md).

## Page flow

Navigation, then a flow that follows AIDA:

- **Attention**: the hero.
- **Interest**: what it is and does (features, bento, work).
- **Desire**: proof and depth (product in use, testimonials, case studies, a scroll story when motion is high).
- **Action**: one closing CTA, then the footer.

Section spacing follows the density dial. Each section carries one message.

## Hero

The hero is one moment: value prop and primary CTA, all inside the first viewport.

- **Headline**: 2 lines on desktop, 3 at most. Put the H1 in a wide container (`max-w-5xl` or wider) so it flows horizontally. Size it with the asset: `text-4xl md:text-5xl lg:text-6xl` by default, `text-6xl md:text-7xl` only for 3-5 word headlines. A 4-line headline is a font-size or container-width error; fix those before cutting copy.
- **Stack**: at most 4 text elements: an optional eyebrow or brand strip, headline, subtext (20 words, 4 lines max), and CTAs (one primary, at most one secondary).
- **Top padding**: `pt-24` max on desktop. Need more presence? Grow type or asset.
- **Visual**: a real image, video, or real component preview. A gradient blob alone is a placeholder.
- **Layouts**: asymmetric split, editorial manifesto, media-mask, kinetic type, curtain reveal, scroll-pinned, cinematic center over full-bleed image with a dark wash. Above variance 4, prefer off-center layouts; centered fits manifesto and launch briefs where the message is the design.
- Trust logos, pricing teasers, feature bullets, avatar rows and taglines live in sections below the hero.

## Sections

- **Layout families**: each family (3-up image cards, split text-image, full-width quote, bento, marquee, sticky stack, horizontal pan, accordion) appears once per page. Eight sections use at least four families. At most two image-text split sections in a row.
- **Section headers**: headline, then body below it at `max-w-[65ch]`. A two-column header earns its place only when the right column holds a visual or interactive element.
- **Eyebrows** (small uppercase tracked labels): at most one per three sections, hero included. Name the topic in plain words. The headline alone is usually enough.
- **Feature rows**: two-column zig-zag, asymmetric grid, bento, scroll-pinned or horizontal scroll, in place of three equal cards.
- **CTAs**: one label per intent across the page (pick one of "Get in touch / Let's talk / Contact us" and reuse it in nav, hero and footer). Primary labels are 1-3 words and fit on one line at desktop.
- **Marquee**: at most one per page.

## Bento

- Exactly as many cells as content items: 3 items, 3 cells; 5 items, 5 cells. Use `grid-flow-dense` and check that `col-span`/`row-span` values interlock with no empty cell.
- 3 to 5 intentional cells beat 8 busy ones.
- At least 2-3 cells carry real visual variation: image, brand gradient, pattern or tint.
- Vary rhythm: mix full-width rows, asymmetric sizes and vertical breaks.

## Imagery

Marketing pages are visual products. Even a minimal page has 2-3 real images.

1. If an image-generation tool is available, generate section-specific assets at the right aspect ratio.
2. Otherwise use real photography: brief-provided URLs, or `https://picsum.photos/seed/{section-keyword}/{w}/{h}`. Filters (`grayscale`, `mix-blend-luminosity`, `contrast-125`) help stock read as art direction.
3. Otherwise leave labelled slots (`<!-- TODO: hero product photo, 1600x1200 -->`) and list the needed images at the end of your reply.

To show a product, use a real screenshot, a generated image, or a real mini component; div-built fake dashboards and terminals read as AI.

**Logo wall**: under the hero, logos only, real SVGs from Simple Icons (`https://cdn.simpleicons.org/{slug}/{hex}`) or devicon. For invented brands, draw a simple monogram SVG. Logos render in both modes; brand name goes in alt text.

**Ambient backgrounds**: radial blurs, grain or mesh gradients fit when the read calls for them. Put grain on a fixed `pointer-events-none` overlay so scrolling containers stay cheap.

## Content and copy

- Default section shape: headline up to 8 words, sub-paragraph up to 25 words, one visual or one CTA.
- More than 5 items get a different component: grouped two-column split, card grid, tabs, accordion, scroll-snap pills, carousel or marquee. Long spec sheets become a 2-col card grid, grouped clusters, or 3-4 featured specs plus a "full specifications" disclosure.
- Precise numbers come from the brief or are marked as sample data.
- One copy register per page (technical, editorial or punchy), unless the brand mixes them on purpose.
- **Testimonials**: 3 lines of quote max, typographic quotes, attribution with name, role and company.
- **Copy audit**: re-read every visible string. Rewrite anything grammatically broken, with an unclear referent, cute-but-wrong, straining to sound thoughtful, or framed as "not just X, but Y" (state Y). Plain functional copy beats clever copy.

## Palette for premium consumer

Cookware, wellness, artisan, luxury and DTC briefs pull toward warm cream + brass/clay/oxblood + espresso text. Reach past it: cold luxury (silver, chrome, smoke), forest (deep green, bone, amber), black and tan, cobalt and cream, terracotta and slate, olive and brick, or monochrome with one saturated pop. Use the warm-craft palette when the brand names those colors or is vintage craft, and rotate families between projects.

## Tells

These mark a page as generated. Use one only when the brief asks for it.

- Version or status labels in the hero (`V0.6`, `BETA`) outside a real launch; version footers on marketing pages.
- Numbered labels: `001 · Capabilities`, `01 / 4` on tiles, "Stage 1 / Step 2" as labels (the step's own verb is the label).
- Micro-meta: "Brand · No. 01" sub-eyebrows, meta-sentences under headings, decorative photo credits, pills overlaid on images.
- Decoration: middle-dot chains (one `·` per line max), colored status dots without real state, crosshair grid lines, vertical rotated text, `<br>`-split italic headlines, hero-bottom strips like `BRAND. MOTION. SPATIAL.`.
- Locale, time or weather strips, unless the brand is about place or time zones.
- Scroll cues ("Scroll to explore", mouse icons).
- Poetic section labels ("Field notes", "Quietly trusted by"); plain labels ("Testimonials", "Trusted by") or none.
- Hairlines on every row of a long list; filled-track progress bars as comparison visuals.
- Custom cursors; gradient text on large headings; outer glows.

## Checklist

Run with the SKILL.md pre-flight.

- [ ] Hero fits the first viewport: headline 2-3 lines, subtext 20 words max, CTA visible, 4 text elements max, `pt-24` max.
- [ ] Hero has a real visual; logo wall sits below it, logos only.
- [ ] Eyebrow count is at most ceil(sections / 3).
- [ ] No layout family repeats; at most two image-text splits in a row; at most one marquee.
- [ ] One CTA label per intent; no CTA wraps at desktop.
- [ ] Bento cell count equals item count, no empty cells, 2-3 cells visually varied.
- [ ] Real images in place, or labelled slots listed for the user.
- [ ] Lists over 5 items use a fitting component.
- [ ] Copy audit done; quotes 3 lines max.
- [ ] None of the tells above, unless the brief asked.
