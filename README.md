# Iron Bear Leather — animated site prototype

Single self-contained page for client presentation. No build step, no dependencies,
no server. Double-click `index.html`.

**Brand:** Iron Bear Leather, Redwater, Texas — handmade full grain leather goods.
Copy and reviews are taken from the client's own material (Facebook graphics and
ironbearleather.com). **Prices are placeholders.**

---

## Files

```
index.html                        the whole site
images/                           photography, logo, bench video
  logo-badge.png                  bear badge, cut out of the client's own graphic
  favicon.png                     same badge at 180px
  beartrap-*.jpg                  Bear Trap wallet photos
  slim-green-hand.jpg             Bear Trap Slim
  tooled-*.jpg                    tooled sunflower purse (work in progress)
  graphic-*.jpg                   the client's own Facebook ad graphics (unused on
                                  the page — kept here in case you want them)
  bench-pattern.mp4                20s muted loop cut from his Pattern.mp4 (cropped
                                  to 5:4 off the portrait original)
  bench-pattern-poster.jpg         poster frame for it
  bench-cutting.mp4                22s muted loop cut from his Cutting.mp4 (cropped
                                  to 5:4 off the portrait original, head out of frame)
  bench-cutting-poster.jpg         poster frame for it
  bench-stitching.mp4              24s muted loop cut from his 66s Stitching.mp4
  bench-stitching-poster.jpg       poster frame for it
SHOPIFY-NOTES.md                  how each section maps to Shopify
```

The original full-resolution photos and the untrimmed 66s video are still in the
folder above this one.

---

## What it does

Nine scroll-driven moments, plain CSS and Intersection Observer — no animation library:

1. **Preloader** — spinning bear badge and a progress rail, then the curtain lifts.
2. **Hero** — headline lines rise under an overflow mask, two product photos float at
   different speeds on scroll, and a rotating SVG seal reads
   "Built to carry ★ Built to last ★ Handmade in Texas".
3. **Marquee band** — infinite scroll of craft terms, pauses on hover.
4. **Collection** — horizontal scroller with scroll-snap, arrow buttons, pointer drag
   and a progress rail.
5. **The Making** — scroll-pinned. The viewport locks while four stages advance
   (Pattern → Cut → Stitch → Finished piece); each cross-fades its own media and the
   step rail tracks along. Stages 01–03 are his own bench videos, each only starting
   to download once its stage becomes active, so the page still loads fast. Stage 04
   is a photo of the finished wallets.
6. **The Iron Bear Standard** — three pillars plus numbers that count up on first view.
7. **Customers are saying** — the six real reviews, swipeable / draggable.
8. **Tooled purse teaser** and **CTA band**.
9. **Bear Den** signup (front-end only — see below).

Plus: reading-progress bar, header inverts automatically over light sections,
section reveals stagger on scroll, headline shrinks to fit if the webfont is blocked.

Below 1000px the pinned section unpins into a stacked layout and each stage plays its
own media as it scrolls in. `prefers-reduced-motion` turns all of it off and the page
renders as static content.

---

## Where to edit things

| What | Where |
|---|---|
| **Prices** | `PRODUCTS` array at the bottom of `index.html` — `price:` on each entry |
| Product names, one-liners, badges | same array (`tag:"soon"` renders the green "Coming soon" chip) |
| Reviews | `REVIEWS` array right below it |
| Aggregate rating (`4.83`, `6 verified reviews`) | reviews section markup, and the `data-count` on the stats row |
| Any photo | overwrite the file in `images/` with the same name, or change the path in `PRODUCTS` |
| Colours | the `:root` block at the top of the `<style>` — `--tan`, `--ink`, `--moss` etc. |
| Announcement bar | `#annTrack` markup near the top of `<body>` |

## Known limits (say these before he asks)

- **The newsletter form does nothing.** It shows a confirmation and clears. It needs
  Shopify or Klaviyo behind it.
- **"Add to cart" buttons do nothing.** They are visual only until this is on Shopify.
- Prices are invented placeholders.
- The three bench videos (pattern, cutting, stitching) were trimmed to ~20s loops and
  compressed for the web (under 1 MB each, H.264 main/4.0 for maximum phone
  compatibility). The originals stay in the folder above.
- Stage 04 ("Finished piece") is a photo, not a video — didn't have footage for it.
  If he sends a clip of the final burnish/inspection, it drops straight in: same
  `<video>` markup as stages 01–03.
- Google Fonts (Oswald, Barlow, Caveat Brush) load from the network. Offline the page
  still works — it falls back to condensed system fonts and the headline auto-fits.
