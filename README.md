# Aishwarya Murali — Portfolio Website

**Live site:** [aishwaryamurali-bi.github.io](https://aishwaryamurali-bi.github.io)

A personal portfolio website for Aishwarya Murali, Senior Analytics Manager & BI Lead. Built with Tailwind CSS, Google Fonts, and custom animated illustrations.

---

## Built with Claude

This website was designed and built through an **iterative collaboration with [Claude](https://claude.ai) (Anthropic)** using [Claude Code](https://docs.anthropic.com/en/docs/claude-code), Anthropic's agentic coding tool. The entire project — from initial design to deployment — was completed through natural language conversation with Claude.

### The AI-Assisted Workflow

| Phase | What Happened | Tools Used |
|-------|---------------|------------|
| **1. Reference-Driven Design** | Provided a reference screenshot and CSS properties. Claude generated pixel-accurate HTML/Tailwind implementations. | Claude Code |
| **2. Automated Screenshot Comparison** | Claude used Puppeteer to render the page, then compared screenshots against the reference image, identifying mismatches down to specific pixel measurements. | Puppeteer |
| **3. Iterative Refinement** | Multiple rounds of render-compare-fix (2-5 passes per page) until output matched the reference within ~2-3px accuracy. | Claude Code + Puppeteer |
| **4. Multi-Page Expansion** | Extended from a single landing page to a full 4-page portfolio site, maintaining consistent design system across all pages. | Claude Code |
| **5. GIF Processing** | Used Sharp (Node.js) to analyze, trim, and optimize animated GIF illustrations — removing flash frames and adjusting timing. | Sharp |
| **6. Asset Blending** | Solved GIF-to-background color blending using CSS `mix-blend-mode` and `filter` properties, achieving seamless integration. | CSS |

### What This Demonstrates

- **Prompt Engineering** — The [`CLAUDE.md`](CLAUDE.md) file is a reusable system prompt that defines a reproducible screenshot-comparison workflow for design recreation
- **Iterative AI Collaboration** — Not "generate and done" — systematic refinement loops with automated quality checks
- **Tool Orchestration** — Combining Claude with Puppeteer (browser rendering), Sharp (image processing), and Git (version control) in a unified workflow
- **Quality Control** — Pixel-level accuracy standards enforced through automated screenshot comparison
- **Problem Solving** — Debugging CSS blend modes, GIF animation artifacts, and cross-page design consistency through conversation

See [`process/README.md`](process/README.md) for a detailed narrative of the build evolution.

---

## Tech Stack

- **HTML5** + **Tailwind CSS** (via CDN)
- **Google Fonts** — Inter (sans-serif), Playfair Display (serif italic)
- **Animated GIF illustrations** with CSS blend-mode integration
- **No build step** — pure static files, zero dependencies in production

## Pages

| Page | File | Description |
|------|------|-------------|
| **Home** | `index.html` | Hero section with animated illustration, navigation |
| **Work** | `works.html` | Project showcases, open source repos, impact metrics |
| **About** | `about.html` | Background, experience timeline, skills, approach methodology |
| **Contact** | `contact.html` | Email, social links, animated illustration |

## Development Tools (used during build, not in production)

- **Puppeteer** — Headless Chrome for automated screenshot comparison
- **Sharp** — Node.js image processing for GIF frame analysis and trimming
- **Claude Code** — AI-assisted development via natural language

---

## License

This project is open source. Feel free to use the workflow patterns and [`CLAUDE.md`](CLAUDE.md) specification for your own projects.
