# /llm-readability — Claude Code Slash Command

A Claude Code custom slash command that analyses any website project for LLM readability and implements all necessary features to make it discoverable by AI systems (Claude, ChatGPT, Perplexity, Google AI Overviews).

## What It Does

When you run `/llm-readability` in Claude Code, it:

1. **Analyses** your website's current LLM discoverability (robots.txt, sitemap, meta tags, content structure)
2. **Scores** it on 7 dimensions and gives an overall GEO (Generative Engine Optimisation) readiness score
3. **Implements** all fixes — creates/updates `llms.txt`, `llms-full.txt`, `robots.txt`, and `sitemap.xml`
4. **Verifies** the build and re-scores to show before/after improvement

### Files Created/Modified

| File | Purpose |
|------|---------|
| `robots.txt` | Explicit Allow rules for 14+ AI crawlers (ClaudeBot, GPTBot, PerplexityBot, etc.) |
| `sitemap.xml` | All pages with current dates |
| `llms.txt` | Curated Markdown index following the [llmstxt.org](https://llmstxt.org) spec — like a sitemap for AI |
| `llms-full.txt` | Complete site content in one Markdown file — AI systems read this instead of trying to render your JavaScript |

## Installation

### Option A: Project-level (recommended for teams)

Copy into your project's `.claude/commands/` directory:

```bash
mkdir -p .claude/commands
curl -o .claude/commands/llm-readability.md https://raw.githubusercontent.com/rete-consulting/claude-code-llm-readability/main/llm-readability.md
```

Then commit it. Anyone on the team can use `/llm-readability` in the project.

### Option B: User-level (available in all projects)

```bash
mkdir -p ~/.claude/commands
curl -o ~/.claude/commands/llm-readability.md https://raw.githubusercontent.com/rete-consulting/claude-code-llm-readability/main/llm-readability.md
```

### Usage

In Claude Code, type:

```
/llm-readability
```

That's it. Claude will analyse your project, implement the fixes, and show you the results.

## Why This Matters

### The Problem

AI systems (Claude, ChatGPT, Perplexity, Google Gemini) increasingly answer user questions by pulling from web content. But most websites are invisible to them:

- **SPAs** render content via JavaScript — AI crawlers see an empty `<div id="root"></div>`
- **robots.txt** often doesn't mention AI crawlers at all
- **No llms.txt** means AI systems have no curated content index to read

### The Solution: llms.txt

The [llms.txt standard](https://llmstxt.org) (proposed by Jeremy Howard, September 2024) provides AI-readable content at a well-known URL. Think of it as `robots.txt` for AI consumption rather than access control.

**Two-file pattern:**
- `/llms.txt` — lightweight index (~2-5KB) for quick lookups
- `/llms-full.txt` — complete content (~10-20KB) for deep ingestion

**Adopted by:** Anthropic, Stripe, Cloudflare, Vercel, Supabase, Shopify, Hugging Face, and 844K+ other websites.

### AI Crawlers Supported

This skill configures `robots.txt` for all major AI crawlers:

| Provider | Crawlers |
|----------|----------|
| Anthropic | ClaudeBot, Claude-User, Claude-SearchBot |
| OpenAI | GPTBot, OAI-SearchBot, ChatGPT-User |
| Perplexity | PerplexityBot, Perplexity-User |
| Google | Google-Extended |
| Apple | Applebot-Extended |
| Other | Amazonbot, CCBot, Bytespider, meta-externalagent |

## How It Scores Your Site

The GEO (Generative Engine Optimisation) readiness score is based on:

| Dimension | What It Measures |
|-----------|-----------------|
| AI Crawler Access | Are AI bots explicitly allowed in robots.txt? |
| Content Discovery | Do llms.txt/llms-full.txt exist and follow the spec? |
| Sitemap Completeness | Are all pages listed with current dates? |
| Meta Tag Quality | Descriptions, JSON-LD, OG tags, canonical URLs |
| Content Structure | Clean headings, self-contained extractable sections |
| Keyword Coverage | Industry terms, geographic terms, positioning |
| FAQ/Citation Readiness | Direct-answer passages AI can quote |

## Works With

Any web project: React, Next.js, Vue, Nuxt, Astro, Svelte, static HTML, Vite, Webpack — the skill auto-detects the framework and static file directory.

## Credits

- [llmstxt.org](https://llmstxt.org) — The llms.txt specification by Jeremy Howard
- Built by [Rete Consulting](https://reteconsulting.dev)

## License

MIT
