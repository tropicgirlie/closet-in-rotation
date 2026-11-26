# Closet, in rotation

A local-first wardrobe companion for putting together outfits from clothes you already own. This builds on the original prototype by Luana Micheau and keeps its `closet-in-rotation-v1` browser storage format. The interface uses a white fashion-editorial canvas so the garments and colour wheel lead the page.

## What it does

- Add pieces from a photo or camera, or start from a receipt, order confirmation, or product screenshot. Images are resized in the browser before saving. A product screenshot can be kept as the item image by explicit choice; receipt screenshots are not retained by default.
- Follow the landing page's three-step walkthrough: choose the intake source, review an item's details, then style and log wears. The item name is required; colour, price, and fibre label improve the insights. A garment photo does not fill fields automatically.
- Read text from purchase images with on-device OCR and suggest item name, category, price, and fibre label. Review the suggestions before saving. OCR downloads Tesseract.js, its worker, and language data on first use; it needs an internet connection then.
- Build an outfit preview from saved pieces using occasion, mood, season, and current weather. Current weather uses device location only after permission and fetches conditions from Open-Meteo. A manual weather choice is available.
- Log wears, see current and projected cost per wear, and review synthetic-fibre percentages parsed from the care label.
- See rough remaining-wear and resale ranges, plus repair, resale, donation, and recycling guidance.
- Export and restore the closet as JSON. Changes appear in other open tabs of the same browser. The app shell is available offline after the first load.
- Explore a sourced seasonal colour wheel, select a shade to see which of your pieces match, then choose a tonal, contrast or accent mix from your saved pieces. The app explains when a matching partner is missing.
- Explore four researched style codes inspired by FARM Rio, Zimmermann, Dior, and Stine Goya. The app interprets each as a way to combine pieces you own and provides an accessory finish plus a lower-cost route. Tag brand names on your pieces to browse them from the corresponding card. These are independent interpretations, not endorsements or product listings.
- See an editorial edit of real FARM Rio clothing, with product photography, source links, fibre and care details, and ways to recreate each idea from your own closet. The winter hero links to the official [Barbour × FARM Rio Fall 2026 campaign on FARM Rio Europe](https://farmrio.eu/pages/barbour-farm-rio-fall-26); its photograph loads from FARM Rio's image CDN. The older generated choosing-a-look illustration is retained as an unused local asset.
- Browse a runway category edit with four real Zimmermann garments: a sculptural dress, a tie-neck shirt with buttoned cuffs, a double-breasted blazer, and tailored trousers. Each links to its original product page, shows its main fabric and care needs, and offers a shortcut to the matching category in your saved closet.
- Save links to women and creators whose style inspires you, with a colour note. These style muses stay in your browser.

## Seasonal colour desk

The current issue lives in [`trends.json`](trends.json). It is a **curated snapshot**, not a live fashion or social-media feed. The Autumn/Winter 2026 issue was curated on 18 November 2026 from [Vogue's Fall 2026 colour report](https://www.vogue.com/article/fall-2026-color-trends), published 21 August 2026. Each colour has a source, a short styling interpretation, and aliases used to match the user's saved item names and colour tags. Selecting a swatch reveals the colour story and matching piece count; its style button gives a matching owned piece priority in the outfit preview. If none is tagged, the app invites the user to add or edit a colour.

For a new issue, replace the season, dates, source link, palette, and aliases in `trends.json`, then review the styling notes against the cited report. Social inspiration is deliberately user-curated: the app does not scrape, track, or claim to follow influencers' accounts automatically.

The brand style codes live in [`brand-codes.json`](brand-codes.json). They are derived from each brand's own description or catalogue, with source links on the cards. The low-cost suggestions begin with rewearing, repairing, or looking secondhand. A lower price or a luxury label is not an environmental or durability score; the item-level estimate considers the fibre label, construction, condition, care needs, and expected use.

The current FARM Rio garment edit lives in [`farm-edit.json`](farm-edit.json). It is a dated selection, not a live product feed. Product photographs load from FARM Rio's image CDN and need a connection; availability and product details can change.

The wordmark, SVG favicon, Apple touch icon, and PWA icons use the same burgundy and ivory monogram. [`ASSET_PROMPTS.md`](ASSET_PROMPTS.md) contains a Midjourney prompt for an original seasonal hero alternative.

The Zimmermann runway examples are a dated editorial selection in `index.html`, not saved wardrobe items or a live catalogue. Their photographs load from Zimmermann's image CDN and need a connection. Fabric details are transcribed from the linked product pages; a luxury label does not establish environmental performance or durability.

## Run locally

Serve the directory with any static server, for example:

```sh
python3 -m http.server 8765
```

Open `http://localhost:8765`. No package installation or account is needed. The site can be hosted on GitHub Pages as it is.

## Privacy and limits

Closet data, photos, and style-muse links are saved in browser local storage and update across tabs in the same browser. They do not sync across devices. Clearing site data removes them, so use **Export closet backup** regularly; the current backup includes pieces and style muses, and the importer still accepts the original array-only format. Photos and purchase images are not uploaded by the app. Purchase screenshots are read in the browser; only confirmed fields are saved, except when you explicitly choose to keep a product screenshot as the item photo. Do not choose this for a receipt containing personal details. Location coordinates are sent to Open-Meteo when you request current weather. Google Fonts and the OCR library are fetched from their respective hosts. The FARM Rio and Zimmermann editorial photographs load from their official sites and need a connection.

Outfit selection and lifecycle guidance use transparent local rules. OCR reads text; it does not understand garment images. There is no generative AI, body-based virtual try-on, live resale appraisal, or brand-reputation database in this version. The outfit preview shows your saved item photos together. Longevity, projected cost per wear, and resale ranges are planning estimates rather than guarantees.

Existing `closet-in-rotation-v1` data loads unchanged. The previous single-file prototype is retained as `legacy-index.html` for reference.

## Data and external sources

- [Open-Meteo forecast API](https://open-meteo.com/en/docs) for current weather.
- [Tesseract.js](https://github.com/naptha/tesseract.js) for browser OCR.
- [Vogue's Fall 2026 colour report](https://www.vogue.com/article/fall-2026-color-trends) for the current seasonal colour issue.
- [FARM Rio](https://farmrio.com/pages/about), [Zimmermann](https://www.zimmermann.com/en-ae/our-story), [Dior Ireland shoes](https://www.dior.com/en_ie/fashion/womens-fashion/shoes/all-shoes-kahoona), and [Stine Goya](https://us.stinegoya.com/pages/about) for the independent brand style codes.
- [Ellen MacArthur Foundation](https://www.ellenmacarthurfoundation.org/the-fashion-remodel/learn) on keeping garments in use through resale, repair, rental, and remaking.
- [Vinted](https://www.vinted.com/how_it_works), [Depop](https://www.depop.com/ie/sell/), and [eBay Ireland](https://www.ebay.ie/sellercentre/seller-update/2025-april/new-conditions-fashion) as example resale destinations. Availability and fees can vary.
- [Citizens Information recycling guidance](https://www.citizensinformation.ie/en/environment/waste-and-recycling/recycling-household-waste/) for checking local textile collection options.

## Licence

MIT. See [LICENSE](LICENSE).
