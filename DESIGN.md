# Design System

Generated from `index.html` by the `design-sessions` skill on 2026-11-12. Update it whenever the styles change.

## Principles

- Warm and traditional: wine, gold and cream on a paper background, with no cool tones.
- Serif (Georgia) headings for gravitas, and a system sans for body text so it stays readable.
- Self-contained: no external fonts, images or scripts. Art is inline SVG and icons are Unicode glyphs.
- Equal treatment of English and Hindi: every visible string exists in both languages.
- Measured copy: no promised outcomes, and visible disclaimers (Reiki isn't medical care, and visitors shouldn't share sensitive information).

## Color tokens

Defined on `:root`:

| Token | Value | Role |
|---|---|---|
| `--ink` | `#47251f` | Body text, input text, lang/menu button text |
| `--wine` | `#722e2c` | Primary brand: buttons, logo mark, trust band, quote panel, card links, step numbers |
| `--gold` | `#b87827` | Accent (**defined but never referenced with `var()`**) |
| `--paper` | `#fffaf0` | Page background |
| `--muted` | `#745d50` | Secondary text: `.lead`, `.muted`, `.note` |

Hard-coded colors, grouped by role:

| Role | Values | Used in |
|---|---|---|
| Gold accent | `#b87827` | Focus outline, SVG outer stroke (duplicates `--gold`) |
| Bronze accents | `#a86b2d`, `#89541d`, `#c89952`, `#e5bd74`, `#e7c68d` | SVG strokes, `.eyebrow` text, `.step` top border, SVG Om ring, SVG gradient |
| Off-white surfaces | `#fffdf7`, `#fffdf8`, `#fffdf9`, `white` | Header and mobile nav, `.card`, inputs, `.form` |
| Cream surfaces | `#fff5e3`, `#f5dfb4`, `#f5ead7`, `#f7e7c8` | Hero background and glow, `.soft` sections, `.symbol` circle |
| Light-on-wine text | `#fff5df`, `#fff1cf`, `#fff0c9`, `white` | Trust band and quote, logo mark, SVG Om, `.btn` |
| Borders | `#e8d9c3`, `#e6d5ba`, `#e4d3ba`, `#dbc9af`, `#bda78b`, `#bba994` | Header, card, form, FAQ rows, lang/menu buttons, inputs |
| Footer | `#42251f` bg, `#f9e9d2` text | `footer` |
| Shadow | `#633b1510` | `.card` |

## Typography

| Element | Font | Size | Notes |
|---|---|---|---|
| Body | `system-ui, sans-serif` | 18px / 1.65 | Form controls inherit the body font |
| h1–h3 | `Georgia, 'Noto Serif Devanagari', serif` | h1 `clamp(42px, 6vw, 76px)`, h2 `clamp(32px, 4vw, 48px)`, h3 `27px` | line-height 1.18, margin `12px 0 18px`; h1 letter-spacing `-.035em` |
| Brand | Georgia, bold | 23px (19px on mobile) | Header logo text |
| `.eyebrow` | body | 13px | Uppercase, `.15em` tracking, weight 750, `#89541d` |
| `.lead` | body | 21px | `--muted`, max-width 590px |
| Nav links | body | 15px | Weight 650 |
| `.quote p` | Georgia | 26px | Om glyph above it at 85px |
| `.note` | body | 14px | `--muted` |
| `.step b` | body | 25px | `--wine`, step numbers 01–03 |

Weights in use: 650 (UI labels and buttons), 700 (summary), 750 (eyebrow), bold (brand, card links).

## Layout and spacing

