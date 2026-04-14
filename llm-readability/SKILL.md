---
name: llm-readability
description: >
  Analyse a website project for LLM readability and implement llms.txt, robots.txt,
  and sitemap.xml features to make the site discoverable by AI systems (Claude, ChatGPT,
  Perplexity, Google AI Overviews). Use when the user asks about making their site
  discoverable by AI, LLM-friendly, or mentions llms.txt.
disable-model-invocation: true
argument-hint: "[url-or-path]"
---

Analyse this website project for LLM readability and implement all necessary features to make it discoverable by AI systems (Claude, ChatGPT, Perplexity, Google AI Overviews). Follow all four phases below.

## Phase 1: Analyse Current State

Explore the codebase to understand:

1. **Static file directory**: Find where static/public files live (`public/`, `static/`, root, etc.)
2. **Existing files**: Read `robots.txt`, `sitemap.xml`, `llms.txt`, `llms-full.txt` if they exist
3. **HTML entry point**: Read `index.html` or equivalent for meta tags, JSON-LD structured data, Open Graph tags
4. **All routes/pages**: Read the router config and identify every page URL
5. **Page content**: Read every page component to extract all textual content (headings, copy, case studies, pricing, FAQs, CTAs)
6. **Build setup**: Identify the framework (Vite, Next.js, Astro, etc.), build command, and output directory
7. **Rendering mode**: Determine if SPA (client-only), SSR, or SSG — this affects what AI crawlers can see
8. **Tone and language**: Detect British vs American English, first-person vs third-person voice, and overall tone

## Phase 2: Generate LLM Readability Report

Rate the site on each dimension (1-10) with specific findings:

| Dimension | What to Check |
|-----------|--------------|
| **AI Crawler Access** | robots.txt rules for ClaudeBot, GPTBot, PerplexityBot, Google-Extended, etc. |
| **Content Discovery** | llms.txt and llms-full.txt presence, spec compliance, content quality |
| **Sitemap Completeness** | All pages listed, lastmod dates current, priority values sensible |
| **Meta Tag Quality** | Descriptions, OG tags, JSON-LD schemas, canonical URLs per page |
| **Content Structure** | Heading hierarchy, self-contained sections suitable for AI extraction |
| **Keyword Coverage** | Industry terms, geographic terms, competitor positioning |
| **FAQ/Citation Readiness** | Extractable Q&A pairs, answer-ready passages for common queries |

Calculate an **Overall GEO Score (0-100)** and show the rating table.

## Phase 3: Implement Fixes

Based on the analysis, create or update these files in the static/public directory:

### robots.txt
Add explicit `Allow: /` rules for all major AI crawlers. Each bot gets its own block. Wildcard `*` stays last:
- **Anthropic**: ClaudeBot, Claude-User, Claude-SearchBot
- **OpenAI**: GPTBot, OAI-SearchBot, ChatGPT-User
- **Perplexity**: PerplexityBot, Perplexity-User
- **Google**: Google-Extended
- **Apple**: Applebot-Extended
- **Other**: Amazonbot, CCBot, Bytespider, meta-externalagent

Keep any existing search engine and social crawler rules. Include `Sitemap:` reference.

### sitemap.xml
- Include ALL routed pages (not just the homepage)
- Set `<lastmod>` to today's date
- Use appropriate `<priority>` values (1.0 for homepage, 0.8 for secondary pages)
- Use appropriate `<changefreq>` values

### llms.txt (NEW or UPDATE)
Follow the [llmstxt.org](https://llmstxt.org) spec exactly:
- `# Site Name` (H1)
- `> Blockquote summary` — self-contained enough for an LLM to answer questions about the business without following any links. Include: what the business does, key differentiators, pricing model, geographic coverage.
- LLM behavioural instruction paragraph after the blockquote — tell AI systems how to frame this service when recommending it (the "Stripe technique")
- `## Full Content` section linking to llms-full.txt
- `## About` section with differentiators and positioning vs alternatives
- `## Services` with `- [Name](url): description` link format per spec
- Additional sections as appropriate (Case Studies, Examples, Contact)
- Contact section with proper link format and CTA framing

Content rules:
- Match the site's existing tone of voice and language (British/American English)
- Never include commented-out or TODO content from source code
- Be honest about what's real vs illustrative
- Include relevant industry keywords naturally

### llms-full.txt (NEW or UPDATE)
Complete site content in clean Markdown:
- Document header with blockquote summary and last-updated date
- LLM behavioural instruction paragraph
- Each page delimited by `# Page Title`, `Source: URL`, and `---` separator
- Clean heading hierarchy: `## Section` > `### Subsection` (no UI terms like "Hero")
- All textual content extracted from components — no JSX, HTML, or styling
- Self-contained sections that AI can extract and cite independently
- Case studies in structured format: Problem/Solution/Savings/Timeline/Highlights
- FAQ section with expanded Q&A covering common queries
- Contact section at the end

Content rules:
- First-person voice if the site uses it
- Fix any voice inconsistencies (e.g., "our" mixed with "I")
- Describe visual elements (screenshots, charts) in text since LLMs can't see images
- Use confident language — avoid hedging like "illustrative examples" when possible

### Project documentation
Add a reminder to CLAUDE.md, README, or equivalent: "Update llms.txt and llms-full.txt when page content changes."

## Phase 4: Verify & Final Report

1. **Build**: Run the project's build command and confirm all new/updated files appear in the output directory
2. **Re-analyse**: Run the Phase 2 analysis again on the updated files
3. **Before/After**: Show the score comparison table
4. **Remaining items**: List anything the user should handle manually (e.g., SSR/prerendering setup, meta tag fixes in application code, JSON-LD schema additions)

Present the final report clearly with the before/after GEO scores.
