# Design System

Generated from `index.html` by the `design-sessions` skill on 2026-11-12. Update it whenever the styles change.

## Principles

- **Cosmic, not corporate**: a dark night-sky base with glowing saffron → rose → violet gradients. Heritage is kept through ॐ, the mandala and a wine-to-plum quote panel.
- **Gen Z voice, honest content**: casual, conversational copy ("Questions? We got you.", "Zero gatekeeping") with no promised outcomes and visible disclaimers.
- **Bold sans plus italic serif**: heavy, tight system-sans headlines, with a Georgia italic gradient line for emphasis.
- **Tactile and alive**: pill shapes, glass surfaces, hover lifts, a marquee ticker and a slowly spinning mandala, all of which switch off under reduced motion.
- **Self-contained and bilingual**: no external assets, and every string exists in English and Hindi.

## Themes

There are two themes, switched by the ☀/☾ `.theme` pill in the header (`data-theme` on `<html>`). The page defaults to the OS preference, and the visitor's choice is saved in `localStorage`.

- **Dark, "cosmic"** (`:root`): a night-sky plum base with a saffron → rose → violet gradient and dark text on the gradient.
- **Light, "saffron"** (`:root[data-theme="light"]`): a warm saffron-cream base (`#fff6e8`) with saffron and amber glows, deep maroon-brown text (`#3b1405`), and a burnt saffron → vermilion → maroon gradient (`#b85500` → `#c2410c` → `#9f1239`) with white text on top. The symbols are saffron, marigold and rose.

The quote panel (wine → plum, cream text, gold ॐ) is the same in both themes, as a fixed heritage element.

## Color tokens

Dark values are shown below. The light theme overrides every token marked †, plus the theme-only tokens listed after the table.

| Token | Value | Role |
|---|---|---|
| `--bg` | `#120a1c` | Page background (with fixed radial glows of rose, violet and saffron) |
| `--bg2` | `#1c1029` | Mobile nav dropdown, `<option>` background |
| `--text` | `#f7f0ff` | Primary text |
| `--muted` | `#bfaed3` | Secondary text, nav links at rest, card and FAQ body |
| `--surface` / `--surface2` | `rgba(255,255,255,.06)` / `.1` | Glass cards, chips, buttons at rest / tags and hover |
| `--line` | `rgba(255,255,255,.13)` | All hairline borders |
| `--saffron` | `#ff9a3c` | Gradient start, Astrology symbol |
| `--rose` | `#ff4f8b` | Gradient middle, Reiki symbol, input focus, open FAQ border |
| `--violet` | `#9b6bff` | Gradient end, Vastu symbol |
| `--gold` | `#f5c26b` | Stickers, focus outline, card links, ticker ✦, FAQ "+", quote ॐ |
| `--wine` / `--plum` | `#722e2c` / `#3d1640` | Quote panel gradient (heritage nod) |
| `--on-grad` | `#160b12` | Text on gradient and solid-accent fills |
| `--grad` | `linear-gradient(120deg, var(--g1), var(--g2) 52%, var(--g3))` | Primary buttons, logo mark, mandala core, gradient text |

† Overridden in light: `--bg`, `--bg2`, `--text`, `--muted`, `--surface`, `--surface2`, `--line`, `--saffron`, `--rose`, `--violet`, `--gold` (`#b45309` amber, for link and icon contrast on cream), `--on-grad` (white).

Theme-aware tokens added for the toggle: `--g1`/`--g2`/`--g3` (gradient stops, also used by the SVG through `.s1`–`.s3`), `--on-sym` (glyph on `.symbol` tiles), `--line-strong` (hover borders), `--sticker-fg`/`--sticker-bg`/`--sticker-line`, `--header-bg`, `--well` (input background), `--core1`/`--core2` (mandala core, through `.c1`/`.c2`), `--art-glow`, and `--page-bg` (body background with its glows).

Card `::after` glows (`--glow` per card), button and chip hover shadows, and the logo glow still use hard-coded rose, saffron and violet `rgba()` tints that work on both backgrounds.

## Typography

System fonts only: `--sans` (`system-ui, -apple-system, "Segoe UI", Roboto, sans-serif`) and `--serif` (`Georgia, "Times New Roman", serif`).

| Element | Style |
|---|---|
| Body | 18px / 1.65, `--sans` |
| h1 | `clamp(44px, 7vw, 88px)`, weight 850, tracking `-.045em`, line-height 1.02. Two block lines; the second (`.accent.grad-text`) is serif italic, weight 400, gradient-filled |
| h2 | `clamp(34px, 4.6vw, 56px)`, weight 800, tracking `-.035em` |
| h3 | 26px, weight 750 (38px in the big bento card, 30px on mobile) |
| `.sticker` | 13px uppercase pill, tracking `.12em`, weight 750, gold on a translucent gold fill |
| `.lead` | 20px, `--muted`, max-width 580px |
| `.num` | 60px, weight 850, gradient text (step numbers) |
| `.quote p` | 26px serif italic |
| `.note` | 14px, `--muted` |

## Layout and spacing

