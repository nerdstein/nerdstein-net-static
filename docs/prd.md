# Product Requirements Document: nerdstein.net Static Site Migration

**Version**: 1.1
**Date**: 2026-05-07
**Author**: Sarah (Product Owner)
**Quality Score**: 91/100

---

## Executive Summary

nerdstein.net is a Drupal 9 site running on a Linode VPS with a Tugboat staging environment. The site is a personal blog and professional presence for Adam Bergstein — a product engineering leader and Drupal community contributor. The current setup requires ongoing server maintenance, hosting costs, and operational overhead that no longer fits the site's purpose as a low-update, content-first blog.

This project migrates nerdstein.net to a Hugo-based static site hosted on Cloudflare Pages (free tier), backed by a GitHub repository. All content is stored as markdown files with frontmatter. New posts are authored by prompting Claude Code, which generates the markdown file, followed by a `git push` that auto-deploys via Cloudflare Pages. The end state is zero hosting cost, zero server maintenance, and a modernized design that preserves the site's brand identity.

The project is complete when nerdstein.net resolves to Cloudflare Pages, all content is migrated and verified, and Linode/Tugboat are decommissioned.

---

## Problem Statement

**Current Situation**: nerdstein.net runs on Drupal 9 on a Linode VPS, with Tugboat for staging. This requires ongoing server maintenance, security patching, hosting costs, and a complex CMS workflow. A full content audit reveals **114+ pieces of content** spanning over a decade of writing — far more than previously estimated.

**Proposed Solution**: Replace the entire stack with a Hugo static site in a GitHub repository, deployed automatically to Cloudflare Pages on every `git push`. Blog posts are markdown files. New posts are created by prompting Claude Code or editing markdown files directly.

**Business Impact**:
- Eliminate Linode VPS hosting costs
- Eliminate Tugboat staging costs
- Eliminate Drupal security patching and maintenance overhead
- Publishing a new post becomes a `git push` (or a Claude Code prompt + push)
- Cloudflare CDN gives faster global performance for free

---

## Success Metrics

**Primary KPIs:**
- **Infrastructure shutdown**: Linode VPS and Tugboat fully decommissioned with no active invoices
- **Content completeness**: All 114+ posts and pages migrated with no content loss (see full content audit in Appendix)
- **URL preservation**: All existing paths (e.g., `/blog/drupalcon-2022-recap`, `/litmus-test-ai-application`) resolve correctly on the new site
- **Live deployment**: nerdstein.net DNS resolves to Cloudflare Pages with valid HTTPS

**Validation**: The project is complete when all four criteria above are met and the author can publish a new blog post end-to-end using only Claude Code and `git push`.

---

## User Personas

### Primary: Adam (Author)
- **Role**: Site owner and sole content creator
- **Goals**: Publish blog posts occasionally with minimal friction; maintain a professional web presence; stop paying for and maintaining servers
- **Pain Points**: Drupal is overkill for a personal blog; server maintenance is a distraction; logging into a CMS to write a post is slower than just writing markdown
- **Technical Level**: Advanced — comfortable with git, CLI tools, and Claude Code

### Secondary: Reader
- **Role**: Colleague, community member, or recruiter visiting the site
- **Goals**: Read blog posts, learn about Adam's background
- **Pain Points**: Slow page loads, broken links
- **Technical Level**: Not relevant — they just want fast pages and working URLs

---

## User Stories & Acceptance Criteria

### Story 1: Publish a New Blog Post

**As an** author
**I want to** describe a blog post to Claude Code and have it generate a markdown file with proper frontmatter
**So that** I can review, optionally edit, and publish by running `git push`

**Acceptance Criteria:**
- [ ] Running a Claude Code prompt like "write a blog post about X" creates a new `.md` file in `content/blog/` with correct frontmatter (title, date, slug, tags, description, draft: false)
- [ ] The generated slug matches the intended URL path
- [ ] A `git push` to `main` triggers an automatic Cloudflare Pages build and deploy within 2 minutes
- [ ] The post appears on the site at `/blog/{slug}` immediately after deploy

### Story 2: Migrate Existing Content

**As an** author
**I want to** all existing nerdstein.net content automatically converted to markdown
**So that** no historical posts, images, or pages are lost during the migration

**Acceptance Criteria:**
- [ ] All blog posts under `/blog/*` and standalone pages (`/litmus-test-ai-application`, `/simplytestme-partners-program`) are converted to markdown files
- [ ] Post publish dates, titles, tags, and slugs are preserved in frontmatter
- [ ] All images embedded in posts are downloaded and referenced locally (no external Drupal file URLs)
- [ ] Home and About pages exist as Hugo pages; About content is rewritten (new copy, same spirit)
- [ ] Taxonomy tags (drupal, politics, etc.) are preserved and functional

### Story 3: Preserve Existing URLs

**As a** reader following an old link
**I want to** reach the correct page on the new site
**So that** search engine rankings and shared links are not broken

**Acceptance Criteria:**
- [ ] All `/blog/*` paths resolve to the same slug on the new site
- [ ] `/about` resolves to the About page
- [ ] `/litmus-test-ai-application` and `/simplytestme-partners-program` resolve correctly
- [ ] Any paths that cannot be preserved have a `_redirects` entry routing to the correct page
- [ ] No 404s for any URL that currently returns 200 on nerdstein.net

### Story 4: Modern Refreshed Design

**As a** reader
**I want to** experience a clean, fast, modern version of nerdstein.net
**So that** the site feels current without losing its familiar character

**Acceptance Criteria:**
- [ ] Single-column layout — sidebar is fully removed
- [ ] Horizontal top nav with logo top-left, Home / About links, social icons
- [ ] Logo (`logo.png`) carried over from Drupal theme
- [ ] Homepage hero includes a hand-drawn/sketchy SVG illustration
- [ ] Post list is chronological, grouped by month/year, with title + excerpt + tags
- [ ] Per-post pages include optional category-based sketch doodle
- [ ] Subtle creative details: sketch-style dividers, brush-stroke link hover animation
- [ ] Typography: Instrument Serif headings, system-ui body, JetBrains Mono code
- [ ] Color: warm near-white background, near-black text, orange `#e8720c` accent
- [ ] Tags displayed as inline `#hashtag` text, not colored boxes
- [ ] Site is mobile-responsive (nav collapses on small screens)
- [ ] HTTPS enforced via Cloudflare

### Story 5: Shut Down Old Infrastructure

**As an** author
**I want to** decommission Linode VPS and Tugboat
**So that** I have no ongoing hosting costs or maintenance obligations for the old stack

