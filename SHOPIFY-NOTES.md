# Iron Bear Leather — porting this prototype to Shopify

He already runs Shopify at ironbearleather.com, so this is a re-theme, not a migration.
Nothing here needs a headless build — everything maps to sections in a standard
Online Store 2.0 theme (Dawn works fine as the base).

---

## 1. Section-by-section mapping

| Prototype section | Shopify | Notes |
|---|---|---|
| Announcement marquee | Announcement bar section | Dawn's is static; the scrolling version is ~15 lines of Liquid + the CSS from `.ann` |
| Header | Header section | Swap the wordmark for the badge PNG; keep "Redwater, Texas" as the tagline |
| Hero | Custom section `hero-animated.liquid` | Two image pickers + heading/subheading/two button settings. The mask animation is pure CSS, it survives the port |
| Marquee band | Custom section, repeatable blocks | One block = one word |
| Collection scroller | Featured collection section | Set layout to "slider". Replace `PRODUCTS` with `{% for product in collection.products %}`. Price becomes `{{ product.price \| money }}`, the "Coming soon" chip becomes a product tag check |
| The Making | Custom section `the-making.liquid` | Four repeatable blocks, each with image **or** video picker + number + heading + text. The scroll maths in the prototype is self-contained — copy the JS block as-is |
| Iron Bear Standard | Multicolumn section + custom stats block | The count-up is the `[data-count]` script |
| Customers are saying | **Review app** — see §3 | Do not hardcode the reviews on Shopify |
| Tooled purse teaser | Image-with-text section | Set it to "Coming soon" until it's listed |
| CTA band | Rich text section | |
| Bear Den signup | Newsletter section | Wire to Shopify Email or Klaviyo |
| Footer | Footer section | |

## 2. Theme settings to set once

- **Colours:** background `#141110`, secondary `#26201B`, page `#F4EDE2`,
  accent `#C8873F`, green accent `#3E4A3B`. Flat fills only — turn off any
  gradient/overlay-gradient options in the theme.
- **Type:** Headings = Oswald (or the closest condensed the theme offers),
  Body = Barlow. Headings uppercase, letter-spacing ~0.
- **Buttons:** square corners, 2px borders. No border radius anywhere.

## 3. Reviews — important

The six reviews on the prototype are his real published reviews, copied from the live
site so the pitch looks true. **On Shopify they must come from the review app**
(Judge.me / Shopify Product Reviews / whatever is feeding the 4.83 badge now) — not
pasted into a section. Two reasons: the average updates itself, and "Verified" stays
honest. Point the app's homepage widget at the section and restyle it with the CSS
from `.rv` / `.rv-scroller`.

## 4. Products to create / confirm

- Bear Trap — Handmade Full Grain Leather Wallet (exists)
- Bear Trap Slim (exists)
- Tooled Sunflower Purse — create as draft / "coming soon"
- Custom Commission — needs a price and a line-item property form (thread colour,
  leather colour) if he wants to sell custom work directly

Colour variants seen so far: Blue Abyss, brown w/ orange stitch, forest green.
One reviewer asked for a **grey/slate** — worth raising with him, it's free product
research.

## 5. Performance

- Images here are resized to 1400px max and re-encoded. On Shopify use
  `image_url: width: 800` + `loading="lazy"` and let the CDN serve WebP.
- The bench video is 1.7 MB and set to `preload="none"` — it only downloads when the
  stitching stage becomes active. Keep that behaviour; upload it to Shopify Files and
  swap the `src`.
- No JS libraries, so nothing to bundle.

## 6. What is not built yet

Front-end only: cart, product pages, collection pages, search, account, policies.
The prototype is the homepage story. Price the build accordingly.
