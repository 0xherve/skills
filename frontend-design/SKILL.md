---
name: frontend-design
description: Design and build web interfaces that look intentional, not templated. Use when building any UI, page, app or HTML; when making a landing page or portfolio; when redesigning an existing site; or when asked to make something look better.
---

# Frontend design

Every rule here is contextual. Read the brief first, then pull only what fits it. 

Existing design language in the project wins over everything below. Match its tokens, components and tone before adding anything new. You can also help standardize the design system for the project you are working in.

## 1. Design read

Before any code, read these signals: page kind (app screen, landing, portfolio, editorial, redesign), the user's vibe words, references they linked or named, the audience, existing brand assets, and quiet constraints (public sector, regulated, accessibility-first, kids). Quiet constraints and the audience outrank your taste.

State the read in one line, with the three dials:

> Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <design system or aesthetic>. Dials: variance 7, motion 6, density 4.

- **Variance** (1 symmetric, 10 asymmetric): 1-3 equal grid, centered. 4-7 offsets, mixed aspect ratios, left-aligned headers. 8-10 masonry, fractional grids (`2fr 1fr 1fr`), large empty zones. Asymmetry lives above `md`; below 768px every layout collapses to one column.
- **Motion** (1 static, 10 cinematic): 1-3 hover and active states only. 4-7 eased CSS transitions and staggered load-ins. 8-10 scroll choreography, pinning, scrubbing.
- **Density** (1 gallery, 10 cockpit): 1-3 `py-32` to `py-48` between sections. 4-7 `py-16` to `py-24`. 8-10 tight padding, 1px dividers in place of cards, `font-mono` for numbers.

Starting presets: SaaS landing 7/6/4, agency 9/8/3, premium consumer 7/6/3, designer portfolio 8/7/3, developer portfolio 6/5/4, editorial 6/4/3, public sector 3/2/5, app screen 4/3/6. "Minimal, calm, Linear-style" pulls toward 5/3/2; "Awwwards, experimental" toward 9/9/3.

If the read forks (say, Linear-clean vs Awwwards-experimental), ask exactly one question. Otherwise declare the read and proceed.

Vary deliberately. Choose layout, type and palette from the read, and make a different choice from the last page you built for a similar brief.

## 2. Foundation

If the brief reads as a real design system (Fluent, Material, Carbon, Polaris, Atlassian, Primer, GOV.UK, USWDS, Radix, shadcn/ui, Bootstrap), install the official package and use it as shipped. One system per project. See [DESIGN-SYSTEMS.md](DESIGN-SYSTEMS.md) for the map, install commands and canonical docs.

Otherwise it's an aesthetic (glass, bento, brutalist, editorial, dark tech, kinetic type). Build with Tailwind and native CSS.

Default stack when the project has none: React or Next.js with Server Components, Tailwind v4 (`@tailwindcss/postcss` or the Vite plugin), Motion from `motion/react`, fonts through `next/font` or self-hosted with `font-display: swap`. Check `package.json` before importing any library and print the install command for anything missing. Interactive pieces (motion, scroll, pointer physics) live in isolated `"use client"` leaf components.

## 3. Constraints

**Scales.** Spacing from a 4px or 8px base (4, 8, 12, 16, 24, 32, 48, 64, 96, 128), no magic numbers. Type from a 1.25 or 1.333 ratio, each size with a job. Body `text-base leading-relaxed max-w-[65ch]`.

**Type.** Default display and body sans: Geist, Satoshi, Outfit, Cabinet Grotesk or a brand font. Inter fits neutral, Linear-style or public-sector briefs. Reach for serif only when the brand names one or the brief is editorial, luxury or heritage, and rotate the serif between projects. Emphasise a word with italic or bold of the same family. Italic display words with descenders (`y g j p q`) need `leading-[1.1]` and `pb-1`.

**Color.** Neutral base (zinc, slate, stone) plus one accent, saturation under 80%. Lock the accent across the whole page. One gray temperature per project. Off-black and off-white in place of pure `#000` and `#fff`. Purple or neon glow only when the brand asks for it.