**Acceptance Criteria:**
- [ ] nerdstein.net DNS is pointed to Cloudflare Pages and live for at least 48 hours before Linode is terminated
- [ ] Linode VPS is terminated (no further billing)
- [ ] Tugboat environment is deleted (no further billing)
- [ ] A final database export/backup of Drupal content is archived locally before shutdown

---

## Functional Requirements

### Phase 0: Design System

**Goal**: Define a cohesive, production-ready design system synthesized from the best personal and product blogs on the web. The design must feel editorially serious, personally human, and subtly creative — without being decorative or noisy.

---

#### Design Inspiration Research

Ten sites were reviewed in detail: taniarascia.com, ma.tt, fromjason.xyz, sj.land, stefanzweifel.dev (personal blogs) and Linear, Notion, HelpScout, Descript, SavvyCal (product/SaaS blogs). The following is a synthesis of what the best among them do, and what nerdstein.net should take from each.

| Site | What to Take |
|------|-------------|
| **Linear blog** | Inter Variable font; tight typographic scale; animated underlines (1.5px, 2.5px offset); dark-capable palette |
| **taniarascia.com** | Warm beige background (`#fdf9ee`); custom SVG illustration system per category; code blocks with macOS terminal chrome and copy button; 760px content width |
| **HelpScout blog** | Author metadata line (name · date · read time); pull quote / callout block styling; CSS custom property design token system |
| **fromjason.xyz** | Dropcaps on first paragraph; ornamental SVG dividers between sections; "weird web" decorative personality; `<blockquote>` with sketch-style left border |
| **ma.tt** | Proof that single-column + system fonts + 940px width is enough; reverse-chronological post list without cards or images |
| **stefanzweifel.dev** | Minimal top nav (About · Articles · Archive · Uses); grouped post list (MM/YYYY dates); "Selected Writing" framing over raw listing |
| **Notion blog** | Grid-based post listing with topic filter tabs; clean card with topic tag above title; consistent thumbnail/no-thumbnail handling |
| **Descript blog** | Bold editorial headings; animated hover underlines on post titles; category-based post browsing |
| **SavvyCal blog** | Maximum white space; content-before-decoration principle; no nav clutter |
| **sj.land** | Multi-color semantic tag system; keyboard shortcut hints; curated "selected writing" over full archive on homepage |

---

#### Synthesized Design Direction: Warm Editorial + Illustrated Personality

This design is single-column and editorially clean (Linear, ma.tt, SavvyCal), warmed with a beige background and serif headings (taniarascia), animated with subtle brush-stroke link effects and hand-drawn SVG illustrations (fromjason, taniarascia), and structured with product-blog-grade metadata and callout components (HelpScout, Notion).

---

#### Layout System

```
┌─────────────────────────────────────────────────────────────────────┐
│  VIEWPORT                                                           │
│                                                                     │
│         ┌───────────────────────────────────────────┐              │
│         │  MAX-WIDTH: 720px  (content)               │              │
│         │  OUTER PADDING: 24px each side             │              │
│         └───────────────────────────────────────────┘              │
│                                                                     │
│  Nav bar spans full viewport width, content inside stays at 720px  │
└─────────────────────────────────────────────────────────────────────┘
```

- **Content max-width**: `720px` — matches taniarascia's 760px content zone, wider than ma.tt's 940px outer (which is single-column already)
- **Outer container**: `1200px` max-width, centered, `padding: 0 24px`
- **No sidebar** at any breakpoint
- **Breakpoints**: Mobile < 640px (nav collapses, padding reduces to 16px); Tablet 640–1024px (full layout, slightly tighter); Desktop 1024px+

---

#### Navigation

Taken from: stefanzweifel.dev (minimal horizontal, left-logo / right-links), Linear (clean link spacing), SavvyCal (breathes, no clutter).

```
┌────────────────────────────────────────────────────────────────────┐
│  [logo]  nerdstein.net            writing  about  archive          │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │
│                                                       [social row] │
└────────────────────────────────────────────────────────────────────┘
```

- Logo left (existing `logo.png`), nav links right: **writing**, **about**, **archive**
- Below the nav rule: a small social icon row (GitHub, LinkedIn, Twitter/X) — inline SVGs, not image files
- No hamburger on desktop; on mobile, nav links stack vertically below logo
- Nav border: a single `1px` rule in `#e5e2db` (warm gray) — not a heavy divider

---

#### Homepage Layout

Taken from: ma.tt + stefanzweifel.dev (post list format), taniarascia (hero illustration), fromjason (ornamental details), sj.land (curated "selected writing" framing).

```
┌───────────────────────────── 720px ────────────────────────────────┐
│                                                                    │
│  [nav]                                                             │
│                                                                    │
│  ┌───────────────────────────────────────────────────────────┐    │
│  │  [SVG hero illustration — sketchy, monochrome, ~280px wide]│    │
│  │  Placed left-aligned or centered, above the intro text     │    │
│  └───────────────────────────────────────────────────────────┘    │
│                                                                    │
│  Hi, I'm Adam. I write about engineering leadership, open source,  │
│  and whatever I can't stop thinking about.                         │
│                                                                    │
│  ────────────────────────────────────────────────────────────     │
│  Selected writing                                                  │
│                                                                    │
│  May 2026                                                          │
│  On building AI literacy tools for kids                            │
│  Engineering · AI · 8 min read                                     │
│                                                                    │
│  April 2022                                                        │
│  DrupalCon 2022 Recap                                              │
│  Drupal · Community · 6 min read                                   │
│                                                                    │
│  September 2021                                                    │
│  Weekend Thoughts: A legacy                                        │
│  Reflection · 4 min read                                           │
│                                                                    │
│                                        → View all writing          │
│                                                                    │
│  ────────────────────────────────────────────────────────────     │
│  [footer: © nerdstein.net · RSS · GitHub · LinkedIn · Twitter]    │
└────────────────────────────────────────────────────────────────────┘
```

- Post list: title + tags + read time on a second line. No excerpts, no cards, no thumbnails. Title links to post.
- "Selected writing" shows 6–8 curated/recent posts, then "View all writing →" to the archive
- Hero illustration: unique SVG, placed once, not repeated on inner pages
- Intro blurb: 2–3 sentences, first-person, rewritten as part of Phase 2

---

#### Single Post Layout

Taken from: HelpScout (metadata line), taniarascia (code blocks, 760px content), fromjason (dropcap, blockquote style), Linear (animated underlines, section signposts).

