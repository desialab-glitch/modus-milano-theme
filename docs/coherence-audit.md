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
- [x] T1.8 (all shared-CSS labels, blog pills, contact consent, article date, fornitori pills/CTA/filter, ambasciatore body done; product badge 10px = D6; 2026-09-25 last batch: popup disclaimer 12→13px, store-map popup address 12→13px and card eyebrow 11→13px, featured-blogs tag badge 11→13px, grid-banner secondary text 10→13px. Breadcrumbs/footer/copyright were already 13px in MDS; timeline/awards descriptions are 13px = at the floor. Exception: store-map pin number.) Text below 13px on mobile: tag pills 11px (blog cards, article), breadcrumb 11px, footer links 12px + copyright 11px, blog filter pills 10.5px, contact consent 12px, article date 12px, fornitori pills 10.6px + CTA 11px, fornitori filter name 12.25px desktop, ambasciatore body 13px, timeline/awards descriptions 13px, store-map lines 13px, popup disclaimer.
- [x] T1.9 Slideshow description text dark grey on orange/photo slides (scheme "background-2" doesn't exist → falls back to light scheme). → cream text on slides.
- [x] T1.10 Two-button gaps: 1rem / 8px / 0 → `--modus-space-xs`; grid-banner 2-button cards stack full width on mobile (Pizzerie, dove-ritiri).
- [x] T1.11 Side gutters not from `--main-padding`: fornitori-filter (40/16px), fornitori-list text (56/24px), related articles (20px on desktop), divider block (50px), article header (+24/32px inset), slideshow tablet (30/60px), CTA wrappers outside `.container` (product recommendations, popular products, simple slider, grid-banner type1).
- [x] T1.12 Desktop side-by-side gutters → `--modus-space-column` (40px): hero-split 32, featured-product 32, FAQ image layout 32, slider-with-info 58–98, sdp-bridge 108, ambasciatore 48, awards 152, video-with-text 32.
- [x] T1.13 `[class*="badge"]` 12px margin hitting inline pills (article meta, article cards, cart subtitles).
- [x] T1.14 Logo tickers pulled wider than the screen (brands, gallery block): fade edges half off-screen.

## Tier 1b — hardcoded section spacing → editor settings (values chosen to match today as closely as possible)
Editor padding/margin settings silently do nothing or don't exist here.

- [x] (product page: forced 40/60px CSS removed, all 80 product templates now use editor settings M top / L bottom — client, 2026-09-25) Timeline (64px), Awards (64px), Ambasciatore (40/24), SDP bridge (72/48), Slideshow (60/80px, padding settings dead), product page `[id^="MainProduct-"]` (40/60px, settings ignored), gallery block ID rule (24px + 30px), newsletter block (60/36px), fornitori filter (32/24), main-page title/body (20px + 32/64px), cart (32/68px), 404 (40px), hero-section content padding.
- [x] (stale settings from the removed pickers are now gone from all templates) AI blocks: add top/bottom spacing selects using the same tokens; replace colour pickers with the page colour scheme. → Newsletter (padding M/M = unchanged, colour scheme instead of background picker, standard eyebrow, xs rhythm, `button--cta`), Gallery (20px px margins → S token padding, colour scheme drives background + fade), Divider (picker → brand gold / subtle). Disabled/unused AI blocks listed in design-system.md.

## Tier 2 — design decisions for the client
- [x] D1 Footer menu columns are hidden below 1150px (only logo + store info on mobile/tablet). Show them? (verify in browser first) → DECIDED: show the footer menus on mobile/tablet.
- [x] D2 Long centered text on mobile → left: IWT-2 "type1" on 21 PDPs (whole block centered), collection.json hero paragraph (311 chars), type1 section headers on mobile, basic page titles. → DECIDED: never centred text — left-aligned everywhere, including text over images (hero, slideshow, banners) and section titles. Only button labels stay centred inside the button.
- [x] D3 FAQ: title tracking 0.12em and questions 23px → standard H2/H3 styles? → DECIDED: FAQ uses the standard heading styles (questions = standard H3).
- [x] D4 Hero section heading 58px vs Hero Split 44px on desktop — which? → DECIDED: all hero headings use the homepage hero size on desktop.
- [x] D5 (no change needed: section H3s already orange, beige on orange scheme; dark green scheme: headings stay beige (client, 2026-09-25)) Headings using H3 (orange) where a section title H2 (gold) is expected: collection carousel, partner logos, timeline, slider with info (2 pages), newsletter popup, basic page title. → DECIDED: keep H3 tags. Rule: H3 is always orange; on the orange scheme always beige.
- [x] D6 Product badges/tags size (10px, below the 13px floor): 12px, 13px, or keep. → DECIDED: 12px (documented exception to the 13px floor, uppercase badge).
- [x] D7 Orange Image with Text (11 collections): image inset an extra 32px each side (framed look) → align to gutter? → DECIDED: align the orange Image with Text image to the gutter (no extra frame).
- [x] D8 Video with Text on desktop: text centered and spread over the full video height → left-aligned, vertically centered like Image with Text? → DECIDED: Video with Text always left-aligned and vertically centred like Image with Text. Mobile: images/videos fill the full content width (between the 20px margins, aligned with the text), text too.
- [x] D9 Product description: italic or normal? (today <p> normal, lists italic — inconsistent) → DECIDED: normal (not italic).
- [x] D10 Blog "load more" button: make it a standard button (full width on mobile)? → DECIDED: standard site button (secondary), full width on mobile.
- [x] D11 Two logo tickers look different → DECIDED: all tickers (awards strip, partner logos, chi-siamo photo strip) stop at the content gutters with the same fade edges.
- [x] D12 Hardcoded "orange" variants (Simple Slider, Image with Text) → replace with the orange colour scheme so there's one orange look. → DECIDED: one orange only — hardcoded orange variants replaced by the orange colour scheme. DONE: Image with Text, Image Text Grid, Simple Slider "Color variant: Orange" and Slideshow "Orange background" slides now just switch the section/slide to the orange scheme; their own orange CSS (colours, 70% eyebrows, button/dot overrides) is gone. Scheme-level rules added once in modus-design-system.css for text buttons and slider dots. Visible differences: eyebrows full beige instead of 70%; mobile orange Image with Text loses the extra 32px of orange under the image (section padding setting applies). Simple Slider keeps its margins painted orange (it has no padding settings). Settings kept (templates untouched) with an info line.

## Content / configuration (not CSS — flagged for the client, not changed)
- [x] product.prodotti-freschi copy vs tov.md — FIXED 2026-09-25: slide heading → "Un rituale di ogni settimana."; "Zero intermediari…" sentence removed; menu tile → "Ogni settimana una selezione diversa, che segue la stagione e il meglio di quello che il Cilento produce. Tutto viene preparato il venerdì e tenuto in fresco fino al ritiro." (facts from the page's own FAQ); gastronomie cards: PRENOTA removed, MAPPA now links to Google Maps for the address printed on each card.
- Password page (only if password protection is enabled): centred layout; modus-design-system.css not loaded there.
- Judge.me cards carousel has "show sample reviews" ON on 55 product templates → may show fabricated reviews. Verify and turn off.
- Newsletter popup promises a gift / discount code by email → verify the discount + automation exist.
- [x] "Contattaci" button inside "Spedizioni e resi" had no link (29 product templates) — FIXED: links to the Contatti page (shopify://pages/contatti).
- Product popups "Details" / "Care" enabled with empty text on 8 product templates; popup labels in English.
- Article sticky CTA "Scopri i prodotti" never renders (block needs an image).
- Tabs (Olio, Vini): full sentences in the subheading field render as an italic eyebrow → belong in description.
- Slider with Info on Pizzerie: 2 empty image slides show placeholders.
- [x] Cart page: English "Shop All" with empty link → "VEDI TUTTI I PRODOTTI" → /collections (same as product pages). Cart UI strings all come from locales/it.json (store primary language it; en installed but unpublished — when English is published, the same keys come from en.default.json and section texts get translated in Translate & Adapt, so no hardcoded Italian was added). Three machine-translated cart strings fixed in it.json: Aggiorna, Rimuovi, Istruzioni per l'ordine. Still marketing-y and unsourced in it.json: cart empty-state "Non perdere le migliori offerte!…" — flag for client.
- Colour scheme "background-2" referenced by many sections but doesn't exist.
- Password page doesn't load modus-design-system.css (only matters if password protection is enabled).
- Rich Text + CTA second button never renders (parameter names).
- Product recommendations CSS for grid mode never loads (malformed tag).

## CSS clean-up (only provably dead / redundant code removed, no visual change)
- [x] Batch 1: per-section `.section-header__title-item { gap: 0 }` in collection-carousel, events-carousel, tabs, simple-slider (duplicates the sitewide `!important` rule; every title-item comes from snippets/section-header.liquid inside `.section-header__line`); list-collections' `gap: var(--modus-space-xs)` (always lost to that rule); tabs' mobile `.section-header__btn-top` margin (identical to the sitewide rule).
- [x] Batch 2 (modus-design-system.css): selectors whose classes exist in no Liquid file and no JS asset — `.tabs__tab`, `.footer__heading`/`.footer__block-heading` rule, `.footer__inner`, `.footer__divider`, `.footer__copyright-content`, `.footer__heading-link` (rule entry only; the `:not()` guard stays), `.footer__block--store-info` entries, `.breadcrumb__sep`, `.product__submit`, `.product-form__payment-info`, `.product__trust-row`, `.rich-text-section .rich-text__content/.rich-text__cta`. Selector-list entries removed only; the remaining selectors in each list are unchanged.
- Kept on purpose (not provably dead): popular-products mobile header margin patch (also zeroes top/bottom margins), products-grid header padding (its padding-top 0 still applies), product-picks mobile CTA move (deliberate behaviour).

## Final verification, one section at a time (2026-09-25)
Static check of all 46 section types in use + the 3 AI blocks against the 9-point checklist at mobile / tablet / desktop (code + real template settings; the storefront could not be rendered from this environment, so the "visual check" items still need a look in the browser). `[v]` = passes the checklist (after fixes where noted), `[!]` = open, needs a decision or content.

**Fixed in this pass** (all uploaded to the draft, checksums verified):
- grid-banner: text-only cards (231 blocks incl. all 80 PDP "La filiera in dettaglio" grids, prodotti-freschi, dove-ritiri) no longer render a placeholder image box.
- image-with-text-2: no placeholder when a PDP has no producer image (17 PDPs) — text uses the full width; logo → heading 24 → 12px; text → stats 28 → 12px; type1 image block gap 32 → 16px at every width.
- popular-products: renders nothing on the storefront when no products are picked (cart page showed 2 placeholder cards); card descriptions 15 → 16px (also products-grid).
- collapsible-content: no placeholder in the image column; header → FAQ list no extra 32px in image layout; question → answer 12px once (was 22px + 12px under closed rows).
- collection + event cards image → title 24 → 16px; event date → title 4 → 12px.
- partner-logos-grid: heading margin no longer stacks on the gaps (28/52/24px → 16/16/12px); desktop gutter token.
- tabs: tab titles (H3) orange (were gold); eyebrow → title 16 → 12px; no empty 12px under the text.
- slideshow: eyebrow line-height 1 → 26px; orange slides: eyebrow full beige, description beige #faf1e4.
- hero-split: tablet column gap 30 → 40px; orange-scheme eyebrow full beige (was 80%).
- simple-slider eyebrow 14 → 15px. multicolumn / slider-with-info: no trailing empty margin. Contatti channel H3s orange (were green via the .h4 size class).
- featured-product: description → price 8 → 12px, add to cart → "Vedi di più" 24 → 12px.
- store-map: button gap 20 → 12px, card eyebrow standard grey; contact-form: no stray divider/padding under the form.
- fornitori-list: mobile image no longer overflows the right gutter; section/gutter/gap tokens (desktop outer gutter = main padding, image side = column gutter, 12px rhythm). fornitori-filter: no 1400px cap, wrap mode left-aligned.
- awards: heading → logos 24 → 12px. sdp-bridge body 15px/1.73 → 16px/1.6. modus-related-articles: header rhythm (18/36 → 12/24px), CTA left, empty subheading/heading guarded.
- main-article header: title → excerpt and excerpt → meta 16/20 → 12px; share links 12.6 → 13px. Search + 404 inputs 12 → 14px; search result labels in eyebrow grey.
- product page: title → price 20 → 12px; stacked media → info 32 → 16px (<990). Header: cart icon no longer 14px further in than the gutter (<1150). Menu drawer account links 12 → 13px.
- type1 header CTAs ("VEDI TUTTI I PRODOTTI" under product recommendations, grid-banner, popular products) left-aligned instead of centred.
- cart: max-width 1200 cap removed (aligns with the gutters); empty-cart rhythm 12px; discount + error lines 12 → 13px. Popup small print now actually 13px italic grey (the sitewide paragraph rule used to win).

**Result per section** — [v] ambasciatore · awards-modus · banner · brands · collapsible-content · collection-carousel · contact-form · events-carousel · featured-blogs · featured-product · fornitori-filter · fornitori-list · footer · grid-banner · header · hero-section · hero-split · image-with-text · image-with-text-2 · main-404 · main-blog · main-cart · main-list-collections · main-page · main-product · main-search · modus-related-articles · multicolumn · partner-logos-grid · popular-products · popup · product-picks · product-recommendations · products-grid · rich-text-cta · sdp-bridge · simple-slider · slider-with-info · slideshow · store-map · tabs · timeline-modus · video-with-text · AI newsletter · AI gallery ticker · AI divider. (main-article: [v] except the desktop item below.)

**Open — needs a decision or a browser check** (not changed):
- [!] main-article (desktop, article with image): image → title gap is 0 and the title starts 32px left of the body column. Needs a visual check before changing the layout.
- [!] main-product (desktop): the buy column is centred inside its half (max 412px) → ~160px between media and text at 1440px. Moving it next to the media (40px gutter) changes the PDP layout noticeably — client decision.
- [x] Blog cards unified on the homepage style (client, 2026-09-25): excerpt 16px/1.6 text colour, date = standard 15px eyebrow, everywhere (journal, search, related articles).
- [!] collection list page: cards sit with no horizontal gap between them (template-collection-list.css sets none) — check in the browser.
- [!] newsletter AI block on mobile: ends flush with its image (no bottom padding), next section starts 12px later — intended?
- [!] fornitori-list "Scopri" link is a text link, not a full-width CTA on mobile; location line uses line-height 1.1 (can wrap on mobile) — keep as design details or standardise?
- [!] ambasciatore highlight box text 14px (callout, below the 16px body size); awards mobile marquee uses its own 32px fade instead of the shared ticker fade (D11).
- [!] products-grid / popular-products card descriptions now 16px (were 15px) — confirm visually on the collection grids.
- [!] slider-with-info pagination may be a 10px number counter (JS not inspectable here); simple-slider on sott-olio uses a 55% image width on desktop (looks deliberate).
- [!] rich-text-cta "In tre passi" (no text/button): 12px under the heading may be doing the job of the gap to the next section — check before removing.
- [x] Empty-cart copy (it.json): "Il tuo carrello è vuoto. Esplora i prodotti dei nostri produttori del Cilento e scopri il mondo Modus." + button "Esplora i prodotti" (cart page, cart drawer, account page); the unused "Non perdere le migliori offerte!" strings rewritten too.
- [x] The 17 PDP templates without a producer image are NOT assigned to any product (dead duplicates: cavatelli, erba-luisa, farina-*-caputo, farina-*-marino, fusilli-cilento, kleos-aglianico, kratos, lagane, le-ghiandaie, limoncello, piscriddi, spaghettone, thumos, valentina; live products use pasta-*/vino-*/liquore-* templates). Nothing to fill; candidates for deletion (client decision). Some also hold wrong producer data (le-ghiandaie → Frantoio Muraglia, piscriddi → Pastificio Cilento).
- [x] Cart "Altri prodotti dal Cilento": automatic fallback (client, 2026-09-25) — popular-products with no picked products shows up to 8 available products from the whole shop (no gift card, no Prodotti Freschi, nothing already in the cart). Picked products still win. Order = the shop's default product order (Liquid can't sort by sales).
- [!] collection.json (generic collection template) FAQ image layout has no image.