**Shape.** One radius system per page (all sharp, all soft 12-16px, or pill for interactive), or a written rule followed everywhere. Shadows tinted to the background hue. Cards only when elevation means hierarchy; otherwise group with spacing, `border-t` or `divide-y`.

**Layout.**
- CSS Grid for multi-column layouts, not flex percentage math.
- Full-height sections use `min-h-[100dvh]`.
- Contain pages with `max-w-7xl mx-auto` or `max-w-[1400px]`.
- Every multi-column component declares its under-768px fallback in the same file.
- Navigation fits one line on desktop, 64-72px tall (80px max).
- Z-index only for real layers (nav, modal, overlay, grain), from a documented scale.
- Wrap animated pages in `overflow-x-hidden` so off-screen motion never adds a horizontal scrollbar.

**States.** Every view ships loading (skeleton matching the final shape), empty (says how to populate), and error (inline for forms, toast only for transient). Buttons get `:active` feedback (`scale-[0.98]` or `-translate-y-px`).

**Forms.** Label above input, helper text, error below, `gap-2`. Every input has a real label; the placeholder is only an example.

**Theme.** One theme per page, light, dark or auto at the root; sections stay in it. Design both modes from the start for consumer pages, with Tailwind `dark:` or CSS variable tokens (pick one). Hierarchy and brand accent must hold in both.

**Accessibility.** WCAG AA contrast on every text, button, placeholder, focus ring and error (4.5:1 body, 3:1 large). Visible focus rings. Semantic HTML. 44px touch targets. Meaningful alt text.

**Motion.** Animate `transform` and `opacity` only. Continuous values (pointer, scroll progress) go through `useMotionValue`/`useTransform`/`useScroll` or ScrollTrigger, never React state or raw `scroll` listeners. Above motion 3, everything honours `prefers-reduced-motion` and collapses to static. Every animation has a one-sentence reason: hierarchy, story, feedback or state change. For motion 5 and up, read [MOTION.md](MOTION.md).

**Icons.** One library: Phosphor, Hugeicons, Radix or Tabler (Lucide only if asked or already present). Consistent stroke width. A missing glyph means a second library, not a hand-drawn path.

**Content.** Realistic text lengths and data. Names, brands and numbers sound real and specific (`47.2%`, not `99.99%`; a contextual brand, not Acme). Concrete verbs over "elevate, seamless, unleash", and the plain word over the fancy one ("use", not "leverage"). Each claim names what the product does or gives a number, not a feeling. Visible text uses periods, commas, colons or a hyphen; zero em or en dashes. Emoji only for a deliberately playful brief.

## 4. Branches

- **Landing page, portfolio, marketing or editorial page**: read [MARKETING.md](MARKETING.md) before building. It holds the hero rules, section flow, bento, imagery, copy and the marketing tells.
- **Redesign of an existing site**: read [REDESIGN.md](REDESIGN.md) first; it decides the mode and the audit.
- **Dashboards, data tables, wizards, editors, native mobile**: use the matching design system or specialist library (TanStack Table, AG Grid, Monaco). Apply only sections 1-3 here.

## 5. Pre-flight

The work is done when every line holds. Check each against the actual code; if one fails, fix it and recheck.

- [ ] Design read and dials stated, and the build matches them.
- [ ] Foundation chosen: official system as shipped, or aesthetic built honestly.
- [ ] Spacing and type come from the scales.
- [ ] One accent, one radius system, one theme, locked across the page.
- [ ] Every text, button, form element and focus ring passes AA contrast in each shipped mode.
- [ ] Loading, empty and error states exist.
- [ ] Every multi-column layout has its mobile fallback; nothing scrolls sideways at 375px.
- [ ] Motion is motivated, transform/opacity only, cleaned up in `useEffect`, and reduced-motion safe.
- [ ] Every imported library is installed; icons come from one library.
- [ ] Zero em or en dashes in visible text; copy read back once and every string makes sense.
- [ ] Branch checklist passed (MARKETING.md or REDESIGN.md), if one applied.
- [ ] You opened the page and looked at it, in both modes if it ships both.
