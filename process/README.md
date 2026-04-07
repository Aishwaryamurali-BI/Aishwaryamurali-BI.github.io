# Build Process — Claude-Assisted Portfolio Website

This document narrates how this portfolio website was built through iterative collaboration with Claude, Anthropic's AI assistant, using Claude Code.

---

## Phase 1: Initial Design Recreation
**Goal:** Recreate a reference design (HuyPhan portfolio) as the starting template.

- Provided a screenshot of [huyml.co](https://huyml.co) along with CSS properties (background color, font family, line-height, etc.)
- Claude generated the initial `index.html` using Tailwind CSS via CDN
- Installed Node.js and Puppeteer for automated screenshot comparison
- Ran **8 iteration rounds** — each round: render page → screenshot → compare against reference → identify mismatches → fix → re-render
- Key refinements: hero typography sizing (Playfair Display italic for first name, Inter bold for last name), navigation spacing, sparkle icon SVGs, section positioning

**Challenges solved:**
- Node.js wasn't installed — Claude installed it via `winget`, then installed Puppeteer locally
- Puppeteer Chrome sandbox issues on Windows — resolved with `--no-sandbox` flag
- Font size calibration — used `vw` units with `min()` capping to prevent text overflow at large viewports

## Phase 2: Content Personalization
**Goal:** Transform the template into Aishwarya Murali's portfolio.

- Changed all text content: name, title, bio, navigation labels
- Replaced "HUYML" branding with "AM"
- Updated navigation from 4 items to 3 (About, Works, Contact)
- Changed year from 2022 to 2026
- Modified tagline and descriptive text

## Phase 3: Multi-Page Expansion
**Goal:** Create dedicated About, Works, and Contact pages.

- Fetched reference pages from huyml.co (About and Contact) using WebFetch to understand layout patterns
- Pulled GitHub repository data via API to populate the Works page with real projects:
  - `fabric-end-to-end-analytics`
  - `copilot-nl-query-showcase`
  - `Enterprise-Semantic-Layer-Governance-Framework-Design`
- Built all 3 sub-pages with consistent navigation and design language
- Added resume content (experience, education, certifications, skills) to About page

## Phase 4: Design System Overhaul
**Goal:** Match all pages to a refined, polished design system.

The index.html was redesigned externally with a new white/minimal aesthetic featuring:
- Sticky header with backdrop blur and "Email me" CTA button
- Timeline-style experience section with colored badges
- Custom color tokens (`#000000a8`, `#0000008c`, `#00000014`)
- Multi-column footer

Claude detected the design change and updated all sub-pages to match:
- Consistent `max-w-[1200px]` container with `px-8` padding
- Matching sticky headers, footers, and typography hierarchy
- Active page indicator (underline) in navigation
- Unified section label style (uppercase, `text-xs`, `tracking-wider`)

## Phase 5: Background Color Unification
**Goal:** Ensure consistent background across all pages.

- Index page used `rgb(235, 235, 235)` (light gray)
- Sub-pages used white (`#ffffff`)
- Updated all pages to match index: `rgb(235, 235, 235)`
- Adjusted sticky header backgrounds to `rgba(235,235,235,0.95)` for consistency

## Phase 6: Illustration Integration
**Goal:** Add animated GIF illustrations that blend seamlessly with the page.

**Index page illustration:**
1. First attempt: inline SVG illustration (person at desk with monitor, bar chart, coffee mug, plant)
2. Second attempt: more detailed SVG matching a reference style (person on chair with laptop, cat, lightbulb)
3. Final: user provided an animated GIF (`illustration 1.gif`)
4. **Blending challenge:** GIF had a different background color than the page, creating a visible rectangle
5. Tested `mix-blend-mode: multiply`, `darken`, `lighten` with various `filter: brightness()` values
6. **Solution:** `mix-blend-mode: darken` + `filter: brightness(1.12) contrast(1.08)` eliminated the color mismatch

**Contact page illustration:**
- Same blending approach applied successfully
- GIF had a darker gray background — same `darken` + brightness/contrast solution worked

**GIF flash fix:**
- Both GIFs had a blank/flash frame at the start of each animation loop
- Used Sharp (Node.js image library) to analyze frame data: 91 frames, ~65ms delays
- Trimmed first 15 frames (~1 second) using Sharp's `page` and `pages` parameters
- Saved as `_trimmed.gif` versions — flash eliminated

## Phase 7: Profile Photo & Final Polish
**Goal:** Add profile photo to About page and finalize.

- LinkedIn profile photo couldn't be fetched programmatically (blocked by LinkedIn)
- User saved photo manually to project directory
- **Placement iterations:**
  1. v1: Large circle (180px) in top-right, aligned with page title — dark ring from original photo visible
  2. v2: Zoomed 115% with offset margins — cut off on right side
  3. v3: Flexbox-centered at 120% scale — still cut off
  4. **Final:** Compact layout — 120px circle inline with name/title/location badge, followed by bio text in a clean 2-column grid. No wasted space.
- Removed "Background" section label per user feedback

---

## Key Takeaways

1. **Iterative refinement beats one-shot generation** — Every page went through 2-8 rounds of render → compare → fix
2. **CSS blend modes solve asset integration** — `mix-blend-mode: darken` with brightness/contrast filters can make any illustration blend into any background
3. **Sharp is powerful for GIF manipulation** — Frame-level analysis and trimming without external tools
4. **Design systems enforce consistency** — Once the color tokens and layout patterns were established, extending to new pages was straightforward
5. **Claude + Puppeteer = automated QA** — Screenshot comparison provides objective quality measurement rather than subjective "looks good enough"