- **Container** `.wrap`: max-width 1160px, 24px side padding (18px on mobile).
- **Sections** `.section`: 76px vertical padding (50px on mobile), and `scroll-margin-top: 90px` to clear the sticky header.
- **Hero**: 90px padding (55px on mobile), two-column grid `1.1fr .9fr` with a 45px gap.
- **Grids**: `.cards` and `.steps` use 3 equal columns (20px / 24px gaps). `.split` uses 2 columns with a 50px gap.
- **One breakpoint, `max-width: 800px`**: every grid collapses to one column, the hero art shrinks to 320px, and the nav becomes a dropdown behind the ☰ button.
- **Radii**: 7px (buttons, inputs), 8px (lang/menu buttons), 16px (cards, form), 18px (quote), 50% (logo mark, symbols).

## Components

- **Header**: sticky, `z-index: 5`, off-white background with a bottom border. Contains the brand (a 48px wine circle `.mark` with ॐ, plus the name), the nav, and the `.lang` / `.menu` outline buttons.
- **`.btn`**: wine fill, white text, min-height 52px, padding `12px 23px`, radius 7px, weight 650. **`.btn.secondary`**: transparent with wine text and border. Inside `.form`, buttons are full width.
- **`.trust`**: a wine band of three ✦ statements, spread with `space-around`.
- **`.card`**: off-white with a warm border, 16px radius, 30px padding and a soft shadow. Holds a `.symbol` (60px cream circle with a glyph), an h3, copy and a wine link.
- **`.quote`**: a wine panel with centered Om and a serif quotation.
- **`.step`**: a numbered column with a bronze top border.
- **FAQ**: native `<details>` / `<summary>` rows with bottom borders, max-width 820px.
- **`.form`**: a white panel. Labels are block-level at weight 650. Inputs are full width with 12px padding and a 7px radius. The result area (`#result`) is hidden until submit.
- **Footer**: dark brown with brand, tagline and a dynamic year.
- **States**: the only interactive state styled is `:focus-visible` (3px `#b87827` outline, 4px offset). **There are no hover states.** The mobile nav is shown with `nav.open`.

## Iconography and imagery

- Hero art is an inline SVG mandala: concentric circles, 8 rotated `<use>` petals, a diamond and two triangles, and ॐ on a wine disc. It is labelled `role="img"` with an `aria-label`.
- Service symbols are Unicode glyphs: ☉ Astrology, ◇ Vastu, ✿ Reiki. ✦ and ॐ are used decoratively.
- No raster images or external assets.

## Internationalization

- Every translatable element has `data-en` and `data-hi`, and its initial text is the English string. The `#lang` button swaps `textContent` on all `[data-en]` elements and sets `<html lang>`.
- Translatable elements must contain plain text only, because nested markup is destroyed on swap.
- Hindi relies on the browser's Devanagari fallback. `'Noto Serif Devanagari'` is named in the heading stack but isn't loaded.

## Accessibility

Already in place: a skip link (`.skip`), `:focus-visible` outlines, `aria-label` on the icon buttons, `aria-expanded` on the menu toggle, an `aria-label` on the hero SVG, `aria-hidden` on decorative Om glyphs, `role="status"` for copy feedback, a `<label>` on every field, `autocomplete="name"`, and `prefers-reduced-motion` turning off smooth scroll.

Gaps:
- The `.symbol` glyphs (☉ ◇ ✿) aren't `aria-hidden`, so screen readers announce them.
- `aria-label` values ("Change language", "Toggle navigation", the SVG label) stay in English in Hindi mode.

## Known inconsistencies

- `--gold` is defined but unused, and `#b87827` is hard-coded in the focus outline and SVG instead.
- There are many near-duplicate off-whites and creams (`#fffdf7` / `#fffdf8` / `#fffdf9`, `#fff5df` / `#fff5e3`, `#fff1cf` / `#fff0c9`) and six border colors. These could collapse into a few tokens.
- An inline `style="display:flex;gap:8px"` sits on the header button wrapper.
- These stay in English when switched to Hindi: the prepared consultation message, the footer brand `<strong>` and © line, `<title>` and meta description, and the `aria-label`s.
- No hover feedback on `.btn`, nav links or card links.
- `'Noto Serif Devanagari'` is referenced but not loaded.
