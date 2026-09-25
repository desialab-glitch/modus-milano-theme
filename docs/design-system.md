# Modus Milano — Design System

## Typography
- H1/H2 font: Antonio Bold (NOT Bebas Neue — this has been a repeated mistake, double check)
- H3 sitewide: brand orange #D16A14
- H2: gold #c28342
- Desktop H1 letter-spacing: 0.06em (finalized, was diagnostically bumped through 0.045/0.06/0.1 before settling here — do not "fix" this thinking it's wrong)
- Mobile H1 letter-spacing: 0.08em (untouched, separate media query override)
- Product Page H1 (.product__title__wrapper h1): explicit 0.06em, coincidentally same as desktop default now

## Spacing tokens (in :root, modus-design-system.css)
- --modus-space-xs: 1.2rem (default rhythm)
- --modus-space-s: 1.6rem
- --modus-space-m: 2.4rem (Simple Slider exception)
- --modus-space-column: 4rem (desktop gutter)

## Known sitewide CSS fixes already applied (don't reintroduce these bugs)
- Multicolumn outer border: removed via `.multicolumn .multicolumn-list__wrapper { border: none !important; }`
- Multicolumn side padding: removed via `.multicolumn .multicolumn-card__wrapper { padding-left: 0 !important; padding-right: 0 !important; }` (top/bottom untouched)
- Inter-card divider lines (.border-item .multicolumn-card::before / .border-item::after): already fixed separately, don't confuse with the outer-border fix above
- Mobile CTAs (≤749px), sitewide via `.button--cta` in modus-design-system.css: full width, 48px min-height, no radius, centered (the Rich Text + CTA look). snippets/button.liquid adds the class whenever rendered with `layout:`; hand-written section CTAs carry it in markup. New sections with their own `<a class="button">` CTA must add `button--cta`; don't write per-section mobile button-width CSS. If a wrapper shrink-wraps the button, add it to the wrapper list in the same rule.
- Card content always fills the full width (client rule, 2026-09-25): image, text and buttons inside a card must reach both edges of the card, and the cards together must fill the section's full width. Space *between* cards goes on the container (`gap`), never as padding inside a card. Grid Banner's mobile slider used to add `padding-right: <mobile_gap>` to each card, so every card except the last was 10px wider than its content. Fixed in sections/grid-banner.liquid: the slider now uses `gap`, and in 2-up mode the flex-basis is `calc((100% - gap) / 2)`.
- @import for Antonio Google Font in modus-design-system.css MUST be the literal first rule in the file (CSS spec requirement) — any edit near the top of this file must verify @import still comes first, this broke silently once already

## Dead/orphaned files (do not edit, don't assume they're live)
- assets/modus-iwt-spacing-fix.css — superseded, dead
- assets/modus-paragraph-global.css — superseded, dead
- sections/image-with-text-OLIO-PATCH-placeholder-not-used.liquid — harmless orphan, renders nowhere
- templates/page.journal.json IS legitimate (not dead — confirmed separate real page from blog.journal.json, has its own documented CTA banner content)
