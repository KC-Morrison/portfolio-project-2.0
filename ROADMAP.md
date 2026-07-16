# Portfolio Site: Iteration Roadmap

Handover document for iterating on `index.html` (kmorrison.dev). Written to be handed to a model (e.g. Opus) or a developer with no prior context.

---

## Context (read first)

- **What it is:** a single-page, single-file HTML portfolio for Katie Morrison, built as a conference handout. Mobile-first, warm and editorial. Fraunces (serif) + Karla (sans), cream background `#FAF5EE`, terracotta accent `#B4552D`, deep green `#3E5C4B` for the contact section, footer and tags.
- **Hard rules (never break these):**
  - Never name the employer. Refer only to "a not-for-profit domestic violence service". The domain `humanandco.org.au` must never appear anywhere, including metadata, alt text and analytics config.
  - Describe capability, never a job title.
  - Australian English spelling in all copy. No em dashes anywhere in copy.
  - Copy stays in Katie's voice: warm, plain, confident, no corporate tone. "Stewardship, not admin."
  - Single primary CTA: Connect on LinkedIn (`https://www.linkedin.com/in/katherine-a-morrison/`).
- **Keep it a single self-contained HTML file** until Phase 5 says otherwise.

---

## Phase 1: Content completion (blocked on Katie, do first when supplied)

Everything here needs input from Katie. Slot content in without changing structure.

1. **Photo.** DONE: hero photo in place as `katie.webp` (800x800 square) with `katie.jpg` fallback, EXIF stripped, `fetchpriority="high"`, alt text with no employer reference. Source file is `assets/source/BINADW KM 7.jpg` (5371x3581) if recrops are ever needed.
2. **Personal projects.** Replace the two dashed `.fun-card` placeholders with real content: what it is, what it does, what made it fun, plus a link or screenshot if shareable. Remove the dashed border once real (it signals "placeholder").
3. **Case study.** Replace the drafted Claude + Obsidian article in the `<details class="post">` body with Katie's own write-up. Check it for identifying details before publishing.
4. **Email decision.** Currently omitted deliberately (her work domain identifies the employer). If she supplies a personal or custom-domain address, add it to the contact section as a secondary action, styled like `.btn-ghost` in cream. Consider an obfuscation approach (JS-assembled mailto) to limit scraping.

**Acceptance:** no bracketed `[Katie to supply]` text remains anywhere on the page.

## Phase 2: Accessibility and robustness

1. **Reduced motion.** Wrap the marquee animation in `@media (prefers-reduced-motion: no-preference)`. With reduced motion, show the words as a static wrapped line.
2. **Focus states.** Add visible `:focus-visible` styles to all links, buttons and the `<details>` summary (terracotta outline works with the palette).
3. **Contrast audit.** Verify all text/background pairs at WCAG AA. Known risks: `--ink-soft #5C534A` on `--cream-deep #F3EADF` (check), footer text `#A9BEAF` on green `#3E5C4B` (likely fails for small text; lighten toward `#C9D8CD` if so).
4. **Semantics.** Confirm one `<h1>`, logical heading order, `<main>` landmark around sections, `aria-label` on the nav, and that the marquee stays `aria-hidden="true"`.
5. **Details animation.** The case study `<details>` snaps open. Add a gentle height/opacity transition (respecting reduced motion).

**Acceptance:** passes Lighthouse accessibility ≥ 95 and keyboard-only navigation works end to end.

## Phase 3: Conference readiness (do before the conference)

1. **Metadata for sharing.** DONE: canonical, Open Graph (including `og:image` at 1200x630), Twitter `summary_large_image` card, JSON-LD `Person` schema and an inline SVG "KM" favicon, all pointing at `https://kmorrison.dev/`.
2. **Hosting.** DONE: this GitHub repository is linked to Netlify and publishes to `kmorrison.dev` on every push to `main`. Rollback via Netlify's Deploys tab (publish an older deploy). Note: `.dev` is HSTS-preloaded, so HTTPS is mandatory (Netlify handles this).
3. **QR code.** DONE: generated for `https://kmorrison.dev/` in two colourways (ink-on-cream and green-on-cream) in `assets/`, each as SVG and high-res PNG, decode-verified. An inverted (cream-on-green) version was tested and failed to decode; keep QR codes dark-on-light. Remaining: test scan distance from a printed A6 before the conference.
4. **Performance pass.** Target Lighthouse performance ≥ 95 on mobile: `font-display: swap` is already set via Google Fonts; consider self-hosting the two fonts as woff2 subsets to remove the third-party request; total page weight should stay under ~500 KB.
5. **Analytics (optional, privacy-first).** If Katie wants to know whether conference scans convert, add a lightweight privacy-respecting counter (e.g. Plausible or GoatCounter). No cookies, no consent banner needed.

**Acceptance:** live URL + QR code scan to a page that loads in under 2 seconds on throttled 4G.

## Phase 4: Polish and personality (nice-to-haves)

1. **Scroll reveal.** Subtle fade-up on cards and section headings via `IntersectionObserver`, disabled under reduced motion.
2. **Marquee hover pause.** Pause the animation on hover/focus so the words are readable on desktop.
3. **Card interest.** Consider a small terracotta arc or textured accent (Cedar-template style) behind the hero or between sections; keep it restrained.
4. **"Open to" line.** Add a one-liner near contact: what Katie is interested in or open to (needs her words).
5. **Skills strip.** Optional one-line capability list if the page feels like it needs it; skip if it reads as padding.

## Phase 5: Growth (after the conference)

1. **Writing as a collection.** When there are 3+ pieces, move writing off the single scroll: either (a) generate lightweight static article pages from markdown with an index at `/writing/`, or (b) migrate to Squarespace Fluid (Cedar-style Journal module) as originally envisaged. Decide based on how much Katie wants to own the stack vs. edit through a UI.
2. **Squarespace copy deck.** If migrating, produce a section-by-section copy deck mapping this page onto a Fluid template, preserving the hard rules above.
3. **RSS / syndication.** If writing stays self-hosted, add an RSS feed so LinkedIn/Substack pieces can cross-link.
4. **Case-study pages.** If projects deepen, promote cards 01 and 02 to their own case-study pages linked from the cards.

---

## Working notes for the implementing model

- The file is deliberately dependency-free: no frameworks, no build step. Keep it that way through Phase 4.
- Katie's browser did not apply CSS `aspect-ratio` on the hero image (the height attribute rendered literally, producing a stretched crop). Avoid `aspect-ratio` on replaced elements; crop images to their intended ratio at the file level instead and use `height:auto`.
- A truncated copy of `index.html` once shipped to production (file cut mid-body, losing the contact section and footer). After any copy, sync or deploy, verify the file ends with `</html>` before calling it done.
- Test at 360px, 768px and 1200px widths; the audience scans this on phones on conference wifi.
- After every iteration, re-run the three checks: no em dashes in copy, no US spellings in copy (CSS keywords excepted), no employer identifiers anywhere.
- When in doubt on tone, cut words rather than add them.
