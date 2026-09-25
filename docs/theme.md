# Modus Milano — Theme State & Known Issues

## Current theme roles (verify before any push — these have changed before)
- "Modus Final" (160332644566): UNPUBLISHED DRAFT, holds all current collection-page and copy edits. This is what gets pulled/edited.
- "Copy of Modus Final" (166528450774): LIVE / MAIN. Never push, publish, delete, or dev against this one.
- Two other unpublished drafts exist (163520118998, 166528450774 dupes) — confirm which is which before touching any theme ID that isn't the two above, IDs get reused/duplicated in this project's history.

## Known live bugs, not yet fixed (check before assuming these are new findings)
- Gift Card product: all 4 variants (€30/50/75/100) show sold out, unpurchasable
- Conserve collection: both products (Passata pomodoro biologico, Pomodoro pelato biologico) priced at €0,00
- Conserve producer bio (Maida) still contains the revoked phrase "Nessun intermediario, solo la terra e il momento giusto" live, despite Notion saying it was cut
- "Modus nella stampa" homepage block pulls the 4 most recent Journal posts automatically instead of 4 curated press articles (Pignataro/De Gustare/Gambero Rosso/ScattiDiGusto) — article_block settings are empty, likely misconfigured
- Formaggi article "formaggi-cilentani-caciocavallo" has literal "test" as its entire body — placeholder, not real copy
- Gastronomie's Prodotti Freschi / menu settimanale button has no real link yet (link is coming)

## Open questions, unresolved
- Whether Cammarano flours are used in pizzeria dough or only Coltivatori Custodi ancient grains (asked to Simona, 24 Sep) — until answered, Pizzerie page keeps grani antichi dei Coltivatori Custodi; Farine collection stays limited to the 2 Cammarano products only

## Source of truth for product data
Google Drive sheet "E Commerce new SDP.doc (1).xlsx" (file id 1KKqGowF2Z6dYwtvR5Iy0yGESnbMqY7OU), tab "Margine" — weights, sale prices, purchase prices, producers. Margin figures on that sheet are internal only, never flag or question them. A price of 0 is worth flagging; any non-zero price on that sheet is treated as correct.
