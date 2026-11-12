# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static, single-page marketing site for Shri Rudraksh Jyotish (Astrology, Vastu, Reiki), intended for GitHub Pages (the repo is named `shri-rudraksh-jyotish.github.io`). There is no build step, package manager, linter, or test suite. The entire site is one file: `index.html`, with inline CSS in `<style>` and inline JS in `<script>`, written minified (CSS on one line, markup and script mostly on one line each).

## Development

- Preview: open `index.html` directly in a browser, or serve the folder (e.g. `python -m http.server`) and visit `http://localhost:8000`.
- Keep the file self-contained: no external scripts, stylesheets, fonts, or images (the hero art is inline SVG; icons are Unicode glyphs).

## Architecture (all in `index.html`)

**Bilingual text (English/Hindi).** Every translatable element carries both `data-en` and `data-hi` attributes, and its initial text content is the English string. The language toggle (`#lang`) swaps `textContent` of every `[data-en]` element and sets `<html lang>`. Consequences:
- Any new visible text must have both `data-en` and `data-hi`, with the English duplicated as the element's content.
- Because `textContent` is replaced, translatable elements must contain only plain text — no nested markup (put `data-en` on the innermost element instead).
- JS-generated strings (copy status messages) branch on the global `hindi` flag. The prepared consultation message itself is always English.

**Consultation form (`#request`).** Purely client-side; nothing is sent or booked. On submit it builds a "Namaste…" message from name/service/questions into `#output`, reveals `#result`, and `#copy` uses the Clipboard API with a select-text fallback. Service card links with `data-service="…"` preselect the `#service` `<select>`; those values must match the `<option value>`s (`Astrology`, `Vastu`, `Reiki`).

**Navigation.** Sections are anchor targets (`#home`, `#services`, `#about`, `#faq`, `#contact`) linked from the sticky header. Below 800px the nav collapses behind `#menu`, toggled via the `.open` class with `aria-expanded` kept in sync.

**Styling.** Theme colors are CSS custom properties on `:root` (`--ink`, `--wine`, `--gold`, `--paper`, `--muted`); a single `@media(max-width:800px)` block handles mobile layout, and `prefers-reduced-motion` disables smooth scrolling.

## Content constraints

The copy deliberately avoids claims of guaranteed outcomes and includes disclaimers (Reiki is complementary and not a substitute for medical care; users shouldn't share sensitive medical/financial info). Preserve this tone and these disclaimers, in both languages, when editing content.
