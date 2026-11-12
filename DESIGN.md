# DESIGN.md — Cinematic Motion Portfolio

> Design reference: [Portfolio / Animation — Mike | Creative Mints](https://dribbble.com/shots/24003762-Portfolio-Animation)
> Additional reference: [Creative Mints project](https://creativemints.com/portfolio-animation) · [Behance case study](https://www.behance.net/gallery/196408297/Portfolio-Animation)
> Status: implementation-oriented interpretation, not the original designer's source specification.

## 1. Design intent

Build an immersive, editorial portfolio in which sculptural artwork and motion establish the identity. The experience should feel like an interactive digital art exhibition rather than a conventional SaaS landing page. Prioritize visual hierarchy, restraint, dimensionality and polished transitions.

### Reference observations versus implementation choices

The reference shows a deep blue cinematic scene, a luminous abstract ring with blue, pink and warm orange surfaces, a centered monogram, small uppercase navigation, and a large white serif name layered over the artwork. The creator describes experimentation with movement and evolving styles. Exact typefaces, color values, animation timings and responsive behavior are not published in the material inspected. The tokens, layout rules and interactions below are proposed implementation choices, not measured originals. The full original animation was not available for frame-by-frame inspection.

## 2. Visual language

- Art direction: futuristic editorial, contemporary gallery, cinematic minimalism.
- Mood: mysterious, confident, refined, experimental.
- Composition: one dominant sculptural object; foreground typography; quiet navigation; generous negative space.
- Materials: iridescent glass, polished metal, translucent resin, luminous gradients.
- Lighting: soft cyan rim light, warm internal highlights, directional reflections, subtle contact shadow.
- Avoid generic SaaS cards, heavy borders, excessive neon, large pill buttons, stock illustrations, cluttered dashboards and indiscriminate glassmorphism.

## 3. Color system

Approximate palette inspired by the reference, with accessibility-oriented text choices.

| Token | Value | Purpose |
|---|---|---|
| `--bg-deep` | `#050B1B` | Main canvas and dark edges |
| `--bg-navy` | `#09233F` | Hero environment |
| `--bg-blue` | `#164A70` | Upper background glow |
| `--surface` | `#101D32` | Menus and secondary surfaces |
| `--text-primary` | `#F7F5F2` | Headlines and important text |
| `--text-muted` | `#B4C5D8` | Descriptions and navigation |
| `--accent-gold` | `#FFC18A` | Active nav, small labels |
| `--accent-cyan` | `#25B9F3` | Artwork rim light |
| `--accent-pink` | `#EF438E` | Artwork reflection |
| `--accent-orange` | `#FF925E` | Artwork highlights |
| `--line` | `rgba(180,197,216,.20)` | Dividers and guides |

Use a radial blue glow fading into navy and near-black, not a flat background. Keep saturated accents mostly inside artwork. Use ivory for high-priority text and gold for limited emphasis. Verify actual contrast over artwork; add a dark scrim behind text if required.

```css
:root {
  color-scheme: dark;
  --bg-deep: #050b1b;
  --bg-navy: #09233f;
  --bg-blue: #164a70;
  --surface: #101d32;
  --text-primary: #f7f5f2;
  --text-muted: #b4c5d8;
  --accent-gold: #ffc18a;
  --accent-cyan: #25b9f3;
  --accent-pink: #ef438e;
  --accent-orange: #ff925e;
  --line: rgba(180,197,216,.20);
  --font-display: 'Bodoni Moda', 'Times New Roman', serif;
  --font-body: 'Manrope', Arial, sans-serif;
  --ease-out: cubic-bezier(.22,1,.36,1);
  --ease-in-out: cubic-bezier(.65,0,.35,1);
  --duration-fast: 180ms;
  --duration-normal: 350ms;
  --duration-scene: 900ms;
  --gutter: clamp(20px, 5vw, 80px);
  --content-max: 1440px;
}
.hero {
  background: radial-gradient(ellipse at 50% 8%, var(--bg-blue), var(--bg-navy) 42%, var(--bg-deep) 85%);
  min-height: 100svh;
  position: relative;
  isolation: isolate;
}
```

## 4. Typography

Recommended substitutes, not identified original fonts: Bodoni Moda for display, Manrope for functional text. Self-host licensed WOFF2 files where practical; retain fallback stacks.

| Role | Desktop | Mobile | Style |
|---|---|---|---|
| Hero name / H1 | `clamp(64px, 9vw, 144px)` | `clamp(42px, 11vw, 64px)` | Serif, 400, line-height .94–1.04, tracking -.045em |
| Section H2 | 64–88px | 38–52px | Serif, 400, line-height 1.04 |
| Project H3 | 32–48px | 28–36px | Serif, 400 |
| Body | 16–18px | 16px | Sans, 400–500, line-height 1.65 |
| Navigation | 12–13px | 14px | Sans, 600, uppercase, tracking .08em |
| Eyebrow | 11–13px | 11–12px | Sans, 600, uppercase, tracking .24em–.35em |

Use oversized type sparingly. A hero name may appear uppercase, centered and visually layered in front of the artwork. Keep ordinary paragraphs in sentence case and limited to roughly 60–70 characters per line. Small decorative labels must never carry essential information alone.

## 5. Layout and spacing

- Desktop: 12-column grid, 24px gaps, fluid outer gutters, maximum content width 1440px.
- Tablet: 8 columns, 20px gaps; mobile: 4 columns, 16px gaps.
- Spacing scale (px): 4, 8, 12, 16, 24, 32, 48, 64, 96, 128.
- Section padding: 96–128px desktop, 64–80px mobile.
- Hero occupies at least one small viewport height; content may expand vertically on short screens.
- Keep the page in normal document flow; no global scroll hijacking.
- Layer order: background (0), artwork (1), optional text scrim (2), hero copy (3), navigation and controls (4), dialogs (10).

### Hero composition

```text
+----------------------------------------------------------------+
| ABOUT          WORK          [MONOGRAM]       SHOP    CONTACT  |
|                                                                |
|                     ABSTRACT 3D SCULPTURE                      |
|                  /                         \\                  |
|    PREV         |    luminous glass ring    |          NEXT    |
|                  \\                         /                  |
|                         ILLUSTRATION                           |
|                        PORTFOLIO NAME                          |
|                              ◆                                 |
|                       GENERATIVE DESIGN                        |
|                                                                |
|                      01 / 03    Scroll ↓                       |
+----------------------------------------------------------------+
```

The diagram describes a suggested layout. The original visible design contains a centered mark, split navigation, artwork, overlaid name, labels and subtle side indicators. Slide numbering and scroll prompt are optional extensions.

- Header: balanced left and right navigation groups around a centered monogram; desktop height 80–100px.
- Artwork: centered, roughly 55–72% of hero width on desktop, with a height cap of about 65vh; maintain its aspect ratio.
- Copy: near the lower third of the hero, overlapping the lower portion of the visual; headline always remains legible.
- Controls: minimal side arrows with faint guide lines; expose accessible names and 44px minimum hit areas.
- Mobile: compact logo/menu header, artwork centered above or partially behind headline, arrows below artwork or within a bottom control row. Do not clip essential text.

## 6. Site structure

The following sections are proposed for a usable portfolio beyond the visible reference hero.

| Section | Content | Layout |
|---|---|---|
| Hero | Identity, discipline, featured sculpture | Full-height immersive scene |
| Selected work | 3–6 projects, role, year, summary | Large editorial image-led rows or two-column grid |
| Project detail | Challenge, contribution, outcome, media | Long-form case study |
| About | Short bio, capabilities, portrait optional | Asymmetric text and image |
| Shop (optional) | Real products or resources | Simple editorial grid; omit if not needed |
| Contact | Email, availability, social links | Large serif call to action |
| Footer | Copyright, navigation, credits | Compact, muted |

Do not invent client logos, testimonials, project outcomes or products. Replace reference name and monogram with the actual portfolio owner's identity. Only include Shop if it has real content.

## 7. Component specifications

### Header / navigation
- Transparent over hero; use an opaque navy surface when necessary for contrast on scroll.
- Split navigation with central logo on desktop. Mobile uses a labeled menu button and collapsible navigation.
- Active link uses gold text and an additional underline or marker, not color alone.
- Hover: subtle color transition; focus: visible 2px outline with 4px offset.
- Use semantic links, a skip link and `aria-current` where appropriate.

### Hero artwork
- Prefer an original GLB/glTF sculptural asset or a licensed pre-rendered image/video.
- The signature form is an abstract twisted torus with cyan exterior, orange interior highlights and pink reflections.
- Model should have believable thickness, bevels, specular reflections and a strong silhouette.
- Use soft area/environment lighting and a restrained background glow; avoid decorative particle overload.
- Keep artwork separate from HTML copy. Never bake navigation or primary headings into an image.
- Static image fallback must preserve the composition when WebGL/video is unavailable.

### Featured project selector
- Previous/next buttons, optional current/total count; controls remain keyboard accessible.
- One active scene at a time. On change, update artwork, project label and title together.
- Use a 700–1000ms crossfade/transform transition; prevent conflicting transitions during rapid input.
- Default to manual navigation; optional autoplay must have a pause control and stop on interaction.
- Announce user-triggered changes through a polite live region without announcing continuous animation.

### Project cards
- Use artwork-first rectangular previews (typically 4:3 or 16:10).
- Title, discipline, year and short description below the media.
- Minimal or no border radius (0–8px); no generic elevated card shadows.
- Hover: image scale up to 1.035 and a subtle arrow movement; focus offers equivalent affordance.
- Entire project link has a descriptive accessible name; no nested interactive controls.

### Buttons and links
- Primary CTA: text link with directional arrow, or restrained outlined button.
- Secondary: understated uppercase link.
- Minimum target size 44×44px for important controls.
- Disabled state only where meaningful; never make navigation depend solely on animation.

## 8. Motion system

Motion is a design feature, not decoration. Animate hierarchy and relationships; avoid simultaneous competing effects.

| Interaction | Duration | Behavior |
|---|---|---|
| Initial artwork reveal | 900–1200ms | Opacity 0→1, scale .96→1 |
| Headline entrance | 650–850ms | Translate Y 24px→0, opacity reveal |
| Label entrance | 400–600ms | Fade with 80–120ms stagger |
| Scene change | 700–1000ms | Crossfade, subtle rotation or scale |
| Hover/focus | 150–250ms | Color, underline or small translation |
| Scroll section reveal | 500–700ms | Opacity and Y 16–24px |
| Ambient artwork drift | 8–14s | Small float or restrained rotation |

### Hero choreography (suggested)
1. 0–250ms: background and navigation establish the scene.
2. 100–1100ms: sculpture fades into view.
3. 350–1050ms: main headline rises into place.
4. 600–1250ms: supporting labels and controls appear.
5. After entrance: optional subtle ambient motion; pause when offscreen.

Use `transform` and `opacity` for DOM animations. Keep pointer parallax optional, limited to ~8px translation or ~3° tilt, disabled on touch and reduced-motion settings. Avoid perpetual animation on text. Do not lock content behind a preloader.

```css
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  .motion-layer, .hero-art, .hero-title, .reveal {
    animation: none !important;
    transition: none !important;
    transform: none !important;
    opacity: 1 !important;
  }
}
```

In JavaScript also observe reduced-motion preference: stop ambient loops, disable pointer tracking and use static scene changes. Do not depend on CSS alone to disable WebGL animation.

## 9. Responsive behavior

| Width | Rules |
|---|---|
| < 640px | Single-column layout, compact menu, poster-first hero, 20px gutters |
| 640–1023px | Balanced artwork and type, 8-column grid, simplify controls |
| 1024–1439px | Full editorial composition, split nav, large artwork |
| ≥ 1440px | Center content within max width; allow background to bleed full screen |

Test at 320, 390, 768, 1024, 1440 and 1920px, including landscape mobile. No horizontal overflow. Support browser zoom up to 200%; allow hero height to grow when text wraps. Respect safe-area insets for edge controls.

## 10. Accessibility

Target WCAG 2.2 AA. Validate contrast at least 4.5:1 for normal text and 3:1 for large text and relevant UI boundaries. Check contrast throughout moving scenes, not only on the first frame.

- Semantic landmarks: header, nav, main, section, footer; one primary H1.
- Keyboard navigation, visible focus, logical DOM order, accessible mobile menu with Escape support and focus restoration.
- Decorative artwork uses empty alt or aria-hidden; informative project artwork has meaningful alt text.
- Provide pause/stop controls for qualifying automatically moving content; no rapid flashes.
- No critical information conveyed solely through color, motion, hover or 3D rendering.
- Contact forms, if used, have labels, errors and submission feedback.
- Ensure essential content is usable without JavaScript and when images fail.

## 11. Implementation guidance

Suggested stack (not required): Next.js + TypeScript + Tailwind CSS, with CSS or GSAP for motion and React Three Fiber/Three.js only when a real interactive 3D object adds value. A static HTML/CSS/JS implementation with pre-rendered assets is also valid. Use one motion library at most unless there is a specific need.

Suggested component structure:

```text
app/
  page.tsx
  layout.tsx
  globals.css
components/
  Header.tsx
  Hero.tsx
  HeroArtwork.tsx
  SceneControls.tsx
  ProjectGrid.tsx
  ProjectCard.tsx
  About.tsx
  Contact.tsx
  Footer.tsx
public/
  artwork/
    hero-poster.webp
    hero.glb            # optional
    hero-loop.webm      # optional alternative
  fonts/
  projects/
DESIGN.md
```

Store content separately from rendering. A project record should contain `id`, `title`, `discipline`, `year`, `description`, `image`, `imageAlt`, and `href`. Featured scene data may add `poster`, `model` or `video` and a background theme. Never require all three media variants to load.

### Performance budgets (targets)
- LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1 at the 75th percentile after deployment.
- Hero poster target ≤ 350KB where quality permits; responsive AVIF/WebP for projects.
- Lazy-load below-fold media and heavy 3D modules; prioritize the hero poster only.
- If using WebGL, cap device pixel ratio around 1.5–2, optimize textures and geometry, and pause rendering when hidden/offscreen.
- Use a poster on low-power devices or failed rendering; avoid loading both large video and GLB by default.
- Reserve image dimensions to avoid layout shift. Fonts use `font-display: swap`.
- Test on a mid-range Android device and throttled mobile network; favor smooth, reliable interaction over visual complexity.

## 12. Design QA and acceptance criteria

- [ ] The opening screen reads as a cinematic editorial portfolio, not a dashboard.
- [ ] A single sculptural focal point dominates the scene.
- [ ] Large serif type, compact navigation and strong negative space establish hierarchy.
- [ ] Artwork and typography remain readable at every viewport and animation state.
- [ ] Navigation, project selection and contact links actually work.
- [ ] Animations are purposeful, interruptible and respect reduced motion.
- [ ] Static fallback works without WebGL and essential content works without JS.
- [ ] Keyboard, touch, focus, contrast and zoom have been tested.
- [ ] No placeholder assets, broken links, fake claims or console errors remain.
- [ ] Asset licenses and attribution are documented.

## 13. Instructions for AI coding agents

Treat this file as the visual and interaction contract. Preserve the cinematic composition, restrained navigation, serif/sans contrast, deep navy palette and sculptural focal point. Implement a functional semantic layout first, then progressively enhance with motion. Reuse tokens instead of scattering hard-coded values. Build real navigation and project links, use the actual owner's identity, and prioritize mobile accessibility and performance. Do not substitute a generic gradient SaaS hero or card-heavy template. If no 3D asset is available, use a locally supplied original or licensed poster and document the missing asset rather than pretending it exists. Do not copy the reference designer's logo, artwork or exact identity without permission. 
