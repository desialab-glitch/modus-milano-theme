# Modus Milano — Theme State & Known Issues

## Current theme roles (verify before any push — these have changed before)
- "Modus Final" (160332644566): UNPUBLISHED DRAFT, holds all current collection-page and copy edits. This is what gets pulled/edited.
- "Copy of Modus Final" (166528450774): LIVE / MAIN. Never push, publish, delete, or dev against this one.
- Two other unpublished drafts exist (163520118998, 166528450774 dupes) — confirm which is which before touching any theme ID that isn't the two above, IDs get reused/duplicated in this project's history.

## Known live bugs, not yet fixed (check before assuming these are new findings)
- Gift Card product: all 4 variants (€30/50/75/100) show sold out, unpurchasable
- Conserve collection: both products (Passata pomodoro biologico, Pomodoro pelato biologico) priced at €0,00
- ~~Conserve producer bio (Maida) still contains the revoked phrase "Nessun intermediario, solo la terra e il momento giusto" live~~ — checked 25 Sep, not present in the live `templates/collection.conserve.json`. Stale, resolved.
- "Modus nella stampa" homepage block pulls the 4 most recent Journal posts automatically instead of 4 curated press articles (Pignataro/De Gustare/Gambero Rosso/ScattiDiGusto) — article_block settings are empty, likely misconfigured
- Formaggi article "formaggi-cilentani-caciocavallo" has literal "test" as its entire body — placeholder, not real copy
- Gastronomie's Prodotti Freschi / menu settimanale button has no real link yet (link is coming)

## Open questions, unresolved
- Whether Cammarano flours are used in pizzeria dough or only Coltivatori Custodi ancient grains (asked to Simona, 24 Sep) — until answered, Pizzerie page keeps grani antichi dei Coltivatori Custodi; Farine collection stays limited to the 2 Cammarano products only

- **For Simona (open, 25 Sep): which Madonna dell'Olivo oil do we sell?** The product sheet ("E Commerce new SDP", row 50) only says "Olio EVO -", 500 ml, €23, producer "Madonna dell'Ulivo". The producer makes separate single-cultivar oils (Rotondella, Carpellese, Itrana, Ravece). Until confirmed, the product text names no cultivar, and the image may not match the oil we sell.

