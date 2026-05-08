# nerdstein.net — Static Site

This is the source repository for [nerdstein.net](https://nerdstein.net), migrated from Drupal 9 to a Hugo static site hosted on Cloudflare Pages.

## Docs

- [PRD — Migration & Design](docs/prd.md)

## Stack

- **Static site generator**: [Hugo](https://gohugo.io/)
- **Hosting**: [Cloudflare Pages](https://pages.cloudflare.com/) (free tier)
- **Content**: Markdown files with YAML frontmatter in `content/blog/`
- **Authoring**: Claude Code or direct file editing

## Local Development

```bash
brew install hugo
hugo server -D
# → http://localhost:1313
```

## Publishing a New Post

Describe the post to Claude Code and it will create the markdown file, then:

```bash
git add content/blog/your-new-post.md
git commit -m "Add: post title"
git push origin main
# → Cloudflare Pages auto-deploys in ~60s
```

## Project Status

Migration in progress. See [docs/prd.md](docs/prd.md) for the full plan.