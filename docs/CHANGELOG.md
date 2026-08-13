# Changelog

Newest last. One entry per change, written at the time of the change.

## 2026-08-09 — Design tokens ported from the parent site
What: Added `docs/tokens.md` (a copy of the measured token reference from
      `spikeypenguin123/tombannerman_website`) and `assets/tb-tokens.css`, which defines
      those values as `--tb-*` custom properties and maps them onto Dawn's own colour,
      type, layout and control properties for `:root` and `.color-scheme-1`.
Why:  The theme has to read as a continuation of tombannerman.com, and CLAUDE.md requires
      every value to come from measured source rather than being invented. Dawn generates
      its properties from `config/settings_data.json`, which is remote-authoritative and
      must not be hand-edited, so the values are overridden in CSS at equal specificity
      and later source order instead.

## 2026-08-09 — Coming-soon (password) page styled
What: Applied the tokens to the password page. Wordmark `Tom.Bannerman` in the header,
      linking back to tombannerman.com; heading changed to "Prints, opening soon" with a
      one-line description; background image and text box turned off for a plain
      typographic page; the email capture's icon-only arrow button replaced with a
      labelled `Notify me` button; a `tombannerman.com →` link back to the parent site.
      New: `assets/tb-password.css`. Edited: `layout/password.liquid`,
      `sections/main-password-header.liquid`, `sections/email-signup-banner.liquid`,
      `templates/password.json`, `locales/en.default.json`.
Why:  Scope item 0 — the password page is the only page the public can currently see, so
      it is the first thing to style. The button change was needed because Dawn positions
      `.field__button` absolutely inside the input as an icon, which cannot carry a
      visible label.

## 2026-08-09 — Coming-soon page copy revised
What: Description line now names the paper and where prints ship from. The parent-site
      link reads "← Back to tombannerman.com", with the arrow leading and its hover nudge
      reversed to match. Added the parent site's colophon to the password footer:
      `tombannerman.com · Built on the Gold Coast · First principles, always.`
Why:  Revised copy from the owner. The footer line brings the two footers into parity,
      which the first pass had deferred.

## 2026-08-09 — Fixed the coming-soon CTA, which was invisible on mobile
What: Raised specificity on the `Notify me` button, the email form layout and the input
      ring reset in `assets/tb-password.css`, and widened the button's focus-ring offset.
Why:  `sections/email-signup-banner.liquid` pulls in four Dawn stylesheets from the body,
      so they load AFTER `tb-password.css` and win every equal-specificity tie. Three
      things were broken as a result: `component-newsletter.css` reset the button to
      `background-color: inherit`, leaving it unfilled — and on mobile, paper text on
      paper, so the primary call to action was invisible; `display: flex` never applied
      to the form, so its `gap` was dropped and the field and button sat flush;
      and the input carried two borders on desktop. Found by rendering the page in
      Chromium from the theme source.

## 2026-08-09 — Palette applied to the whole storefront, not just the password page
What: `layout/theme.liquid` now loads `assets/tb-tokens.css` and the site's three
      typefaces. All five of Dawn's colour schemes are mapped to the parent site's
      palette, not just scheme-1: paper, raised paper, ink, the dark simulator panel,
      and violet. Added `--tb-panel*` tokens for the dark schemes. Heading tracking and
      `::selection` now apply site-wide; body sizing and link colour stay scoped to the
      password page.
Why:  `tb-tokens.css` was only ever loaded by `layout/password.liquid`, so every real
      storefront page still rendered in stock Dawn `#FFFFFF` — reported as painfully
      bright. Contrast was measured for every scheme; all pairings clear WCAG AA except
      links on scheme-2 at 4.49:1, kept for link-colour consistency.

## 2026-08-09 — Storefront content and chrome aligned with the parent site
What: Storefront header renders the `Tom.Bannerman` wordmark instead of the Shopify store
      name; storefront footer carries the colophon. Homepage replaced: Dawn's demo hero
      is gone and the homepage opens directly on the product grid, titled "All prints"
      at 3:2 (`image_ratio: adapt`), one column on mobile. No intro section — the owner
      asked for the prints to be the first thing on the page. Announcement bar now
      states the paper and where prints ship from. Footer newsletter heading is "New
      prints, occasionally". `.tb-mark` and `.tb-colophon` moved into `tb-tokens.css` so
      both layouts share one definition.
Why:  The storefront was still Dawn's demo — a stock illustration hero, "Welcome to our
      store", "Join our email list / Get exclusive deals and early access to new
      products". That last one is the marketing register the brief rules out, and none of
      it read as a continuation of tombannerman.com.

## 2026-08-09 — Wordmark no longer wraps in the storefront header
What: `.header__heading-link .tb-mark` pins the wordmark to 19px, `white-space: nowrap`,
      `word-break: normal`, and full-strength foreground colour.
Why:  Dawn sets `word-break: break-word` on the header heading and sizes it as an `.h2`
      (20px, 24px on desktop), which was breaking "Tom.Bannerman" mid-word into
      "Tom.Bannerm / an" on a phone. It also renders the heading at 75% opacity. The
      parent site's wordmark is a flat 19px at full strength and never wraps. Measured in
      Chromium: 157px wide against a 181px centre column at phone width.

## 2026-08-09 — About section added; the Australia claim removed
What: Announcement bar changed from "Printed on Hahnemühle Photo Rag · Shipped from
      Australia" to "Fine-art prints, shipped worldwide". Added an `about` rich-text
      section to the homepage, below the grid, on scheme-2 with a link out to
      tombannerman.com. Bio later rewritten to the owner's own copy, adding EARTH and
      TRAVEL collection notes as uppercase caption labels between the paragraphs.
Why:  Prodigi routes each order to whichever lab is closest to the customer, so nothing
      is reliably shipped from Australia and the old line was not true. The About section
      is the owner's request — a short first-person profile, placed after the prints so
      the work still leads.

## 2026-08-13 — Portrait added to the About block
What: New `sections/tb-about.liquid` + `assets/tb-about.css`, and `assets/tb-portrait.jpg`
      (1000×1334, 261 KB, re-encoded from the owner's original 1762×2350). The homepage
      `about` section switches from Dawn's `rich-text` to `tb-about`, carrying the same
      copy across as heading / text / label / button blocks.
Why:  Dawn's image sections take their image from an `image_picker`, which stores a
      reference to a file uploaded in the Shopify admin — unreachable from the repo. A
      theme asset referenced with `asset_url` is the only way to version the portrait
      alongside the copy. Trade-off: no Shopify CDN srcset, so the file is pre-sized to
      1000px, which covers the ~500px it renders at on a 2x display.
