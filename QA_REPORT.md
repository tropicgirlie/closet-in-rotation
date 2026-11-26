# Synthetic wardrobe QA — 26 November 2026

This run used isolated Chromium browser profiles against the public GitHub Pages site, followed by the updated local site. It did not alter a person's saved wardrobe. The synthetic persona owns seven colour-led winter pieces across FARM Rio and Zimmermann: two dresses, two tops, two layers, and trousers. Seven garment photos were temporarily downloaded from the product pages already linked in the editorial. The images and synthetic backup are test-only files outside this repository.

## Tested flows

| Flow | Result |
| --- | --- |
| Open all four main views | Passed |
| Upload seven real garment photos; save name, category, colour, brand, price, fibre and season | Passed; seven stored items and seven rendered photos |
| Search and filter the closet | Passed |
| Open item detail and log a wear | Passed |
| Generate a colour-led outfit; change occasion, mood and manual weather; reroll and log it | Passed |
| Review synthetic share, cost per wear and circular guidance | Passed |
| Save, find and remove a style muse | Passed |
| Use FARM Rio and brand styling shortcuts | Passed |
| Read text from a real product-page screenshot | Passed; OCR suggested a partial name and category, requiring review |
| Export a backup and restore it in a second isolated browser profile | Passed, including all seven photos |
| Check each view at a 390 px mobile width | Passed without horizontal overflow |
| Reload the app shell offline after service worker activation | Passed |
| Check for uncaught browser exceptions | None |
| Edit price, opt to retain a product screenshot as an item photo, keep a receipt screenshot private by default, and delete a piece | Passed on local update |
| Choose tonal, contrast and accent mixing from the colour wheel | Passed on local update; contrast selected a green jacket with red trousers, tonal selected a pink knit with red trousers |
| Load editorial product images | All seven loaded in the browser |
| Use device location to request current weather | Passed with a synthetic Dublin location |
| Update a piece in one tab and see it in another tab in the same browser | Passed on local update |
| Update a style muse in one tab and see it in another tab in the same browser | Passed on local update |
| Display the white editorial page and border-free runway and closet cards at desktop and 390 px widths | Passed on local update; no mobile overflow |
| Scroll through four real runway photographs on mobile | Passed; all four loaded |

## Findings

- Wardrobe photo cards stretched their images beyond the visible tile and cropped garment details. The local update now constrains photos inside the tile.
- Purchase screenshots used for OCR were always discarded as photos. The local update offers an explicit **Keep this image as the item photo** choice; it is off by default because receipts can contain personal details.
- The wheel originally chose only a shade. The local update adds tonal, contrast and accent mix actions using saved pieces.
- The prior cream page and bordered runway cards crowded the editorial. The local update uses a white gallery background, removes the coloured lines above garment descriptions and drops card outlines while preserving colour in the garments, wheel and small accents.
- A follow-up refinement puts quiet colour washes inside the runway image panels and style-code cards. It removes the remaining top rules and allows saved garment names to occupy two lines on mobile.
- Same-browser tabs now update when a piece or style muse changes. There is no account or cloud sync across devices. Export/import moves data between browser profiles but replaces the destination closet. A sync backend and a deliberate migration flow are still required.
- OCR extracts visible text, not garment attributes. The tested product screenshot yielded a partial name and category, while price and fibre were unavailable. Users must review fields before saving.
- Automatic link checks returned rate limits for two FARM Rio pages and a bot response for Dior; their status in a normal browser was not established by those requests. The other tested editorial and source pages returned successfully.

The synthetic browser profile is not a user account. Real user accounts and automatic cross-device sync remain unimplemented.
