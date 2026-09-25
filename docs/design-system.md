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

## Section spacing (top/bottom of each section) — edited per section, values defined once
- Every section keeps its own "Margin top/bottom" (outside its background) and "Padding top/bottom" (inside its background) settings in the theme editor: none / XS / S / M / L. Choose these per section as needed.
- The sizes behind those options live ONLY in the `--modus-section-space-*` tokens in modus-design-system.css. snippets/section-margin.liquid and snippets/section-padding.liquid read them via snippets/section-space-value.liquid. To change what "M" means sitewide, edit the token, never a snippet or a section.
- Current values (unchanged from before the tokens were introduced):

  | Size | Mobile (<990px) | 990–1149px | Desktop (≥1150px) |
  |---|---|---|---|
  | none | 0 | 0 | 0 |
  | XS | 12px | 12px | 12px |
  | S (also blank) | 30px | 32px | 32px |
  | M | 40px | 52px | 64px |
  | L | 60px | 80px | 100px |
- Any section that isn't built on these settings (AI-generated blocks, custom sections, app sections) must still take its vertical spacing from these tokens — no hardcoded px/rem section spacing anywhere.

## Per-section checklist (run on every new or edited section, on mobile AND desktop)
1. Section top/bottom spacing comes from the editor settings → `--modus-section-space-*` tokens. No hardcoded section padding/margin.
2. Side gutter = the theme `.container` / `var(--main-padding)` (20px mobile, 80px ≥1150px), same on both sides. Nothing extra on top of it (no inner side padding that pushes text in further than other sections).
3. Eyebrow → heading → text → CTA gaps = `var(--modus-space-xs)` (12px), applied once (element margin OR flex gap, never both). Stacked media ↔ text gap = `var(--modus-space-s)` (16px). Desktop side-by-side gutter = `var(--modus-space-column)`.
4. Alignment: left-aligned text for editorial/content sections on mobile. Centered only for short overlay/banner moments (hero over image, one-line CTA).
5. Typography: eyebrow = Lora italic 15px, grey rgba(61,61,61,0.6) on light schemes; H2 Antonio gold (29px mobile); body paragraphs 16px / line-height 1.6 via the sitewide paragraph rule. No text below 13px on mobile (open exception: the product-card collection badge, 10px uppercase, pending a size decision). Any text that can wrap to two lines needs a line-height of at least 1.4 (small labels/badges included).
6. CTAs: carry `button--cta` (automatic via snippets/button.liquid with `layout:`); on mobile they're full width, 48px tall, square. If the CTA doesn't fill the width, fix the shrink-wrapping wrapper in the shared rule, not per section.
7. Empty elements (e.g. a CTA wrapper with no button) must not add space.
8. Color scheme overrides (e.g. the orange scheme's beige text) still win — section rules must not use higher specificity than the scheme rules.
9. After any theme push: no userErrors, and checksums on the draft match the local files.

## Known sitewide CSS fixes already applied (don't reintroduce these bugs)
- Multicolumn outer border: removed via `.multicolumn .multicolumn-list__wrapper { border: none !important; }`
- Multicolumn side padding: removed via `.multicolumn .multicolumn-card__wrapper { padding-left: 0 !important; padding-right: 0 !important; }` (top/bottom untouched)
- Inter-card divider lines (.border-item .multicolumn-card::before / .border-item::after): already fixed separately, don't confuse with the outer-border fix above
- Mobile CTAs (≤749px), sitewide via `.button--cta` in modus-design-system.css: full width, 48px min-height, no radius, centered (the Rich Text + CTA look). snippets/button.liquid adds the class whenever rendered with `layout:`; hand-written section CTAs carry it in markup. New sections with their own `<a class="button">` CTA must add `button--cta`; don't write per-section mobile button-width CSS. If a wrapper shrink-wraps the button, add it to the wrapper list in the same rule.
- Product-card collection badge (`.card__collection-title`, "show collection name"): styled ONCE in modus-design-system.css (orange Antonio uppercase tag, line-height 1.4). Don't restyle it per section; section-scoped `.subtitle` rules must exclude it with `:not(.card__collection-title)` (it also carries the `subtitle` class).
- @import for Antonio Google Font in modus-design-system.css MUST be the literal first rule in the file (CSS spec requirement) — any edit near the top of this file must verify @import still comes first, this broke silently once already

## Dead/orphaned files (do not edit, don't assume they're live)
- assets/modus-iwt-spacing-fix.css — superseded, dead
- assets/modus-paragraph-global.css — superseded, dead
- sections/image-with-text-OLIO-PATCH-placeholder-not-used.liquid — harmless orphan, renders nowhere
- templates/page.journal.json IS legitimate (not dead — confirmed separate real page from blog.journal.json, has its own documented CTA banner content)
