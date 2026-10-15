# Motion

For motion dial 5 and up. The baseline rules (transform/opacity only, motion values, reduced motion, a reason per animation) live in [SKILL.md](SKILL.md).

## Claimed means shown

Above motion 4 the page moves: hero entry, scroll reveal on key sections, hover physics on CTAs and cards. If working motion won't fit the scope, drop the dial to 3 and ship a clean static page. Half-built motion (cut-off triggers, jumpy entries, missing cleanup) is worse than none.

## Library choice

- **Motion** (`motion/react`): UI state, hover, reveal, layout transitions. The default.
- **GSAP + ScrollTrigger**: pinning, scrubbing, scroll hijack. Isolate in its own leaf component with `gsap.context` and `ctx.revert()` cleanup.
- **Three.js / WebGL**: canvas backgrounds and 3D. Same isolation.
- Keep GSAP or Three.js and Motion in separate component trees; they fight over frames.

## Patterns

- **Hover physics**: image inside `overflow-hidden`, `group-hover:scale-105 transition-transform duration-700 ease-out`.
- **Springs** for UI motion: `type: "spring", stiffness: 100, damping: 20`.
- **Magnetic buttons and pointer effects** (premium, playful, agency reads): `useMotionValue` + `useTransform`, outside render.
- **Perpetual loops** (pulse, shimmer, typewriter): only where they signal something live (status, feed, AI activity). Informational sections stay still.
- **Layout transitions**: `layout` / `layoutId` for reorders, expanding modals, shared elements. Only on elements that change.
- **Stagger**: `staggerChildren` with parent and children in the same client tree, or CSS `animation-delay: calc(var(--index) * 100ms)`.
- **Scroll-driven**: `useScroll`, ScrollTrigger, IntersectionObserver, or CSS `animation-timeline: view()`.
- **Image scale on scroll**: enter at `scale: 0.8`, grow to 1, fade toward `opacity: 0.2` on exit.
- **Scrubbed text reveal**: words go from `opacity: 0.1` to 1 as the paragraph scrolls through.
- **Pinned split**: section title pinned left while a gallery scrolls on the right.
- `will-change: transform` only on elements that animate. Lazy-load heavy libraries below the fold.

## Reveal stagger (no pinning)

Prefer Motion's `whileInView` for "appear on scroll". Save GSAP for pin and scrub work.

```tsx
"use client";
import { motion, useReducedMotion } from "motion/react";

export function RevealStagger({ items }: { items: string[] }) {
  const reduce = useReducedMotion();
  return (
    <ul className="grid gap-6">
      {items.map((item, i) => (
        <motion.li
          key={item}
          initial={reduce ? false : { opacity: 0, y: 24 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true, amount: 0.3 }}
          transition={{ duration: 0.6, delay: i * 0.06, ease: [0.16, 1, 0.3, 1] }}
        >
          {item}
        </motion.li>
      ))}
    </ul>
  );
}
```

## Sticky stack

Cards pin at the viewport top and the previous card shrinks as the next arrives. The key settings: `start: "top top"`, every card but the last pinned, and the shrink driven by the next card's trigger.

```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function StickyStack({ cards }: { cards: React.ReactNode[] }) {
  const ref = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !ref.current) return;
    const ctx = gsap.context(() => {
      const els = gsap.utils.toArray<HTMLElement>(".stack-card");
      els.forEach((card, i) => {
        if (i === els.length - 1) return;
        ScrollTrigger.create({
          trigger: card,
          start: "top top",
          endTrigger: els[els.length - 1],
          end: "top top",
          pin: true,
          pinSpacing: false,
        });
        gsap.to(card, {
          scale: 0.92,
          opacity: 0.55,
          ease: "none",
          scrollTrigger: { trigger: els[i + 1], start: "top bottom", end: "top top", scrub: true },
        });
      });
    }, ref);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <div ref={ref} className="relative">
      {cards.map((card, i) => (
        <div key={i} className="stack-card sticky top-0 min-h-[100dvh] flex items-center justify-center">
          {card}
        </div>
      ))}
    </div>
  );
}
```

## Horizontal pan

Vertical scroll drives a horizontal track. The wrapper pins at `start: "top top"`, the scroll length equals the track overflow, and the inner track scrubs.

```tsx
"use client";
import { useRef, useEffect } from "react";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { useReducedMotion } from "motion/react";

gsap.registerPlugin(ScrollTrigger);

export function HorizontalPan({ children }: { children: React.ReactNode }) {
  const wrap = useRef<HTMLDivElement>(null);
  const track = useRef<HTMLDivElement>(null);
  const reduce = useReducedMotion();

  useEffect(() => {
    if (reduce || !wrap.current || !track.current) return;
    const ctx = gsap.context(() => {
      const distance = track.current!.scrollWidth - window.innerWidth;
      gsap.to(track.current, {
        x: -distance,
        ease: "none",
        scrollTrigger: {
          trigger: wrap.current,
          start: "top top",
          end: () => `+=${distance}`,
          pin: true,
          scrub: 1,
          invalidateOnRefresh: true,
        },
      });
    }, wrap);
    return () => ctx.revert();
  }, [reduce]);

  return (
    <section ref={wrap} className="relative overflow-hidden">
      <div ref={track} className="flex h-[100dvh] items-center">{children}</div>
    </section>
  );
}
```

## Glass

For premium consumer, Apple-adjacent or media-overlay reads. Beyond `backdrop-blur`, add a 1px inner border (`border-white/10`) and an inset highlight (`shadow-[inset_0_1px_0_rgba(255,255,255,0.1)]`), with a solid fallback under `prefers-reduced-transparency`. For an Apple Liquid Glass look, see the approximation in [DESIGN-SYSTEMS.md](DESIGN-SYSTEMS.md).

## Vocabulary

Pattern names to design and talk with:

- **Hero**: asymmetric split, editorial manifesto, video/media mask, kinetic type, curtain reveal, scroll-pinned.
- **Navigation**: dock magnification, magnetic button, gooey menu, dynamic island, radial menu, speed dial, mega menu.
- **Layout**: bento, masonry, chroma grid, split-screen scroll, sticky-stack sections.
- **Cards**: parallax tilt, spotlight border, glass panel, holographic foil, swipe stack, morphing modal.
- **Scroll**: sticky stack, horizontal hijack, sequence scroll, zoom parallax, SVG progress path, liquid swipe.
- **Media**: dome gallery, coverflow, drag-to-pan grid, accordion slider (strips expand on hover), hover image trail, glitch image.
- **Type**: kinetic marquee, text mask reveal, scramble, circular text path, gradient stroke, inline pill images inside headlines.
- **Micro**: particle burst, liquid pull-to-refresh, skeleton shimmer, direction-aware hover fill, ripple, SVG line drawing, mesh gradient, lens blur depth.