```
┌───────────────────────────── 720px ────────────────────────────────┐
│  [nav]                                                             │
│                                                                    │
│  ← Back to writing                                                 │
│                                                                    │
│  # Post Title in Instrument Serif, large                           │
│                                                                    │
│  Adam Bergstein · April 12, 2022 · 6 min read · #drupal           │
│                                                                    │
│  [optional: small category SVG doodle, right-floated, ~80px]      │
│                                                                    │
│  ┌── dropcap ────────────────────────────────────────────────┐    │
│  │  T  he first paragraph opens with a dropcap. The opening  │    │
│  │     sentence is a hook — a question, a quote, a claim.    │    │
│  └───────────────────────────────────────────────────────────┘    │
│                                                                    │
│  Body text in system-ui, 18px, line-height 1.7                     │
│                                                                    │
│  ## Section Heading (H2 in Instrument Serif)                       │
│                                                                    │
│  > "A quote that frames the section argument."                     │
│  > — Author, *Book Title*                                          │
│                                                                    │
│  ┌─────────────────────────────────────────────────────────┐      │
│  │  ⚡ Callout block — key insight or warning              │      │
│  │  Styled with left border in accent orange, light bg     │      │
│  └─────────────────────────────────────────────────────────┘      │
│                                                                    │
│  ```bash                                                           │
│  ┌── filename.sh ────────────────────────── [copy] ──────┐        │
│  │  hugo server -D                                        │        │
│  └────────────────────────────────────────────────────────┘        │
│                                                                    │
│  ────────────────────────────────────────────────────────────     │
│  [← Previous post title]         [Next post title →]              │
└────────────────────────────────────────────────────────────────────┘
```

---

#### Typography System

Taken from: Inter Variable (Linear), Instrument Serif (editorial warmth), system-ui body (ma.tt, stefanzweifel), JetBrains Mono (taniarascia code blocks).

```css
/* Design Tokens */
--font-heading:    'Instrument Serif', Georgia, serif;
--font-body:       -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
--font-mono:       'JetBrains Mono', 'Fira Code', monospace;

/* Typographic Scale */
--text-xs:         0.75rem;   /* 12px — timestamps, metadata secondary */
--text-sm:         0.875rem;  /* 14px — tags, nav links, captions */
--text-base:       1.125rem;  /* 18px — body (larger than typical 16px) */
--text-lg:         1.25rem;   /* 20px — post list titles */
--text-xl:         1.5rem;    /* 24px — H3 */
--text-2xl:        2rem;      /* 32px — H2 */
--text-3xl:        2.75rem;   /* 44px — H1 / post title */
--text-hero:       3.5rem;    /* 56px — homepage hero heading (if used) */

/* Line Heights */
--leading-tight:   1.2;   /* headings */
--leading-body:    1.7;   /* body text — generous, from HelpScout research */
--leading-code:    1.5;   /* code blocks */

/* Font Weights */
--weight-normal:   400;
--weight-medium:   500;
--weight-semibold: 600;
--weight-bold:     700;
```

**Loading strategy**: `Instrument Serif` loaded via Google Fonts (display=swap, headings only — minimal FOUT). `JetBrains Mono` loaded only on pages with code. Body uses no web font at all.

---

#### Color System

Taken from: taniarascia's warm beige (#fdf9ee), Descript's dark text (#1a1a1a), Linear's animated underline accent, HelpScout's CSS custom property token approach.

```css
/* Light Mode (default) */
--color-bg:          #fdf9f0;  /* warm parchment — from taniarascia, warmer than pure white */
--color-bg-subtle:   #f5f0e8;  /* slightly deeper warm — for code block backgrounds, callouts */
--color-text:        #1a1a1a;  /* near-black — from Descript */
--color-text-muted:  #6b6563;  /* warm gray — metadata, captions */
--color-border:      #e5e0d8;  /* warm light gray — nav rule, dividers */
--color-accent:      #c85a00;  /* deep orange — links, hover, dropcap */
--color-accent-subtle: #fce8d8; /* light orange tint — callout backgrounds */
--color-code-bg:     #1e1e1e;  /* dark — code blocks use dark bg in light mode (taniarascia model) */
--color-code-text:   #d4d4d4;

/* Dark Mode (prefers-color-scheme: dark) */
--color-bg:          #131210;  /* very dark warm black */
--color-bg-subtle:   #1e1c18;
--color-text:        #e8e4dc;  /* warm off-white */
--color-text-muted:  #9a958c;
--color-border:      #2e2b26;
--color-accent:      #f07830;  /* brighter orange in dark mode */
--color-accent-subtle: #2a1800;
--color-code-bg:     #0d0c0a;
--color-code-text:   #d4d4d4;
```

**Rationale for warm parchment (`#fdf9f0`)**: Pure white backgrounds feel sterile and harsh at scale. taniarascia uses `#fdf9ee`, which creates warmth without being "vintage." This pairs naturally with the illustration system and the serif heading font.

---

#### Illustration & Creative Detail System

Taken from: taniarascia (category illustrations), fromjason (ornamental SVG dividers, dropcaps), Linear (animated underlines), Descript (hover title effects).

**1. Homepage hero SVG**
- One custom hand-drawn/sketchy SVG — stylized laptop, coffee, Drupal drop, or abstract nerd motif
- Monochrome or two-tone (dark + accent orange)
- Width ~280px, placed above the intro text block
- Stays fixed on homepage; not used on inner pages

**2. Category doodles (per post)**
- A small set of 6–8 SVG icons, one per tag category:
  - `#drupal` → stylized Drupal drop
  - `#community` → speech bubbles
  - `#leadership` → compass or arrows
  - `#running` → running shoe
  - `#agile` → sprint loop
  - `#reflection` / `#personal` → journal/pen
  - `#sports` → ball or jersey
  - `#ai` → circuit/spark
- Right-floated on single post pages, ~64–80px, `opacity: 0.85`
- Reused across all posts in the same category

**3. Section dividers**
- Between major sections on homepage and about page: a short hand-drawn SVG line (~120px wide) centered, in `--color-border` — replaces a plain `<hr>`
- Inside posts: standard `<hr>` styled as a 1px warm gray rule with generous margin (3rem top/bottom)

**4. Animated underlines (Linear-style)**
- All post title links: underline drawn via `background-image: linear-gradient(...)` on hover
- Animation: `background-size` transitions from `0% 1.5px` to `100% 1.5px` in `0.2s ease`
- Color: `--color-accent`
- Applied to: post list titles, nav links, in-content links

**5. Dropcap on posts**
- First paragraph of every blog post gets a dropcap
- Styled via CSS `::first-letter` pseudo-element
- Font: `Instrument Serif`, `font-size: 4rem`, `float: left`, `line-height: 0.85`, `margin: 0.1em 0.15em 0 0`
- Color: `--color-accent`

