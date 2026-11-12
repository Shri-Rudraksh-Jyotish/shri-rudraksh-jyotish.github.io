# Sessions

Log of work sessions on this repository, newest first. Each entry records what changed, decisions made, and open follow-ups.

## 2026-11-12: Claude Code setup and design documentation

**Changes**
- `CLAUDE.md`: added guidance for Claude Code covering the single-file structure, how to preview, the bilingual `data-en`/`data-hi` mechanism, the consultation form, nav behavior, and content tone.
- `.claude/skills/design-sessions/SKILL.md`: added a project skill that generates DESIGN.md from the source and keeps SESSIONS.md as an append-only log.
- `DESIGN.md`: extracted the design system (tokens, typography, layout, components, i18n, accessibility, inconsistencies) from `index.html`.
- `SESSIONS.md`: created this log, backfilled from git history.
- `.claude/skills/design-sessions/SKILL.md`: extended the skill to also generate AGENTS.md and GEMINI.md.
- `AGENTS.md`: added tool-neutral agent instructions derived from CLAUDE.md, plus pointers to DESIGN.md and SESSIONS.md.
- `GEMINI.md`: added a thin Gemini CLI wrapper that imports AGENTS.md with `@./AGENTS.md`.

**Decisions**
- No build tooling or tests were introduced. The site stays a single self-contained `index.html`.
- DESIGN.md documents the code as it is; inconsistencies are listed rather than fixed.
- CLAUDE.md is the single source of agent guidance. AGENTS.md is derived from it, and GEMINI.md imports AGENTS.md rather than duplicating it, so the three can't drift apart.

**Follow-ups**
- [ ] Translate the prepared consultation message, footer brand and © line, `<title>`/meta description and `aria-label`s for Hindi mode.
- [ ] Use `var(--gold)` in place of hard-coded `#b87827`, and consolidate the near-duplicate off-white, cream and border colors into tokens.
- [ ] Add hover states for `.btn`, nav links and card links.
- [ ] Mark the `.symbol` glyphs `aria-hidden="true"`.
- [ ] Load or drop `'Noto Serif Devanagari'` from the heading font stack.
- [ ] Commit CLAUDE.md, DESIGN.md, SESSIONS.md, AGENTS.md, GEMINI.md and `.claude/` (currently untracked).

## 2026-11-12: Initial site (backfilled from git history)

**Changes**
- `LICENSE`: initial commit (`2fb74ca`).
- `shri-rudraksh-jyotish.html`: added the full single-page site with inline styles and script (`be32e37`).
- Renamed `shri-rudraksh-jyotish.html` to `index.html` so it serves as the GitHub Pages root (`7a911e1`).
