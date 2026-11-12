# AGENTS.md

This file is generated from CLAUDE.md by the `design-sessions` skill (2026-11-12). Make edits in CLAUDE.md and regenerate this file.

Guidance for AI coding agents working in this repository.

## Overview

A static, single-page marketing site for Shri Rudraksh Jyotish (Astrology, Vastu, Reiki), meant for GitHub Pages (the repo is named `shri-rudraksh-jyotish.github.io`). There's no build step, package manager, linter or test suite. The whole site is one file, `index.html`, with inline CSS in `<style>` and inline JS in `<script>`. It's written minified: the CSS is on one line, and the markup and script are mostly on one line each.

## Development

- Preview: open `index.html` directly in a browser, or serve the folder (e.g. `python -m http.server`) and visit `http://localhost:8000`.
- Keep the file self-contained: no external scripts, stylesheets, fonts or images. The hero art is inline SVG and icons are Unicode glyphs.

## Architecture (all in `index.html`)

**Bilingual text (English/Hindi).** Every translatable element has both `data-en` and `data-hi` attributes, and its initial text is the English string. The language toggle (`#lang`) swaps the `textContent` of every `[data-en]` element and sets `<html lang>`. This means:
- Any new visible text needs both `data-en` and `data-hi`, with the English also written as the element's content.
- Because `textContent` is replaced, translatable elements can contain only plain text, with no nested markup. Put `data-en` on the innermost element instead.
- JS-generated strings (the copy status messages) branch on the global `hindi` flag. The prepared consultation message itself is always in English.

**Consultation form (`#request`).** This runs entirely in the browser; nothing is sent or booked. On submit it builds a "Namaste…" message from the name, service and questions into `#output`, then reveals `#result`. `#copy` uses the Clipboard API, falling back to selecting the text. Service card links with `data-service="…"` preselect the `#service` `<select>`, so those values must match the `<option value>`s (`Astrology`, `Vastu`, `Reiki`).

**Navigation.** Sections are anchor targets (`#home`, `#services`, `#about`, `#faq`, `#contact`) linked from the sticky header. Below 800px the nav collapses behind `#menu`. It's toggled with the `.open` class, and `aria-expanded` is kept in sync.

**Styling.** Theme colors are CSS custom properties on `:root` (`--ink`, `--wine`, `--gold`, `--paper`, `--muted`). A single `@media(max-width:800px)` block handles the mobile layout, and `prefers-reduced-motion` turns off smooth scrolling.

## Content constraints

The copy deliberately avoids promising outcomes and includes disclaimers: Reiki is complementary and not a substitute for medical care, and visitors shouldn't share sensitive medical or financial information. Keep this tone and these disclaimers, in both languages, when editing content.

## Project docs

- **DESIGN.md**: the design system (tokens, typography, layout, components, i18n, accessibility, known inconsistencies). Read it before changing styles or markup, and update it when tokens or components change.
- **SESSIONS.md**: a work log, newest first. At the end of each work session, add an entry dated `## YYYY-MM-DD: <title>` with **Changes**, **Decisions** and **Follow-ups** sections. Never edit earlier entries.