**6. Blockquote style**
- Left border: `4px solid --color-accent`
- Background: `--color-accent-subtle`
- Padding: `1rem 1.25rem`
- Italic body text, citation line in `--color-text-muted`

**7. Callout block**
- Used for key insights, warnings, tips
- Triggered in markdown via Hugo shortcode: `{{< callout >}} content {{< /callout >}}`
- Left border accent, subtle background, optional icon (⚡ info, ⚠ warning)

---

#### Code Block System

Taken from: taniarascia (macOS chrome, copy button, filename display, dark background).

- Dark background (`#1e1e1e`) in both light and dark mode — code blocks always dark
- Optional filename shown as a tab above the block: `┌── config.toml ──────────── [copy] ┐`
- Syntax highlighting via Hugo's built-in Chroma engine (theme: `dracula` or `monokai`)
- Copy button top-right: small icon button, JS-only progressive enhancement
- `border-radius: 8px`, `overflow: auto`, horizontal scroll on overflow

---

#### Archive Page

Taken from: stefanzweifel.dev (date-first dense listing), sj.land (color-coded tags), ma.tt (reverse chronological simplicity).

```
┌──────────────────────────────────────────────────────────────────┐
│  All writing  (114 posts)                                        │
│                                                                  │
│  Filter: [All]  [drupal]  [community]  [leadership]  [personal] │
│                                                                  │
│  2022                                                            │
│  Apr 12  DrupalCon 2022 Recap                     #drupal       │
│                                                                  │
│  2021                                                            │
│  Sep 11  Weekend Thoughts: A legacy            #reflection       │
│  Sep 04  Weekend Thoughts: Leading through change #leadership    │
│  Aug 28  Weekend Thoughts: Chaos is opportunity   #leadership    │
│  Aug 14  Weekend Thoughts: Focused Priorities     #leadership    │
│  Aug 01  Weekend Thoughts: Growth Mindset         #leadership    │
│  Jul 15  Weekend Thoughts: Get into details       #leadership    │
│                                                                  │
│  2020                                                            │
│  ...                                                             │
└──────────────────────────────────────────────────────────────────┘
```

- Year headers as section separators (`font-weight: 600`, `color: --color-text-muted`, `margin-top: 2rem`)
- Each post: `date · title (linked) · tag` on one line — no excerpt
- Filter tabs: static Hugo taxonomy pages (no JS required); "All" is default
- Dense, scannable — this is a complete index, not a highlights reel

---

#### About Page

Taken from: stefanzweifel.dev ("About" framing), HelpScout (warm author presence), fromjason (personal voice without stuffiness).

- No sidebar, no photo (unless Adam wants one)
- Short bio rewritten in Phase 2 — first person, specific, not a LinkedIn summary
- Optional sections: "What I'm working on", "How I got here", "Outside of work"
- Social/contact links at the bottom, not in a sidebar widget
- Consistent with post page layout — same max-width, same font stack

---

#### Design Principles (Constraints)

- **No sidebar** at any breakpoint — retired permanently
- **No cards** on the homepage or archive — titles-only list
- **No thumbnail images** in post listings — content speaks for itself
- **No colored tag boxes** — tags appear as small `#hashtag` text in muted gray
- **Dark mode** supported via `prefers-color-scheme` — no toggle required
- **Zero layout JavaScript** — all layout is CSS; JS only for copy button and optional dark mode toggle
- **Font budget**: 2 web fonts max (Instrument Serif for headings, JetBrains Mono for code); system-ui for body
- **No third-party CSS frameworks** — custom CSS with design tokens only
- **SVG illustrations**: inline or `<img>`, never background-image; all monochrome or two-tone

---

#### Design Deliverables (Phase 0)

1. CSS design token file (`tokens.css`) with all custom properties
2. Hugo theme scaffold: `baseof.html`, `index.html`, `single.html`, `list.html`, `about.html`
3. Navigation partial with logo + links + social icons
4. Homepage post list component
5. Single post page with dropcap, blockquote, callout shortcode, code blocks
6. Archive page with year grouping and tag filter tabs (Hugo taxonomy pages)
7. Hero SVG illustration (homepage)
8. Category doodle SVG set (6–8 icons)
9. Section divider SVG
10. Mobile breakpoint behavior validated at 375px, 640px, 1024px
11. Dark mode validated

**Out of scope for Phase 0**: Final copy for About/Home — written during Phase 2.

---

### Phase 1: Hugo Framework + GitHub + Cloudflare Pages

**Hugo configuration:**

```
nerdstein.net/              ← git repository root
├── config.toml             ← site config, menus, permalinks
├── content/
│   ├── _index.md           ← homepage content
│   ├── about.md            ← about page
│   └── blog/
│       └── *.md            ← one file per blog post
├── static/
│   ├── images/             ← migrated post images
│   └── logo.png            ← existing logo
├── themes/
│   └── nerdstein/          ← custom Hugo theme
│       ├── layouts/
│       │   ├── _default/
│       │   │   ├── baseof.html
│       │   │   ├── list.html
│       │   │   └── single.html
│       │   ├── index.html
│       │   └── partials/
│       │       ├── nav.html
│       │       ├── head.html
│       │       ├── social.html
│       │       └── footer.html
│       ├── shortcodes/
│       │   └── callout.html
│       └── assets/
│           └── css/
│               └── main.css
└── .github/
    └── (optional: workflows for linting/validation)
```

**Hugo `config.toml` key settings:**
```toml
baseURL = "https://nerdstein.net"
title = "Nerdstein"
theme = "nerdstein"
languageCode = "en-us"

[permalinks]
  blog = "/blog/:slug"

[params]
  logo = "/logo.png"
  description = "Home of Nerdstein"
  twitter = "https://www.twitter.com/n3rdstein"
  facebook = "https://www.facebook.com/adam.bergstein"
  linkedin = "https://www.linkedin.com/in/nerdstein"
  featuredPosts = ["drupalcon-2022-recap", "simplytest-from-ground-up", ...]
```

**Blog post frontmatter standard:**
```yaml
---
title: "DrupalCon 2022 Recap"
date: 2022-04-12
slug: "drupalcon-2022-recap"
tags: ["drupal", "community"]
description: "A recap of DrupalCon Portland 2022 and key takeaways."
draft: false
---
```

**Cloudflare Pages setup:**
- Connect GitHub repo to Cloudflare Pages
- Build command: `hugo`
- Build output directory: `public`
- Hugo version pinned via `HUGO_VERSION` environment variable in Cloudflare Pages settings
- Every push to `main` triggers a production deploy
- Every pull request branch gets an automatic preview URL (replaces Tugboat)

