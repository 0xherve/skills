# Design systems

When the brief reads as a real system, install the official package and use it as shipped: its tokens, its components, its theming. One system per project. Customise within the system's theming; recreating its CSS by hand or overriding most of its tokens defeats the point.

## Map

| Brief reads as | Reach for |
|---|---|
| Microsoft-style enterprise SaaS, dashboards | `@fluentui/react-components` or `@fluentui/web-components` |
| Google-ish, Material-flavoured product | `@material/web` + Material 3 tokens |
| IBM-style B2B, enterprise analytics, dense data | `@carbon/react` + `@carbon/styles` |
| Shopify app surfaces | Polaris web components (`polaris.js`) or Polaris React |
| Atlassian / Jira-style product | `@atlaskit/*` + `@atlaskit/tokens` |
| GitHub-style devtool or community page | `@primer/css`, or `@primer/react-brand` for marketing |
| UK public-sector service | `govuk-frontend` |
| US public-sector, trust-first | `uswds` |
| Fast local business or agency MVP | Bootstrap 5.3 |
| Accessible React foundation | `@radix-ui/themes` |
| Modern SaaS where you own the components | shadcn/ui, customised: radii, colors, shadows, type set to the project |
| Tailwind-based SaaS or AI marketing | Tailwind v4 utilities + `dark:` |

Set theming once at the root (`layout.tsx` or page root) so sections inherit it.

## Aesthetics without a package

Build these with native CSS and Tailwind, and label borrowed inspiration honestly in comments.

| Aesthetic | Implementation |
|---|---|
| Glass, frosted | `backdrop-filter`, layered borders, highlight overlay, solid fallback under `prefers-reduced-transparency` |
| Bento | CSS Grid, mixed cell sizes, `grid-flow-dense` |
| Brutalism | Native CSS, monospace, raw borders |
| Editorial | Asymmetric grid, generous whitespace, serif when justified |
| Dark tech | Mono type, one neon accent, terminal motifs |
| Aurora, mesh | SVG or layered radial gradients |
| Kinetic type | CSS animations, scroll-driven animation, GSAP for hijacks |

## Install

```bash
npm install @material/web                                  # Material Web (M3)
npm install @fluentui/react-components                     # Fluent UI React v9
npm install @fluentui/web-components @fluentui/tokens      # Fluent web components
npm install @carbon/react @carbon/styles                   # IBM Carbon
npm install @radix-ui/themes                               # Radix Themes
npx shadcn@latest init && npx shadcn@latest add button card input
npm install --save @primer/css                             # Primer CSS
npm install @primer/react-brand                            # Primer Brand
npm install govuk-frontend                                 # GOV.UK Frontend
npm install uswds                                          # USWDS
yarn add @atlaskit/css-reset @atlaskit/tokens @atlaskit/button   # Atlassian
npm install bootstrap                                      # Bootstrap 5.3
# Shopify Polaris: in the app HTML head
#   <meta name="shopify-api-key" content="%SHOPIFY_API_KEY%" />
#   <script src="https://cdn.shopify.com/shopifycloud/polaris.js"></script>
```

## Canonical docs

Read the system's own docs before reinventing a component.

- Material Web: https://material-web.dev/theming/material-theming/, https://m3.material.io/develop/web
- Fluent UI: https://fluent2.microsoft.design/get-started/develop, https://learn.microsoft.com/en-us/fluent-ui/web-components/
- Carbon: https://carbondesignsystem.com/developing/react-tutorial/overview/
- Polaris: https://shopify.dev/docs/api/app-home/web-components, https://polaris-react.shopify.com/components
- Atlassian: https://atlassian.design/get-started/develop, https://atlassian.design/tokens/design-tokens
- Primer: https://primer.style/, https://github.com/primer/brand
- GOV.UK: https://design-system.service.gov.uk/components/button/
- USWDS: https://designsystem.digital.gov/documentation/developers/
- Bootstrap: https://getbootstrap.com/docs/5.3/layout/grid/
- Tailwind: https://tailwindcss.com/docs/dark-mode, https://tailwindcss.com/blog/tailwindcss-v4
- Radix: https://www.radix-ui.com/themes/docs/components/theme
- shadcn/ui: https://ui.shadcn.com/docs
- MDN: backdrop-filter, prefers-color-scheme, prefers-reduced-motion, Grid layout, Scroll-driven animations
- Apple materials: https://developer.apple.com/design/human-interface-guidelines/materials, https://developer.apple.com/documentation/TechnologyOverviews/liquid-glass

## Apple Liquid Glass on the web

Liquid Glass is an Apple platform material. Apple ships no web CSS for it, so anything on the web is a frosted-glass approximation; say so in a comment.

```css
/* Web approximation of Apple Liquid Glass, not an Apple asset */
.liquid-glass-web-approx {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  border-radius: 999px;
  border: 1px solid rgb(255 255 255 / .32);
  background:
    linear-gradient(135deg, rgb(255 255 255 / .30), rgb(255 255 255 / .08)),
    rgb(255 255 255 / .12);
  backdrop-filter: blur(24px) saturate(180%) contrast(1.05);
  -webkit-backdrop-filter: blur(24px) saturate(180%) contrast(1.05);
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / .48),
    inset 0 -1px 0 rgb(255 255 255 / .12),
    0 18px 60px rgb(0 0 0 / .18);
}
.liquid-glass-web-approx::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  border-radius: inherit;
  background:
    radial-gradient(circle at 20% 0%, rgb(255 255 255 / .55), transparent 34%),
    linear-gradient(90deg, rgb(255 255 255 / .18), transparent 42%, rgb(255 255 255 / .14));
  pointer-events: none;
}
.liquid-glass-web-approx::after {
  content: "";
  position: absolute;
  inset: 1px;
  border-radius: inherit;
  border: 1px solid rgb(255 255 255 / .14);
  pointer-events: none;
}
@media (prefers-color-scheme: dark) {
  .liquid-glass-web-approx {
    border-color: rgb(255 255 255 / .18);
    background:
      linear-gradient(135deg, rgb(255 255 255 / .16), rgb(255 255 255 / .04)),
      rgb(15 23 42 / .42);
    box-shadow: inset 0 1px 0 rgb(255 255 255 / .22), 0 18px 60px rgb(0 0 0 / .42);
  }
}
@media (prefers-reduced-transparency: reduce) {
  .liquid-glass-web-approx {
    background: rgb(255 255 255 / .96);
    backdrop-filter: none;
    -webkit-backdrop-filter: none;
  }
}
```

`prefers-reduced-transparency` support is uneven; keep text contrast sufficient even without the blur.
