# ORO Profile Update Implementation Plan

> Execute inline in the existing workspace; no deployment or Git changes are required.

**Goal:** Display the six supplied profile pages and align the five contact links without changing the approved visual design.

**Architecture:** Keep the existing static HTML, styles, and percentage-positioned link overlays. Convert PNGs to WebP at their original dimensions. The user confirmed that the PNGs in `public/pages/` and `public/ORO.pdf` are already the new files.

**Tech Stack:** Static HTML/CSS, Pillow for conversion, Playwright for local browser checks.

**Spec:** The user's request in this conversation, including the five exact destination URLs.

## Constraints

- Preserve all visual styling, responsive layout, and Vercel configuration.
- Do not regenerate images or display URLs over the artwork.
- Keep the confirmed new PDF byte-for-byte unchanged.
- Provide a local preview; do not deploy to production.

## Review Focus

- Full button coverage, including icons and background, at mobile and desktop widths.
- Original image dimensions, colors, and sharpness.
- Correct six-page order and exact destination URLs.
- No obsolete WhatsApp overlay or missing resources.
- No layout shift from incorrect image dimensions.

## Steps

- [x] Inspect all six PNGs and the PDF; record image dimensions and contact button pixel bounds.
- [x] Preserve original PNGs in `new-profile/`, then encode `public/pages/01.webp` through `06.webp` losslessly; decoded pixels match every source image exactly.
- [x] Update only page markup, dimensions, accessibility descriptions, and contact link coordinates in `public/index.html`.
- [x] Serve `public/` locally and verify all resources, five links, button edges, responsive geometry, and screenshots at mobile and desktop widths.
- [x] Check that the PDF and Vercel configuration hashes match their initial values; provide the preview and verification results.

## Verification results

- Original dimensions retained: 3297 × 4659 on every page.
- Total image size: 46,035,614 bytes PNG → 33,768,280 bytes WebP (26.6% smaller).
- Browser widths checked: 320, 375, 390, 768, 1440 pixels; no horizontal overflow or browser errors.
- Forty button hit points per width, covering icon, label, background, and border; all passed.
- All five actual new-tab click destinations checked at 390 and 1440 pixels; outbound requests intercepted locally to avoid third-party dependencies.
- Original CSS, new PDF, and `.vercel/project.json` preserved byte-for-byte.
- Screenshots and machine-readable results saved in `.local-preview/`.
- Local preview: http://127.0.0.1:4173/ — no deployment performed.