**URL preservation:**
- Hugo permalink config maps `/blog/:slug` — all existing `/blog/*` URLs preserved automatically
- Standalone pages (`/litmus-test-ai-application`, `/simplytestme-partners-program`) created as Hugo pages with matching slugs
- A `static/_redirects` file handles any remaining redirect needs (Cloudflare Pages supports Netlify-style `_redirects`)

---

### Phase 2: Content Migration

**Migration approach:**

1. **Scrape nerdstein.net** using `wget` or a custom Python script:
   - Download all HTML pages (blog posts, standalone pages, Home, About)
   - Download all images from `/sites/default/files/`
   - Preserve original publish dates from Drupal's HTML metadata or `<time>` elements

2. **Convert HTML → Markdown** using `pandoc` or a Python script with `html2text` / `markdownify`:
   - Strip Drupal-specific HTML classes and wrappers
   - Preserve heading hierarchy, links, code blocks, blockquotes
   - Replace absolute image URLs with relative paths pointing to `static/images/`

3. **Generate frontmatter** for each post:
   - Extract title from `<h1>` or `<title>` tag
   - Extract date from Drupal's `<time datetime="...">` element or URL slug
   - Extract tags from taxonomy term links
   - Generate slug from existing URL path

4. **Cleanup pass** (Claude Code-assisted):
   - Remove residual HTML artifacts
   - Normalize heading levels
   - Fix broken links (internal links updated to new URL structure)
   - Flag posts with unusual formatting for manual review

5. **About and Home pages**:
   - Home: new short intro blurb + links to recent posts (replaces Drupal view block)
   - About: Adam rewrites his bio with Claude Code assistance; existing content used as source material

6. **Images**:
   - All images saved to `static/images/` with original filenames
   - Alt text added where missing

**Full content audit** (114 pieces of content discovered via Drupal node traversal — far more than the 15 originally estimated from the blog listing page):

**URL structure note**: Drupal used inconsistent URL prefixes over the years — `/blog/`, `/content/`, `/presentation/`, and bare top-level paths. Hugo will normalize all of these under `/blog/` with `_redirects` handling the old paths.

**Static pages (migrated but rewritten):**

| Current URL | Title |
|-------------|-------|
| `/` | Homepage |
| `/about` | About |

**Standalone pages (preserve URL, refresh content):**

| Current URL | Title |
|-------------|-------|
| `/litmus-test-ai-application` | A litmus test of an AI application |
| `/simplytestme-partners-program` | SimplyTest.me Partners Program |
| `/drupal-identity-road-ahead` | Drupal, Identity, and the Road Ahead |

**Blog posts — Recent (2020–2022):**

| Current URL | Title |
|-------------|-------|
| `/blog/drupalcon-2022-recap` | DrupalCon 2022 Recap |
| `/presentation/evaluating-landscape-drupal-competition` | Evaluating the Landscape of Drupal Competition |
| `/blog/simplytest-from-ground-up` | SimplyTest.me From The Ground Up |
| `/blog/weekend-thoughts-6` | Weekend Thoughts, 9/11/21: A legacy |
| `/blog/weekend-thoughts-5` | Weekend Thoughts, 9/4/21: Leading through change |
| `/blog/weekend-thoughts-4` | Weekend Thoughts, 8/28/21: Where there is chaos, there is opportunity |
| `/blog/weekend-thoughts-3` | Weekend Thoughts, 8/14/21: Focused Priorities |
| `/blog/weekend-thoughts-2` | Weekend Thoughts, 8/1/21: Growth Mindset |
| `/blog/weekend-thoughts-1` | Weekend Thoughts, 7/15/21: Get into details |
| `/blog/welcome-matt-glaman` | SimplyTest.me Welcomes Matt Glaman |
| `/blog/drupal-ci-cd` | Drupal CI/CD with TugboatQA and Github Actions |
| `/blog/new-site-2020` | Finally! A website refresh |
| `/blog/getting-started-drupal-rector-development` | Getting Started with Drupal Rector Development |
| `/blog/drupal-community-care-packages` | Drupal Community Care Packages |
| `/blog/simplytestme-opencollective-update` | SimplyTest.me OpenCollective Update |
| `/blog/drupal-9-deprecations-simplytestme` | Drupal 9 Deprecations with SimplyTest.me |
| `/blog/new-beginnings` | New Beginnings |
| `/blog/simplytestme-release-welcomes-tugboatqa-centarro-and-linode` | SimplyTest.me release welcomes TugboatQA, Centarro, and Linode |
| `/blog/devops-primer` | A DevOps Primer |
| `/blog/simplytestme-and-google-summer-code-2019` | SimplyTest.me and Google Summer of Code 2019 |
| `/blog/my-2019-aaron-winborn-award-nomination` | My 2019 Aaron Winborn Award Nomination |
| `/blog/season-simplytest` | The Season of SimplyTest |

**Blog posts — 2017–2019:**

| Current URL | Title |
|-------------|-------|
| `/blog/custom-rest-resources-drupal-8` | Custom REST Resources in Drupal 8 |
| `/blog/running-pro-tips` | Running Pro-Tips |
| `/blog/static-and-dynamic-capabilities-design-systems` | Static and Dynamic Capabilities of Design Systems |
| `/blog/mid-2018-drupal-coffee-exchange-updates` | Mid-2018 Drupal Coffee Exchange Updates |
| `/blog/achieving-clarity-component-based-best-practices` | Achieving Clarity in Component-based Best Practices |
| `/blog/leveon-bell-and-saquon-barkley` | LeVeon Bell and Saquon Barkley |
| `/blog/simplytestme-roadmap-early-2018` | SimplyTest.me Roadmap (Early 2018) |
| `/blog/2017-conference-review` | 2017 Conference Review |
| `/blog/future-simplytestme` | The Future of SimplyTest.me |
| `/blog/impacts-drupal-and-ambitious-digital-experiences` | Impacts of Drupal and Ambitious Digital Experiences |
| `/blog/retrospecting-legal-and-technical-ramifications-reactjs` | Retrospecting on the Legal and Technical Ramifications of ReactJS |
| `/blog/exploring-simplicity-drupal-design-components` | Exploring simplicity in Drupal design components |
| `/blog/analysis-drupal-governance` | An Analysis of Drupal Governance |
| `/blog/local-core-development-environments` | Local core development environments |
| `/blog/promoting-community-toxicity` | Promoting Community Toxicity |
| `/blog/drupal-contribution-non-profit` | A Drupal Contribution Non-Profit |
| `/blog/community-governance-considerations-open-source-projects` | Community Governance Considerations of Open Source Projects |
| `/blog/what-gets-me-morning` | What Gets Me Up In The Morning |
| `/blog/removing-site-building-drupals-vocabulary` | Removing Site Building From Drupal's Vocabulary |