## Open fact questions from the 25 Sep copy condense (kept as is or hidden, need a source)
- Third gastronomia: "Portanuova" (contatti) vs "via Pirelli" (gastronomie)
- Prodotti Freschi page: hero promises 48h shipping of conserve/vini/olio on a pickup-only page; "tre prodotti" vs 3/4/5 portions; pickup "lunedì a sabato" vs Corso Como Tue–Sun; unverified "Presìdi Slow Food, DOP, bio" tile and "Il primo punto Modus"
- Pelato CARATTERISTICHE says "San Marzano" grown in Capaccio Paestum — check Maida's wording (the San Marzano DOP area is elsewhere)
- Fusilli (Terra Dura): Senatore Cappelli called a "grano antico locale"; "Trafila: bronzo" on a hand-rolled fusillo
- Lagane: "il formato più antico del Cilento" (unverified superlative); "taglio a mano" vs "trafilatura al bronzo"
- Erbe: FAQ heading "Biologiche certificate" with no certification named; the video block about Nicola Di Novella's minestra sits on the Erbe Cilento page
- Formaggi: health claims (pregnancy, lactose) with no source; ripening "circa 15 giorni" vs "tra 10 e 15 giorni"
- Paolo: learned leavening from his nonna (pizzerie) vs kneaded with his madre (chi-siamo)
- Vini: Kleos serving advice differs between pages; order-change window "2 ore" (kleos, valentina) vs "1 ora" elsewhere; Piscriddi serving temperature 16–18 °C vs 14–16 °C
- Soppressata "l'unico salame lardellato della Campania" — check against the Slow Food Presidio page. **Status split (25 Sep):** already removed from `product.soppressata-di-gioi.json`, but still present on `collection.salumi.json` (practical grid, "LA SOPPRESSATA LARDELLATA" column) — same claim, two different states on two pages about the same product. Needs one decision applied to both.
- Aura (tonno): removed "pescato artigianalmente" from the live/enabled banner text on both tuna product templates. Still present, unconfirmed, in the DISABLED comparison FAQs on `product.tonno-di-palinuro-ala-lunga` (pfaq-2) and `product.tonno-di-palinuro-rosso` (pfaq-4) — flagged for priority when the 20 hidden comparison FAQs (below) are cleaned up, since re-enabling either FAQ as-is would reintroduce the unconfirmed claim.
- **New (25 Sep): `product.infilatella-classica` banner_0** has "È la forma più antica di questa conserva" — unverified superlative, not sourced anywhere else on that page.
- Confirmed orphaned/dead product templates (verified via live product query, not just filename): product.kratos, product.valentina, product.thumos, product.kleos-aglianico, product.le-ghiandaie, product.piscriddi, product.lagane, product.cavatelli, product.fusilli-cilento, product.spaghettone, product.erba-luisa, product.limoncello, product.farina-cuoco-caputo, product.farina-enkir-marino, product.farina-nuvola-caputo, product.farina-pizzeria-caputo, product.farina-tipo-00-marino (the Caputo/Marino farina templates don't even exist as theme files anymore — only product.farina-di-grano-duro and product.farina-integrale-di-grano-duro are live). Candidates for deletion once confirmed.
- 20 product-comparison FAQs are hidden (disabled, not deleted) on the product templates, per the ToV no-comparison rule. Checked 25 Sep: every comparison FAQ found (ALFA/CRUX/IDRA/RISERVA, candele-corte, infilatella noci/mandorle, both tonno templates) is already disabled — none are live, so no active violation, but they still need actual deletion rather than just disabling.

## Whole-page redundancy review (25 Sep) — status
All 12 remaining collection pages and all 77 product templates were re-read as whole pages (not section-by-section) against docs/tov.md, on the draft theme only. Backups of every pre-edit file are in `theme-backups/2026-09-25-collection-page-rebalance/` and `theme-backups/2026-09-25-product-whole-page-review/`.
- **Collections, edited:** conserve, erbe, farine, formaggi, pasta, prodotti-da-forno, salumi, sott-olio-e-sotto-sale (cross-section repetition removed; 2 banned product-comparisons fixed on pasta/sott-olio-e-sotto-sale; 2 banned negative-claim constructions fixed on erbe/salumi).
- **Collections, no change needed:** fichi, legumi-e-cereali, liquori, vini.
- **Note:** products-grid/card descriptions on these 12 collections run 190–300+ characters, matching the olio/miele reference pages — NOT the 110–125 target stated elsewhere in docs/tov.md for "collection card descriptions". This is an unresolved inconsistency between the stated rule and the actual reference pages; nobody has reconciled it, don't force a trim without deciding which is right.
- **⚠️ Concurrent editing detected 25 Sep:** while the collections review was running, someone/something else was actively editing collection.conserve.json, collection.erbe.json and collection.farine.json on the draft theme in real time via the theme editor. Handled safely (re-fetch + re-verify checksum before every write) but means the draft theme is not exclusively under this workflow's control — check for further live edits before trusting any cached copy.
- **Products, edited:** 35 of 77 templates (19 in one batch, 16 in another) — same pattern each time: an `image_with_text_2` block added by an earlier section-by-section pass restated facts already given in the banner grid above it, sometimes 3–4 times on one page (e.g. product.riserva's awards list). Trimmed to remove the duplication, kept the fact once.
- **Products, no change needed:** 24 templates (already non-redundant, no banned constructs).
- **Products, orphaned/skipped:** 17 templates, see the confirmed-dead list above.

## Source of truth for product data
Google Drive sheet "E Commerce new SDP.doc (1).xlsx" (file id 1KKqGowF2Z6dYwtvR5Iy0yGESnbMqY7OU), tab "Margine" — weights, sale prices, purchase prices, producers. Margin figures on that sheet are internal only, never flag or question them. A price of 0 is worth flagging; any non-zero price on that sheet is treated as correct.
