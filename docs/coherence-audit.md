# Section coherence audit — 2026-09-25

Read-only audit of all 54 section types in use + the 4 AI blocks on the draft theme "Modus Final" (160332644566), against the per-section checklist in docs/design-system.md. Findings below are grouped by how they get fixed. Each fix is applied on the draft only, with a backup in theme-backups/ first. Status: `[ ]` open, `[~]` partly done, `[x]` done, `[?]` needs decision, `[v]` verified in the final pass.

Already fixed during the audit (2026-09-25): mobile CTAs full width (`.button--cta`), section spacing tokens, collection badge line-height + single rule, product tags as badges, orange-scheme eyebrows beige everywhere, Video with Text mobile layout, newsletter block mobile gutter, Fornitori filter mobile text size.

## Tier 1 — shared fixes that bring sections in line with the approved checklist
No design decision needed; each restores the documented rule.

- [x] T1.1 Section header (snippets/section-header.liquid, used by ~15 section types): eyebrow→heading→description is 18px (base flex gap 0.6rem + 12px margins), 24px in list-collections. → `.section-header__title-item{gap:0}` sitewide; remove list-collections' own gap.
- [x] T1.2 Section header → content gap: hardcoded 20px + heading margin = 32px without description, 20px with. → one token (`--modus-space-m`, 24px) and last child margin 0. Simple Slider's own 36px override removed.
- [x] T1.3 Type2 header CTA on mobile/tablet: description touches the button (0 gap) e.g. Popular Products on Pizzerie; Featured Blogs uses 24px. → `--modus-space-xs` everywhere (<990).
- [x] T1.4 Image with Text + Image with Text 2 (<990): image↔text gap doubled to 32px (56 PDPs) and eyebrow→heading→text 16px. → gap `--modus-space-s` once, text rhythm `--modus-space-xs`.
- [x] T1.5 Empty wrappers adding space: IWT-2 empty stats block (+28–32px, ~40 PDPs), slideshow button div with no button (+64px on mobile, PDP recipes), grid-banner cards without buttons (+12px), empty `.section-header_btn` (+32px), Slider with Info empty text block, FAQ last item (+24px), product popup empty image div.
- [x] T1.6 Eyebrow colour: generic rule sets no colour, so some eyebrows render full dark; others hardcode #4d4d4d / opacity .8 / .5 / .7. → sitewide default rgba(61,61,61,.6) on light schemes (dark + orange schemes keep their overrides); remove per-section eyebrow colours.
- [x] T1.7 Body paragraphs at line-height 1.6: IWT (23px), Simple Slider items (23px), section-header description (23px), Hero section (1.4), main-page body (14px/1.75), featured-product description (14px/1.4), 404 intro.
- [~] T1.8 (all shared-CSS labels, blog pills, contact consent, article date, fornitori pills/CTA/filter, ambasciatore body done; product badge 10px = D6) Text below 13px on mobile: tag pills 11px (blog cards, article), breadcrumb 11px, footer links 12px + copyright 11px, blog filter pills 10.5px, contact consent 12px, article date 12px, fornitori pills 10.6px + CTA 11px, fornitori filter name 12.25px desktop, ambasciatore body 13px, timeline/awards descriptions 13px, store-map lines 13px, popup disclaimer.
- [x] T1.9 Slideshow description text dark grey on orange/photo slides (scheme "background-2" doesn't exist → falls back to light scheme). → cream text on slides.
- [x] T1.10 Two-button gaps: 1rem / 8px / 0 → `--modus-space-xs`; grid-banner 2-button cards stack full width on mobile (Pizzerie, dove-ritiri).
- [ ] T1.11 Side gutters not from `--main-padding`: fornitori-filter (40/16px), fornitori-list text (56/24px), related articles (20px on desktop), divider block (50px), article header (+24/32px inset), slideshow tablet (30/60px), CTA wrappers outside `.container` (product recommendations, popular products, simple slider, grid-banner type1).
- [ ] T1.12 Desktop side-by-side gutters → `--modus-space-column` (40px): hero-split 32, featured-product 32, FAQ image layout 32, slider-with-info 58–98, sdp-bridge 108, ambasciatore 48, awards 152, video-with-text 32.
- [x] T1.13 `[class*="badge"]` 12px margin hitting inline pills (article meta, article cards, cart subtitles).
- [x] T1.14 Logo tickers pulled wider than the screen (brands, gallery block): fade edges half off-screen.

## Tier 1b — hardcoded section spacing → editor settings (values chosen to match today as closely as possible)
Editor padding/margin settings silently do nothing or don't exist here.

- [ ] Timeline (64px), Awards (64px), Ambasciatore (40/24), SDP bridge (72/48), Slideshow (60/80px, padding settings dead), product page `[id^="MainProduct-"]` (40/60px, settings ignored), gallery block ID rule (24px + 30px), newsletter block (60/36px), fornitori filter (32/24), main-page title/body (20px + 32/64px), cart (32/68px), 404 (40px), hero-section content padding.
- [ ] AI blocks: add top/bottom spacing selects using the same tokens; replace colour pickers with the page colour scheme.

## Tier 2 — design decisions for the client
- [x] D1 Footer menu columns are hidden below 1150px (only logo + store info on mobile/tablet). Show them? (verify in browser first) → DECIDED: show the footer menus on mobile/tablet.
- [ ] D2 Long centered text on mobile → left: IWT-2 "type1" on 21 PDPs (whole block centered), collection.json hero paragraph (311 chars), type1 section headers on mobile, basic page titles. → DECIDED: never centred text — left-aligned everywhere, including text over images (hero, slideshow, banners) and section titles. Only button labels stay centred inside the button.
- [x] D3 FAQ: title tracking 0.12em and questions 23px → standard H2/H3 styles? → DECIDED: FAQ uses the standard heading styles (questions = standard H3).
- [x] D4 Hero section heading 58px vs Hero Split 44px on desktop — which? → DECIDED: all hero headings use the homepage hero size on desktop.
- [x] D5 (no change needed: section H3s already orange, beige on orange scheme; dark green scheme: headings stay beige (client, 2026-09-25)) Headings using H3 (orange) where a section title H2 (gold) is expected: collection carousel, partner logos, timeline, slider with info (2 pages), newsletter popup, basic page title. → DECIDED: keep H3 tags. Rule: H3 is always orange; on the orange scheme always beige.
- [x] D6 Product badges/tags size (10px, below the 13px floor): 12px, 13px, or keep. → DECIDED: 12px (documented exception to the 13px floor, uppercase badge).
- [ ] D7 Orange Image with Text (11 collections): image inset an extra 32px each side (framed look) → align to gutter? → DECIDED: align the orange Image with Text image to the gutter (no extra frame).
- [ ] D8 Video with Text on desktop: text centered and spread over the full video height → left-aligned, vertically centered like Image with Text? → DECIDED: Video with Text always left-aligned and vertically centred like Image with Text. Mobile: images/videos fill the full content width (between the 20px margins, aligned with the text), text too.
- [x] D9 Product description: italic or normal? (today <p> normal, lists italic — inconsistent) → DECIDED: normal (not italic).
- [x] D10 Blog "load more" button: make it a standard button (full width on mobile)? → DECIDED: standard site button (secondary), full width on mobile.
- [x] D11 Two logo tickers look different → DECIDED: all tickers (awards strip, partner logos, chi-siamo photo strip) stop at the content gutters with the same fade edges.
- [ ] D12 Hardcoded "orange" variants (Simple Slider, Image with Text) → replace with the orange colour scheme so there's one orange look. → DECIDED: one orange only — hardcoded orange variants replaced by the orange colour scheme.

## Content / configuration (not CSS — flagged for the client, not changed)
- Judge.me cards carousel has "show sample reviews" ON on 55 product templates → may show fabricated reviews. Verify and turn off.
- Newsletter popup promises a gift / discount code by email → verify the discount + automation exist.
- "Contattaci" button inside "Spedizioni e resi" has no link on 20 product templates.
- Product popups "Details" / "Care" enabled with empty text on 8 product templates; popup labels in English.
- Article sticky CTA "Scopri i prodotti" never renders (block needs an image).
- Tabs (Olio, Vini): full sentences in the subheading field render as an italic eyebrow → belong in description.
- Slider with Info on Pizzerie: 2 empty image slides show placeholders.
- Cart page recommendations: English "Recommended" / "Shop All", Shop All link empty.
- Colour scheme "background-2" referenced by many sections but doesn't exist.
- Password page doesn't load modus-design-system.css (only matters if password protection is enabled).
- Rich Text + CTA second button never renders (parameter names).
- Product recommendations CSS for grid mode never loads (malformed tag).