**Blog posts — 2016–2017 (Community/Conduct):**

| Current URL | Title |
|-------------|-------|
| `/blog/communal-action-self-and-others` | Communal Action in Self and Others |
| `/blog/civility-community` | Civility is Community |
| `/blog/evolving-clarity-conduct-technical-communities` | Evolving Clarity of Conduct in Technical Communities |
| `/blog/follow-more-informed-opinion-our-community-crisis` | Follow Up: A more informed opinion on our community crisis |
| `/blog/troubling-situation-indeed` | A Troubling Situation Indeed |
| `/blog/first-based-approaches-need-die` | "First" based approaches need to die |
| `/blog/not-victim` | Not A Victim |
| `/blog/commits-drupalorg` | Commits on Drupal.org |
| `/varnish-drupal-8` | Just Another Varnish and Drupal 8 Blog Post |
| `/blog/lessons-learned-why-and-how-drupal-contributions` | Lessons Learned: The "Why" and "How" of Drupal Contributions |
| `/blog/balancing-theory-and-practice` | Balancing Theory and Practice |
| `/blog/setting-your-system-drupal-coding-standards` | Setting up your system for Drupal coding standards |
| `/blog/technical-lift-drupal-8` | The Technical Lift of Drupal 8 |
| `/content/peeling-back-onion-drupal-security-and-compliance` | Peeling Back the Onion: Drupal Security and Compliance |
| `/content/accessible-continuous-integration-primer` | Accessible Continuous Integration - A Primer |
| `/blog/theming-drupal-8-field-collections` | Theming Drupal 8 Field Collections |
| `/content/lessons-learned-drupal-8-module-porting` | Lessons Learned: Drupal 8 Module Porting |
| `/content/accessible-continuous-integration-security-and-compliance-edition` | Accessible Continuous Integration - Security and Compliance Edition |
| `/content/hacking-agile-contracts` | Hacking Agile Contracts |
| `/blog/office-dead` | The office is dead |
| `/content/accessible-continuous-integration-2016-stanford-drupal-camp` | Accessible Continuous Integration - 2016 Stanford Drupal Camp |
| `/blog/slideshow-drupal-8` | A slideshow in Drupal 8 |
| `/blog/our-fights-are-not-your-fights` | Our fights are not your fights |
| `/blog/site-updates-drupal` | Site Updates in Drupal |
| `/blog/common-drupalvm-use` | Common DrupalVM Use |
| `/content/data-generation-drupal` | Data Generation in Drupal |
| `/content/web-services-primer-drupal-8` | Web Services Primer in Drupal 8 |
| `/blog/2016-pittsburgh-pirates-predictions` | 2016 Pittsburgh Pirates Predictions |
| `/blog/just-enough-planning-agile-concept` | "Just Enough" Planning - An Agile Concept |
| `/blog/patterns-devops-practices` | Patterns of DevOps Practices |
| `/content/evolving-tools-agile-world` | Evolving tools in an Agile world |
| `/blog/reliability` | Reliability |
| `/blog/engineering-tenets-agile` | Engineering Tenets of Agile |
| `/blog/simpletests-hanging-drupal-8` | Simpletests hanging in Drupal 8? |

**Blog posts — 2014–2015:**

| Current URL | Title |
|-------------|-------|
| `/blog/simple-beauty-life` | Simple beauty of life |
| `/blog/my-temperature-happy` | My temperature is happy |
| `/blog/2015-steelers-draft-predictions` | 2015 Steelers Draft Predictions |
| `/blog/being-present` | Being present |
| `/blog/institutional-knowledge` | Institutional knowledge |
| `/blog/imitation-best-form-flattery` | Imitation is the best form of flattery |
| `/blog/why-keurig-sucks` | Why Keurig Sucks |
| `/blog/plea-patience` | A plea for patience |
| `/blog/acquia-certification-exams` | Acquia certification exams |
| `/blog/routine-stifles-innovation` | Routine stifles innovation |
| `/blog/desirable-short-term-memory` | Desirable Short Term Memory |
| `/blog/social-vampirism-services` | Social Vampirism in Services |
| `/blog/local-drupal-development-sandboxes` | Local Drupal development sandboxes |
| `/blog/serenity-thought` | Serenity of thought |

**Older posts — no /blog/ prefix (pre-2014, top-level or non-standard paths):**

| Current URL | Title |
|-------------|-------|
| `/open-source-free-puppies` | Open source tools are free |
| `/nodes-with-no-pages` | Nodes with no page views |
| `/balance-trust-and-quality` | A balance of trust and quality |
| `/its-not-you-its-me` | It's not you, it's me |
| `/agile-spree` | An Agile Spree |
| `/risks-unwaivering-swagger` | Risks and Unwavering Swagger |
| `/the-noob` | The role of the noob |
| `/migration-tips-tricks` | Migration Tips and Tricks |
| `/dont-solve-same-problem-twice` | Don't solve the same problem twice |
| `node/7` | Learning is giving, not just receiving |
| `node/9` | A call for simplicity |
| `node/10` | Some perspective on difficult customers |
| `node/11` | Keeping up with the Joneses |
| `node/12` | Design issues of a distributed Drupal system |
| `node/13` | Research contributions when problems are already solved |
| `node/14` | A brief comparison of text editors |
| `node/15` | Tools I can't live without |
| `node/16` | Varnish and Drupal |
| `node/17` | Should the Pens trade Orpik? |
| `node/18` | Automated Drupal Code Improvements |
| `node/19` | Life in transition |
| `node/20` | Mediated web file content management |
| `node/21` | Bagel-ology |
| `node/22` | Towards organizational efficacy |

*Notes on oldest content (node/1–5): "World Campus", "Salary and Reappointments", "Penn State Learning", "Welcome" — likely early test/admin nodes from the site's original setup. Recommend reviewing whether these should be migrated or archived-only.*

---

### Phase 3: Claude Code Authoring Workflow

**Creating a new blog post with Claude Code:**

```bash
# Example prompt to Claude Code:
"Write a blog post about my experience at DrupalCon 2024. 
Title: 'DrupalCon 2024: Community at the Core'
Tags: drupal, community
Include an intro, 3 main sections, and a closing thought."
```

