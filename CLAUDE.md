# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A static, single-page marketing site for Shri Rudraksh Jyotish (Astrology, Vastu, Reiki), meant for GitHub Pages (the repo is named `shri-rudraksh-jyotish.github.io`). There's no build step, package manager, linter or test suite. The whole site is one file, `index.html`, with inline CSS in `<style>` and inline JS in `<script>`, written in readable, formatted form.

## Development

- Preview: open `index.html` directly in a browser, or serve the folder (e.g. `python -m http.server`) and visit `http://localhost:8000`.
- Visual check without a browser window: `chrome --headless=new --screenshot=out.png --window-size=1366,5200 file:///<abs path>/index.html`. Headless Chrome won't lay out narrower than about 500px, so for a mobile check, load the page in a 390px-wide `<iframe>` from a scratch page and screenshot that.
- Keep the file self-contained: no external scripts, stylesheets, fonts or images. The hero art is inline SVG and icons are Unicode glyphs or emoji. The only outbound link is the `wa.me` share link.

## Architecture (all in `index.html`)

**Bilingual text (English/Hindi).** Every translatable element has both `data-en` and `data-hi` attributes, and its initial text is the English string. The `#lang` toggle swaps the `textContent` of every `[data-en]` element (including `<title>` and the toggle's own label), swaps `aria-label` on every element with `data-label-en` / `data-label-hi`, and sets `<html lang>`. This means:
- Any new visible text needs both `data-en` and `data-hi`, with the English also written as the element's content. New `aria-label`s need `data-label-en` / `data-label-hi`.
- Because `textContent` is replaced, translatable elements can contain only plain text, with no nested markup. Split styled fragments into sibling elements, each with its own translations, the way the two-line `<h1>` does.
- JS-generated strings (the prepared message and copy status) branch on the global `hindi` flag. When the language toggles while a message is shown, it's rebuilt in the new language.

**Consultation form (`#request`).** This runs entirely in the browser; nothing is sent or booked. `build()` composes a "Namaste…" message from the name, the selected option's text and the questions into `#output`, and sets `#wa` to `https://wa.me/?text=…`. `#copy` uses the Clipboard API, falling back to selecting the text. Any link with `data-service="…"` (service cards and hero chips) preselects `#service`, so those values must match the `<option value>`s (`Astrology`, `Vastu`, `Reiki`). Links that also have `data-prompt` (the hero chips) copy their visible text into `#message`.

**Navigation.** Sections are anchor targets (`#home`, `#services`, `#about`, `#how`, `#faq`, `#contact`) linked from the sticky header. Below 800px the nav collapses behind `#menu`, toggled with the `.open` class and `aria-expanded`.

**Motion.** The script adds `.js` to `<html>`, and `.reveal` elements fade in through an IntersectionObserver. Content stays visible without JS. The mandala `.spin`, the `.spark` floats and the `.ticker` marquee are CSS animations. The ticker's second `.group` is an `aria-hidden` duplicate for a seamless loop, so edit both groups together. `prefers-reduced-motion` turns off all animation and transitions.

**Themes.** There are two themes, chosen by `data-theme` on `<html>`. `:root` holds the dark "cosmic" tokens, and `:root[data-theme="light"]` overrides them with the saffron light palette. A small inline script in `<head>` sets `data-theme` before first paint, using the saved `localStorage.theme` or else `prefers-color-scheme`. The `#theme` button toggles the theme, saves the choice, and updates its own glyph (☀/☾), its translated `aria-label` and `<meta name="theme-color">` through `syncThemeBtn()`. With no saved choice, the page follows OS theme changes. Any new color must be a token defined in **both** blocks: never hard-code a color that differs between themes. That includes SVG gradient stops, which read tokens through CSS classes (`.s1`–`.s3`, `.c1`/`.c2`). The only deliberate fixed colors are the wine quote panel and its text.

**Styling.** Every color, radius and font stack is a custom property. The signature gradient is `--grad` (built from `--g1`–`--g3`), with `--on-grad` text on top: dark text in the dark theme, white in light. A single `@media(max-width:800px)` block handles the mobile layout. DESIGN.md documents the full system.

## Content constraints

The voice is casual and Gen Z-friendly ("Questions? We got you."), but the copy must never promise outcomes or predictions. Keep the disclaimers: Reiki is complementary and not a substitute for medical or mental health care, visitors shouldn't share sensitive medical or financial information, and spiritual guidance isn't professional advice. Keep this tone and these disclaimers in both languages, and keep the Hindi copy gender-neutral.

## Project docs

DESIGN.md is the design system, and SESSIONS.md is the work log (newest first, append-only). AGENTS.md and GEMINI.md are generated from this file by the `design-sessions` skill, so edit this file and rerun the skill rather than editing them directly.
