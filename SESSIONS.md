# Sessions

Log of work sessions on this repository, newest first. Each entry records what changed, decisions made, and open follow-ups.

## 2026-11-12: Claude Code setup, design documentation and Gen Z redesign

**Changes**
- `index.html`: redesigned for Gen Z appeal:
  - Look: a dark cosmic theme with a saffron → rose → violet gradient and a bold sans plus italic serif headline.
  - New pieces: tap-to-start prompt chips, a marquee ticker, a bento services grid with hashtag tags, "vibe" rows in About, a new "How it works" anchor, and two new FAQs (horoscope vs consultation, first-timers).
  - Form: a WhatsApp share button.
  - Motion: a spinning mandala, sparkles and scroll reveals, all off under reduced motion.
  - Copy: rewritten in a casual voice in both languages, keeping every disclaimer and adding mental health care to the Reiki disclaimer.
  - The file is no longer minified.
- `index.html`: added a light/dark theme toggle (☀/☾ button in the header). The light theme is a warm saffron palette: cream background, maroon-brown text, a burnt saffron → maroon gradient with white button text. Colors that differ by theme are now tokens, including the SVG gradient stops. A head script applies the saved or OS theme before first paint, and the button label is translated.
- `CLAUDE.md`: added guidance for Claude Code covering the single-file structure, how to preview, the bilingual `data-en`/`data-hi` mechanism, the consultation form, nav behavior, and content tone.
- `.claude/skills/design-sessions/SKILL.md`: added a project skill that generates DESIGN.md from the source and keeps SESSIONS.md as an append-only log.
- `DESIGN.md`: extracted the design system (tokens, typography, layout, components, i18n, accessibility, inconsistencies) from `index.html`.
- `SESSIONS.md`: created this log, backfilled from git history.
- `.claude/skills/design-sessions/SKILL.md`: extended the skill to also generate AGENTS.md and GEMINI.md.
- `AGENTS.md`: added tool-neutral agent instructions derived from CLAUDE.md, plus pointers to DESIGN.md and SESSIONS.md.
- `GEMINI.md`: added a thin Gemini CLI wrapper that imports AGENTS.md with `@./AGENTS.md`.
- `CLAUDE.md`, `AGENTS.md`, `DESIGN.md`: updated for the redesign (new tokens, motion, `data-label-*` i18n, chips, WhatsApp link, a headless Chrome screenshot recipe, Gen Z voice rules).

**Decisions**
- No build tooling or tests were introduced. The site stays a single self-contained `index.html`.
- DESIGN.md documents the code as it is; inconsistencies are listed rather than fixed.
- CLAUDE.md is the single source of agent guidance. AGENTS.md is derived from it, and GEMINI.md imports AGENTS.md rather than duplicating it, so the three can't drift apart.
- Redesign: dark-only theme, with the heritage cues (ॐ, mandala, wine quote panel) kept so older visitors still recognise the brand. System fonts only, so the page stays self-contained. Hindi copy is gender-neutral. WhatsApp sharing goes through `wa.me/?text=` with no phone number, because no real contact number exists in the repo.
- Verified with headless Chrome: desktop at 1366px, mobile in a 390px iframe, plus a scripted Hindi toggle and form submit (Hindi message, translated `aria-label`s and WhatsApp URL confirmed).

**Follow-ups**
- [x] Translate the prepared consultation message, footer brand and © line, `<title>` and `aria-label`s for Hindi mode. (The meta description is still English only.)
- [x] Consolidate colors into tokens. Superseded by the new token set; remaining hard-coded `rgba` glows and SVG stops are listed in DESIGN.md.
- [x] Add hover states for `.btn`, nav links and card links.
- [x] Mark the `.symbol` glyphs `aria-hidden="true"`.
- [x] Drop `'Noto Serif Devanagari'` from the heading font stack.
- [ ] Add the business's real WhatsApp number (`wa.me/<number>?text=`) so shares go straight to them.
- [x] Add a light theme. Done as the saffron theme, selectable with the header toggle and defaulting to the OS preference. Verified with headless Chrome (desktop and 390px mobile renders, plus a scripted toggle confirming the saved choice, `theme-color` and the translated label).
- [ ] Rename the symbol color tokens by role, since `--violet` is marigold in the light theme.
- [ ] Re-translate a chip prompt in `#message` when the language toggles.
- [ ] Commit CLAUDE.md, DESIGN.md, SESSIONS.md, AGENTS.md, GEMINI.md and `.claude/` (currently untracked).

## 2026-11-12: Initial site (backfilled from git history)

**Changes**
- `LICENSE`: initial commit (`2fb74ca`).
- `shri-rudraksh-jyotish.html`: added the full single-page site with inline styles and script (`be32e37`).
- Renamed `shri-rudraksh-jyotish.html` to `index.html` so it serves as the GitHub Pages root (`7a911e1`).
