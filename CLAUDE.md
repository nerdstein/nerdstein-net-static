# nerdstein.net — Authoring Guide for Claude Code

This is the Hugo static site for nerdstein.net. This file gives Claude Code the context needed to create new blog posts, maintain existing content, and make site changes consistently.

---

## Site Structure

```
nerdstein-net-static/
├── hugo.toml                  # Site config: baseURL, theme, menus, params
├── content/
│   ├── _index.md              # Homepage (layout handles content; minimal body here)
│   ├── about.md               # About page — first-person bio
│   ├── archive.md             # Archive page (uses custom layout)
│   └── blog/
│       ├── _index.md          # Blog section index (title only)
│       └── *.md               # One file per post
├── static/
│   └── images/                # Post images live here; reference as /images/filename.jpg
├── themes/nerdstein/
│   ├── assets/css/main.css    # All CSS — edit here for design changes
│   ├── layouts/
│   │   ├── _default/          # baseof.html, single.html, list.html
│   │   ├── index.html         # Homepage layout
│   │   └── partials/          # head.html, nav.html, footer.html, post-meta.html
│   └── layouts/shortcodes/
│       └── callout.html       # {{< callout >}} shortcode
└── CLAUDE.md                  # This file
```

---

## Creating a New Blog Post

1. Create a new file at `content/blog/{slug}.md`
2. The filename should match the slug (kebab-case, all lowercase)
3. Add frontmatter (see template below)
4. Write the post body in Markdown below the closing `---`

### File naming convention

- File: `content/blog/my-post-title.md`
- Slug in frontmatter: `"my-post-title"`
- URL: `https://nerdstein.net/blog/my-post-title`

The slug in frontmatter controls the URL. Keep it short, descriptive, and kebab-case. Match the filename to the slug.

---

## Frontmatter Template

Every post requires all of these fields:

```yaml
---
title: "Exact Post Title Here"
date: YYYY-MM-DD
slug: "url-friendly-slug-in-kebab-case"
tags: ["tag1", "tag2"]
description: "One sentence — appears in post listings and as the SEO meta description. Make it count."
draft: false
---
```

### Field notes

- `title`: Exact title as it should appear on the page. Use title case. Can include punctuation.
- `date`: ISO 8601 format `YYYY-MM-DD`. Use today's date for new posts.
- `slug`: Kebab-case. No spaces, no special characters except hyphens. This becomes the URL path.
- `tags`: Array of strings. Use existing tags when applicable: `drupal`, `community`, `leadership`, `reflection`, `personal`, `engineering`, `agile`, `open-source`, `ai`.
- `description`: One sentence, under 160 characters. Write it as a standalone statement, not "In this post, I..."
- `draft`: Always `false` for posts ready to publish. Set to `true` to write without publishing.

---

## Authoring Style Guide

Posts on this site have a consistent voice: technically grounded, intellectually curious, and direct. Follow these principles when writing new content.

### Voice and Tone

- Write in first person. This is a personal site.
- Be direct. Make your point. Don't hedge everything.
- Curious and inquisitive, not preachy or didactic.
- Confident but not arrogant. Have a point of view and state it clearly.
- Appropriate levity when it fits — dry humor, not forced cheerfulness.
- Technical when appropriate, accessible when not.

### Post Structure

**Opening (required hook):** Start with one of:
- A relevant quote that genuinely frames the piece — not decoration
- A pointed question that the post will work toward answering
- A surprising or counterintuitive data point
- A specific, concrete observation from experience

Never open with: "In this post, I will..." or "Today I want to talk about..." or a dictionary definition.

**Body:** Three to five sections. Each section makes a specific point, not just covers a topic. Section headings should be specific and tell you something: "Why agile fails in isolation" rather than "Challenges."

**Closing:** Land the point. Summarize the key insight in 1-2 sentences. Optionally end with an open question that invites reader reflection — not a rhetorical nothing, but a question that actually opens something up.

### Length

- Target: 400–1200 words
- Short is fine if the piece is complete
- Long is fine if the length is earned
- Do not pad for length

### References and Citations

Back up assertions with at least one of:
- A book reference: "In *The Mythical Man-Month*, Fred Brooks argues that..."
- A named data point: "According to the 2023 Stack Overflow Developer Survey..."
- A quote: properly attributed with name and work
- A concrete personal or industry example

Do not write "studies show" or "research suggests" without naming the study.

**Reference sources to draw from:** Fred Brooks (*The Mythical Man-Month*), Clayton Christensen (*The Innovator's Dilemma*), Carol Dweck (*Mindset*), James Clear (*Atomic Habits*), Cal Newport, Adam Grant, bell hooks, Donald Knuth, Stanley McChrystal (*Team of Teams*), Drupal community figures.

### Formatting

- **Bold** sparingly — only for a term being defined or a genuinely critical phrase
- `` `code` `` for all code, commands, and file paths — even inline
- `>` blockquote for pull quotes or notable statements within the post body
- Lists are fine for enumerations, but prefer prose for connected ideas
- Avoid bullet point abuse — if it can be a sentence, make it a sentence

---

## Shortcodes

### Callout block

Use for key insights, important warnings, or tips worth calling out:

```markdown
{{< callout >}}
Your callout content here. Supports **bold**, `code`, and other inline markdown.
{{< /callout >}}
```

Renders with an orange left border and subtle orange background.

---

## Local Development

```bash
# Preview the site (includes drafts)
hugo server -D

# Preview without drafts (mirrors production)
hugo server

# Build for production
hugo
```

Visit `http://localhost:1313` after running `hugo server`.

---

## Publishing a Post

Once a post is written and `draft: false`:

```bash
git add content/blog/your-post-slug.md
git commit -m "Add post: Your Post Title"
git push origin main
```

Cloudflare Pages automatically builds and deploys within ~60 seconds of a push to `main`. The post appears live at `https://nerdstein.net/blog/your-post-slug`.

To preview before publishing, set `draft: true` and run `hugo server -D` locally.

---

## Adding Images

1. Place the image in `static/images/` (e.g., `static/images/drupalcon-2022-photo.jpg`)
2. Reference it in markdown as `/images/drupalcon-2022-photo.jpg`

```markdown
![Alt text describing the image](/images/drupalcon-2022-photo.jpg)
```

Always include descriptive alt text.

---

## Editing the Design

All CSS lives in `themes/nerdstein/assets/css/main.css`. The file is organized with section comments. Design tokens (colors, fonts, spacing) are defined as CSS custom properties at the top of the file and in a `@media (prefers-color-scheme: dark)` block.

Do not use Tailwind, Bootstrap, or any CSS framework — this site uses plain CSS only.

---

## Common Tag Reference

Use existing tags consistently. Create new tags sparingly.

| Tag | Used for |
|-----|----------|
| `drupal` | Drupal CMS, contrib, community |
| `community` | Open source community, governance, conduct |
| `leadership` | Engineering leadership, management, teams |
| `reflection` | Personal reflection, mindset, philosophy |
| `personal` | Life, family, running, non-technical |
| `engineering` | Software engineering craft, architecture |
| `agile` | Agile practices, process, DevOps |
| `open-source` | Open source broadly (not Drupal-specific) |
| `ai` | Artificial intelligence, ML, LLMs |