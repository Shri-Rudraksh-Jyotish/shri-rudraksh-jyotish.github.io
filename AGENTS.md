# AGENTS.md

This file is generated from CLAUDE.md by the `design-sessions` skill (2026-11-12). Make edits in CLAUDE.md and regenerate this file.

Guidance for AI coding agents working in this repository.

## Overview

A static, single-page site for Shri Rudraksh Jyotish (Astrology, Vastu, Reiki), meant for GitHub Pages (the repo is named `shri-rudraksh-jyotish.github.io`). There's no build step, package manager, linter or test suite. The whole site is one file, `index.html`, with inline CSS in `<style>` and inline JS in `<script>`, written in readable, formatted form.

**DESIGN.md is the visual and interaction contract** (a cinematic editorial direction: deep navy, a sculptural focal point, serif/sans contrast, restrained navigation, purposeful motion). It is hand-authored, so read it before changing styles, layout or motion, and follow it. It was written for a portfolio; this site maps its "featured project selector" onto the three services and its "selected work" onto the service rows. Don't invent projects, products or testimonials.

## Development

- Preview: open `index.html` directly in a browser, or serve the folder (e.g. `python -m http.server`) and visit `http://localhost:8000`.
- Headless visual check: `chrome --headless=new --virtual-time-budget=8000 --window-size=1440,900 --screenshot=out.png file:///<abs path>/index.html`. Some caveats:
  - The hero is `min-height:100svh`, so a tall window stretches it. For a full-page shot, use a scratch copy that injects `.hero{min-height:900px!important}`.
  - Add `.js .reveal{opacity:1!important;transform:none!important}` too, or the scroll-reveal sections can be captured mid-fade.
  - Headless Chrome won't lay out narrower than about 500px, so check mobile by loading the page in a 390px-wide `<iframe>`.
- Keep the file self-contained: no external scripts, stylesheets, fonts or images. The font stacks name "Bodoni Moda" and "Manrope" first but don't load them; they're used only if installed, with Bodoni 72/Didot/Times and Segoe UI/system-ui as fallbacks. To use them for real, self-host WOFF2 files in the repo. The only outbound link is the `wa.me` share link.

## Architecture (all in `index.html`)

**Bilingual text (English/Hindi).** Every translatable element has both `data-en` and `data-hi` attributes, and its initial text is the English string. The `#lang` toggle swaps the `textContent` of every `[data-en]` element (including `<title>`), swaps `aria-label` on every element with `data-label-en` / `data-label-hi`, and sets `<html lang>`. This means:
- Any new visible text needs both `data-en` and `data-hi`, with the English also written as the element's content. New `aria-label`s need `data-label-en` / `data-label-hi`.
- Because `textContent` is replaced, translatable elements can contain only plain text. Put icons and arrows in sibling `aria-hidden` spans, e.g. `<a class="btn"><span data-en…>Text</span><span class="arr" aria-hidden="true">→</span></a>`.
- JS-generated strings (the prepared message, copy status, theme label, scene text) branch on the global `hindi` flag.
- Uppercase tracked labels get `letter-spacing:0` under `html[lang="hi"]`, because tracking breaks Devanagari conjuncts. Add any new tracked class to that rule.

**Header.** It's fixed: transparent over the hero, and `.solid` after 40px of scroll or while the menu is open. The two `.nav-group` lists sit either side of an absolutely centred ॐ `.monogram`. Below 1024px the nav collapses into a dropdown behind `#menu`; opening it focuses the first link, and Escape closes it and returns focus. An IntersectionObserver scroll spy sets `aria-current` on the link for the section in view.

**Hero scene selector.** This is the DESIGN.md "featured project selector". The `scenes` array (Astrology / Vastu / Reiki, en+hi strings, service value) drives `go(dir)`:
- It sets `.hero[data-scene]`, which changes the `--a1`–`--a3` artwork tints (SVG stops read them through `.a1`–`.a3`, with a transition on `stop-color`).
- It rotates `#turn` by ±120°.
- It crossfades `#scene-eyebrow` and the `aria-live` `#scene-info` through `.swapping`.
- It's throttled by `busy` for 900ms, and changes instantly under reduced motion.
- `paintScene()` rewrites the elements' `data-en`/`data-hi`, so the language toggle keeps working.
- `#scene-link` carries the current `data-service`.

The artwork is decorative (`aria-hidden`). The H1 is always the brand name.

**Consultation form (`#request`).** This runs entirely in the browser; nothing is sent or booked. `build()` composes a "Namaste…" message into `#output` in the active language and sets `#wa` to `https://wa.me/?text=…`. Any element with `data-service` (service rows, `#scene-link`, quick-start `.prompt` buttons) preselects `#service`, so its values must match the `<option value>`s (`Astrology`, `Vastu`, `Reiki`). Elements that also have `data-prompt` copy their text into `#message`.

**Motion** (DESIGN.md §8):
- **Entrance choreography:** CSS keyframes on load: header fade, then `.art-wrap` scale-in, then the h1 `rise`, then `.seq` items staggered by `--i`.
- **Ambient drift:** `.drift` runs a 12s loop and is paused while the hero is offscreen (`.offscreen`).
- **Scroll reveals:** `.js .reveal` fades in through an IntersectionObserver. Content stays visible without JS.
- **Restrictions:** no perpetual text animation, which is why the old marquee is now the static `.values` strip. `prefers-reduced-motion` turns off all animation and transitions.

**Themes.** `data-theme` on `<html>` selects one of two palettes:
- **Deep navy (default):** the `:root` tokens from DESIGN.md (`--bg-deep`, `--bg-navy`, `--bg-blue`, `--surface`, `--text`, `--muted`, `--gold`, `--line`, …).
- **Saffron light (opt-in):** overrides in `:root[data-theme="light"]`.

A head script applies the saved `localStorage.theme` before first paint. `#theme` toggles and saves the choice, and `syncThemeBtn()` updates the glyph, the translated label and `<meta name="theme-color">`. Any color that differs between themes must be a token defined in both blocks. Artwork accents (`--a1`–`--a3`) are per scene, not per theme.

**Layout.** There's a 12-column `.grid` (24px gaps) inside `.wrap` (max 1440px, fluid `--gutter`). Breakpoints are 1023px (nav collapses, columns stack) and 639px (single column, hero controls drop below the artwork). Buttons are outlined rectangles (`--radius: 4px`) and secondary actions are uppercase `.link`s; don't use pill buttons or card grids (DESIGN.md §2).

## Content constraints

The voice is casual and Gen Z-friendly ("Questions? We got you."), but the copy must never promise outcomes or predictions. Keep the disclaimers: Reiki is complementary and not a substitute for medical or mental health care, visitors shouldn't share sensitive medical or financial information, and spiritual guidance isn't professional advice. Keep this tone and these disclaimers in both languages, and keep the Hindi copy gender-neutral.

## Project docs

- **DESIGN.md**: the hand-authored visual and interaction contract. Read it before changing styles, layout or motion, and follow it. Don't rewrite it unless asked.
- **SESSIONS.md**: a work log, newest first. At the end of each work session, add an entry dated `## YYYY-MM-DD: <title>` with **Changes**, **Decisions** and **Follow-ups** sections. Never edit earlier entries.