- **Container** `.wrap`: max-width 1180px, 24px gutters (16px on mobile).
- **Sections**: 88px vertical padding (60px on mobile), `scroll-margin-top: 80px`.
- **Hero**: grid `1.15fr .85fr`, 40px gap. On mobile the mandala moves above the text (`order: -1`, max-width 300px).
- **Services bento**: grid `1.25fr 1fr`, 18px gap. The Astrology `.card.big` spans 2 rows with its content aligned to the bottom.
- **About** `.split`: `1fr 1fr`, 56px gap. **Steps**: 3 equal columns, 18px gap.
- **Breakpoint**: a single `max-width: 800px` block that collapses every grid to one column and turns the nav into a dropdown.
- **Radii**: `--r-sm` 14px (inputs), `--r-md` 20px (symbols, vibes, FAQ rows), `--r-lg` 28px (cards, form, quote), `--pill` 999px (buttons, chips, tags, stickers).

## Components

- **Header**: sticky glass (`--header-bg` with a 14px backdrop blur) and a hairline bottom border. Gradient `.mark` logo with a rose glow. Nav links are muted until hovered. `.theme` (a 42px round pill with a gold ☀/☾), `.lang` and `.menu` are glass pills.
- **`.btn`**: gradient pill, min-height 52px, weight 750, `--on-grad` text. On hover it lifts 2px and gains a rose shadow. **`.btn.ghost`** is transparent with a hairline border and a glass fill on hover.
- **`.chip`**: a glass pill prompt in the hero. On hover it lifts and tints rose. It carries `data-service` and `data-prompt`.
- **`.sticker`**: a gold uppercase pill above each section heading.
- **`.ticker`**: a full-bleed band with a `.track` of two identical `.group`s, scrolling over 38s. Each item gets a gold ✦ prefix.
- **`.card`**: a glass panel with a 28px radius. On hover it lifts 4px, brightens its border and strengthens its corner `::after` glow (`--glow` comes from `.c-astro`, `.c-vastu` or `.c-reiki`). It contains a solid-accent `.symbol` tile, an h3, muted copy, `.tags` (hashtag pills) and a gold link.
- **`.quote`**: a wine → plum panel with a glowing gold ॐ and a serif italic line.
- **`.vibe`**: a glass row with an emoji, a bold title and a muted line.
- **`.step`**: a glass card with a gradient `.num`.
- **FAQ**: `<details>` glass rows. The native marker is replaced by a gold "+" that rotates 45° when open, and the open row gets a rose border.
- **`.form`**: a glass panel with a 12px blur. Inputs are dark translucent wells with a rose focus border. Results show **Copy** (ghost) and **Share on WhatsApp** (gradient) side by side.
- **Footer**: a hairline top border with muted text.

## Motion

| Effect | Implementation |
|---|---|
| Mandala rotation | `.spin` group, `transform-origin: 220px 220px`, 90s linear infinite |
| Sparkles | `.spark` ✦ glyphs, 5s `float` (bob, scale and fade) with staggered delays |
| Ticker | `.track` `translateX(-50%)` over 38s, linear infinite |
| Scroll reveal | `.js .reveal` starts at opacity 0 / +24px and goes to `.in` through an IntersectionObserver (threshold .12) |
| Hover | 0.2–0.25s transforms on buttons, chips and cards |

Under `prefers-reduced-motion: reduce`, every animation and transition is turned off, the ticker wraps into a static centered row with its duplicate hidden, and reveals show immediately.

## Iconography and imagery

- The hero mandala is inline SVG: a gradient-stroked (`#sg`) ring, dashed outer circle, 8 `<use>` petals and a diamond with triangles, all rotating. It sits on a dark radial core, with a gradient disc and a dark ॐ in the centre. Gold dots mark the compass points.
- Service glyphs: ☉ Astrology, ◇ Vastu, ✿ Reiki. Emoji are used in chips, vibes and status messages (💼 💞 🏠 🪴 🌙 💬 🧘 🤝 ✨ ✅). Decorative glyphs are `aria-hidden`.
- No raster images or external assets.

## Internationalization

- Text: `data-en` / `data-hi` on every translatable element, swapped through `textContent`. This includes `<title>` and the language button's own label.
- Accessible names: `data-label-en` / `data-label-hi`, swapped into `aria-label`.
- Translatable elements hold plain text only. Styled fragments are separate siblings (e.g. the h1's two `<span>`s).
- The prepared message and copy status come from JS in the active language, and the message rebuilds when the language toggles.
- Hindi copy is written gender-neutral.

## Accessibility

Already in place: a translated skip link, a global `:focus-visible` gold outline, `aria-expanded` and `aria-controls` on the menu, translated `aria-label`s, `lang="hi"` on the Hindi toggle label, a labelled hero SVG, `aria-hidden` on decorative glyphs, emoji and the duplicate ticker, `role="status"` feedback, a `<label>` on every field, and full reduced-motion support. Text colors are light on near-black (`--text` and `--muted` both pass WCAG AA). Gradient buttons use dark text.

## Known inconsistencies

- Glow and shadow `rgba()` tints are hard-coded and identical in both themes. The SVG stops keep hex `stop-color` attributes only as a fallback; CSS overrides them.
- In the light theme the `--violet` token holds marigold (`#f2b233`), so the name no longer describes the color. Consider renaming the symbol tokens by role (`--sym-astro`, etc.).
- Without JavaScript the page always renders dark: the light palette is applied only through the head script.
- Chip prompts are copied into `#message` in whichever language is active at click time, and switching language later doesn't retranslate them.
- The `<meta name="description">` is English only.
- The italic serif accent line has no Devanagari italic, so in Hindi it renders upright in the fallback font.
- Emoji appearance depends on the platform.