Claude Code will:
1. Create `content/blog/drupalcon-2024-community-at-the-core.md`
2. Populate frontmatter: `title`, `date` (today), `slug`, `tags`, `description`, `draft: false`
3. Write the full post body in markdown

Author then:
```bash
git add content/blog/drupalcon-2024-community-at-the-core.md
git commit -m "Add DrupalCon 2024 post"
git push origin main
# → Cloudflare Pages auto-deploys within ~60 seconds
```

**Creating a post manually** (no Claude Code):
1. Copy an existing markdown file as a template
2. Update frontmatter fields
3. Write content below the `---` delimiter
4. `git push` to publish

**Draft posts:**
- Set `draft: true` in frontmatter to prevent publishing
- Hugo excludes drafts from production builds by default
- Preview locally with `hugo server -D` (includes drafts)

**Local development setup:**

```bash
# Prerequisites
brew install hugo

# Clone repo and serve locally
git clone https://github.com/nerdstein/nerdstein.net
cd nerdstein.net
hugo server -D
# → Visit http://localhost:1313
```

**CLAUDE.md** (to be added at repo root for Claude Code context):
- Documents site structure, frontmatter format, slug conventions, image placement
- Documents the authoring style guide (see below) so Claude Code generates posts that match Adam's voice
- Claude Code reads this automatically, enabling consistent post generation without per-prompt instructions

---

### Authoring Style Guide

This style guide defines how posts on nerdstein.net are written. It is embedded in `CLAUDE.md` so that Claude Code applies it automatically when generating any new post.

**Voice and Tone:**
- Technically grounded, intellectually curious, and direct — never casual to the point of losing rigor
- Inquisitive framing: posts often start from a question, challenge an assumption, or examine something from an unexpected angle
- Personal but not meandering — the author's perspective is present without becoming self-indulgent
- Confident, not preachy; makes a point of view clear without lecturing
- Appropriate levity — not every post needs to be serious, but humor is dry and earned, not forced

**Structure:**
- **Opening**: Hook with a question, a provocation, a surprising data point, or a famous quote that frames the piece. Do not start with "In this post, I will..." Never open with a definition.
- **Body**: Three to five substantive sections. Each section has a clear point, not just a topic. Headings are specific and tell you something ("Why agile fails in isolation" not "Challenges").
- **Supporting material**: Back up assertions with at least one of:
  - A book reference (author + title, brief paraphrase of the relevant idea)
  - A data point or research finding (cited source, not vague)
  - A famous quote (relevant, not decorative)
  - A concrete example from personal or industry experience
- **Closing**: Land the point. Summarize the key insight in 1–2 sentences. Optionally end with an open question to invite reader reflection.

