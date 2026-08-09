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