**Quote Usage:**
- Use quotes to open a section or the whole piece when the quote genuinely frames the argument — not as decoration
- Always attribute properly: "Author Name, *Book or Work Title*" or "Speaker Name"
- Prefer quotes from engineers, leaders, researchers, or writers who've actually lived the thing being discussed
- Example sources to draw from: Donald Knuth, Linus Torvalds, Fred Brooks (*The Mythical Man-Month*), Clayton Christensen (*The Innovator's Dilemma*), James Clear (*Atomic Habits*), Cal Newport, Adam Grant, bell hooks, Drupal community figures

**Research and Data:**
- When making a factual claim, link or cite a source — don't write "studies show" without naming one
- Books are first-class citations: "In *Team of Teams*, Stanley McChrystal argues that..."
- Data points from industry reports (Stack Overflow Developer Survey, GitHub Octoverse, Gartner) are acceptable; be specific about the year
- Don't pad with excessive citations — one strong reference per major claim is enough

**Formatting:**
- Use **bold** sparingly — only for a term being defined or a genuinely critical phrase
- Use `code blocks` for all code, commands, and file paths — even inline
- Use blockquotes `>` for pull quotes or notable callouts within the post body
- Lists are fine for enumerations, but don't turn everything into bullets — prose is preferred for connected ideas
- Post length: 400–1200 words is the target. Short is fine if complete. Long is fine if earned.

**Frontmatter fields generated for every post:**
```yaml
---
title: "Exact post title"
date: YYYY-MM-DD
slug: "url-friendly-slug"
tags: ["tag1", "tag2"]
description: "One sentence that appears in post listings and SEO meta."
draft: false
---
```

**Example post opening styles:**
```markdown
# Option 1: Quote opening
> "The best programs are written so that computing machines can perform them quickly
>  and so that human beings can understand them clearly."
> — Donald Knuth

There's a reason Knuth put human clarity first. Most of the code I've inherited
in my career was written for the machine, not the reader...

# Option 2: Question opening
What does it actually mean to remove "site building" from Drupal's vocabulary?
It sounds like marketing. It might be strategy. It's probably both...

# Option 3: Data/provocation opening
In 2022, the Drupal project had 1.3 million sites. That number sounds like
health. It isn't. The question is whether the community knows it...
```

---

### Phase 4: Infrastructure Shutdown

**Pre-shutdown checklist:**
- [ ] nerdstein.net DNS pointing to Cloudflare Pages and stable for 48+ hours
- [ ] All pages returning 200 (spot-checked against content inventory table above)
- [ ] Full Drupal database export archived locally (`mysqldump nerdstein > nerdstein-backup-YYYY-MM-DD.sql`)
- [ ] All files from `/sites/default/files/` downloaded to local backup
- [ ] Drupal codebase archived (optional: `git archive` or tarball)

**Shutdown steps:**
1. **Tugboat**: Delete all environments from Tugboat dashboard → cancel subscription
2. **Linode VPS**: Power off the Linode instance → delete the instance from Linode Cloud Manager → verify no further invoices
3. **DNS**: Confirm all DNS records point to Cloudflare Pages (no A records pointing to old Linode IP)
4. **Email** (if hosted on Linode): Verify no email services are running on the VPS before termination (if MX records point elsewhere, this is a no-op)

---

## Technical Constraints

### Performance
- Hugo builds are sub-second for sites of this size — no constraint
- Cloudflare Pages CDN serves static assets globally; target page load < 1s on fast connections
- No JavaScript frameworks or client-side rendering — HTML/CSS only (except optional minimal JS for mobile nav)

### Security
- No backend, no database, no attack surface beyond static files
- HTTPS enforced via Cloudflare (automatic SSL certificate)
- No user authentication or form handling required
- Any future contact form would use a third-party service (e.g., Cloudflare Turnstile + email forwarding)

### Integration
- **GitHub**: Repository hosting; Cloudflare Pages builds triggered on push to `main`
- **Cloudflare Pages**: Build and serve static site; handles CDN, HTTPS, preview deployments per branch
- **Hugo**: Static site generator; version pinned to avoid breaking changes
- **Claude Code**: Authoring assistant; uses repo `CLAUDE.md` for site-specific context

### Technology Stack
- Static site generator: Hugo (latest stable, pinned in Cloudflare Pages env var)
- Theme: Custom Hugo theme (`themes/nerdstein/`) — no third-party theme dependency
- CSS: Plain CSS with custom properties (no preprocessor, no Tailwind — keep it simple)
- JavaScript: Minimal (mobile nav toggle only, vanilla JS)
- Hosting: Cloudflare Pages (free tier)
- Repository: GitHub (public or private — author's choice)
- DNS: Managed in Cloudflare (same account as Pages for simplicity)

---

## MVP Scope & Phasing

### Phase 0: Design (Before Code)
- Hugo theme scaffold with sidebar layout
- Color system using existing palette
- Typography refresh
- Mobile breakpoint
- Iterate with Adam before proceeding

### Phase 1: Framework Setup (Foundation)
- GitHub repository initialized
- Hugo installed and configured
- `config.toml` with permalinks, params, menus
- Cloudflare Pages connected to GitHub, auto-deploying
- Custom domain `nerdstein.net` configured in Cloudflare Pages
- HTTPS active

### Phase 2: Content Migration (Data)
- Full site crawl and HTML download
- HTML → Markdown conversion for all 16 pages
- Images downloaded and placed in `static/images/`
- Frontmatter generated for all posts
- Cleanup pass for formatting artifacts
- About and Home pages rewritten
- All URLs verified

### Phase 3: Authoring Workflow (Tooling)
- `CLAUDE.md` written at repo root
- Authoring instructions documented in `README.md`
- Local development setup documented
- End-to-end test: create a new post via Claude Code, push, verify live

### Phase 4: Decommission (Cleanup)
- Drupal backup archived
- Linode VPS terminated
- Tugboat deleted
- DNS verified pointing to Cloudflare Pages only

**MVP Definition**: Phases 1–4 complete, with Phase 0 design approved before Phase 1 build begins.

### Future Considerations
- RSS feed (Hugo generates this natively — just needs to be enabled)
- Search (lunr.js static search, or Cloudflare's built-in search)
- Dark mode toggle
- Comment system (e.g., Giscus backed by GitHub Discussions)
- Analytics (Cloudflare Web Analytics — free, privacy-respecting)

---

## Risk Assessment

| Risk | Probability | Impact | Mitigation Strategy |
|------|------------|--------|---------------------|
| Content loss during HTML→Markdown conversion | Medium | High | Archive full Drupal DB + files before starting; validate every migrated page against live site |
| DNS propagation delay causes downtime | Low | Medium | Pre-configure Cloudflare Pages custom domain; reduce Linode DNS TTL to 300s 24h before cutover |
| Drupal posts with complex HTML (tables, embeds) don't convert cleanly | High | Low | Cleanup pass after conversion; Claude Code can reformat problematic posts |
| Hugo version breaking change after migration | Low | Low | Pin `HUGO_VERSION` env var in Cloudflare Pages; don't auto-update |
| Old Linode IP still in DNS after shutdown | Low | High | Audit all DNS records before terminating Linode; Cloudflare DNS manager makes this easy |
| Scale of content migration underestimated | **Realized** | Medium | Full audit complete — 114+ posts across 10+ years; migration script required, not manual |
| Inconsistent URL prefixes (`/blog/`, `/content/`, `/presentation/`, bare top-level, `/node/N`) | High | Medium | Map all canonical URLs (audited above); `_redirects` file handles all variants |
| Oldest posts (node/1–22 era) may have no URL alias, only `/node/N` | High | Low | These get new `/blog/` slugs; old `/node/N` URLs redirected |
| Some early posts may not be worth migrating (test/admin content) | Low | Low | Review node/1–5 before migration; archive if not real content |

---

## Dependencies & Blockers

**Dependencies:**
- **Cloudflare account**: Must be created or confirmed active before Phase 1
- **GitHub account**: `nerdstein` GitHub org/account for repository hosting
- **Hugo installation**: Local machine needs Hugo installed for development
- **Domain access**: DNS for `nerdstein.net` must be transferable to Cloudflare DNS management

**Known Blockers:**
- None identified — all tooling is free and available

---

## Appendix

### Glossary
- **Hugo**: An open-source static site generator written in Go. Converts markdown + templates into HTML.
- **Cloudflare Pages**: Cloudflare's free static site hosting platform with global CDN and automatic GitHub deploys.
- **Frontmatter**: YAML metadata block at the top of a markdown file, delimited by `---`, used by Hugo to set post title, date, tags, slug, etc.
- **`_redirects`**: A plain-text file in Cloudflare Pages' `static/` directory that defines URL redirects in Netlify format.
- **Linode**: The cloud VPS provider currently hosting the Drupal site.
- **Tugboat**: A staging/preview environment service currently used alongside Linode.

### Existing nerdstein.net Design References
- Logo: `/themes/nerdstein/logo.png` on the live server (carried over as-is)
- Existing brand colors (for reference — new palette is refined from these):
  - Orange: `#ffa200` → refined to `#e8720c` in new design
  - Teal: `#008e8e` (retired — not used in new design)
  - Dark: `#232323` → `#1a1a1a` in new design
- Sidebar layout: **retired** — replaced by horizontal top nav + single column

### Design Inspiration
**Personal sites:**
- taniarascia.com — editorial + custom illustration model
- fromjason.xyz — personal voice + simple layout
- ma.tt — minimal, writing-first
- sj.land — refined details and polish

**Product/SaaS blogs (design reference only):**
- Linear blog — tightest typography and single-column execution in the industry
- Notion blog — editorial hierarchy, document-like feel
- HelpScout blog — readable density, strong author attribution
- Descript blog — bold headings, editorial illustration
- SavvyCal blog — minimal, white-space-driven

**Reference collection:** [danielwirtz.com/blog/favorite-personal-websites](https://danielwirtz.com/blog/favorite-personal-websites)

### References
- Hugo documentation: https://gohugo.io/documentation/
- Cloudflare Pages Hugo deployment guide: https://developers.cloudflare.com/pages/framework-guides/deploy-a-hugo-site/
- Cloudflare Pages `_redirects` format: https://developers.cloudflare.com/pages/configuration/redirects/
- pandoc (HTML→Markdown): https://pandoc.org/

---

*This PRD was created through interactive requirements gathering with quality scoring to ensure comprehensive coverage of business, functional, UX, and technical dimensions.*