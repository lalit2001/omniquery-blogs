---
name: create-omniquery-blog
description: Use this skill when the user asks to "write a blog post", "create a blog", "write an article", "draft a post" about any OmniQuery-related topic — NL2SQL, data federation, AI analytics, integrations, product features, tutorials, or comparisons. Writes a complete MDX file ready to commit to the omniquery-blogs GitHub repo, including pixel art SVG diagrams generated via the create-pixel-art skill.
---

# Create OmniQuery Blog Post

Write a complete, publication-ready MDX blog post for OmniQuery. This skill works alongside the `create-pixel-art` skill — use it to generate SVG diagrams and flow charts that are embedded in the post.

## Repository & Publishing Info

- **GitHub repo**: `https://github.com/lalit2001/omniquery-blogs`
- **Published at**: `https://omniquery.ai/blog/{category}/{slug}`
- **Cache refresh**: Posts go live within 1 hour of pushing to `main` (ISR revalidate)

---

## Folder Structure

The repo has two parallel folder trees — one for MDX posts, one for SVG assets. **Mirror the category folder** when saving SVG files.

```
omniquery-blogs/
├── nl2sql/
│   └── what-is-nl2sql.mdx          ← blog post
├── tutorials/
│   └── connecting-postgresql.mdx
├── integrations/
│   └── mongodb-setup.mdx
├── product/
├── ai-analytics/
├── case-studies/
├── engineering/
│
└── assets/                         ← ALL SVG/image files go here
    ├── nl2sql/                      ← mirrors nl2sql/ category
    │   ├── nl2sql-flow.svg
    │   └── accuracy-comparison.svg
    ├── tutorials/                   ← mirrors tutorials/ category
    │   └── connection-diagram.svg
    ├── integrations/
    ├── product/
    ├── ai-analytics/
    ├── case-studies/
    └── engineering/
```

### Category folders for posts

| Folder | Use for |
|--------|---------|
| `nl2sql/` | What is NL2SQL, how it works, benchmarks, accuracy |
| `product/` | OmniQuery features, releases, changelogs, roadmap |
| `tutorials/` | Step-by-step guides, how-tos, getting started |
| `integrations/` | PostgreSQL, MySQL, MongoDB, Trino, Snowflake, S3, BigQuery |
| `ai-analytics/` | AI/LLM in data analytics, trends, comparisons |
| `case-studies/` | Customer stories, ROI, use cases by industry |
| `engineering/` | Architecture deep dives, technical decisions, internals |

---

## Required Frontmatter

Every MDX file MUST start with this block. All SEO fields are required:

```yaml
---
title: "Primary Keyword — Secondary Keyword | OmniQuery"
date: "YYYY-MM-DD"
slug: "url-friendly-slug-matching-filename"
description: "Action-oriented 1–2 sentences under 160 chars. State the benefit and include the primary keyword."
tags: ["tag1", "tag2", "tag3"]
author: "Author Full Name"
authorImage: "https://github.com/lalit2001.png"
readTime: "X min read"
---
```

### Frontmatter rules
- `title` — include primary keyword early; append `| OmniQuery` for brand SEO
- `slug` — must exactly match the filename (without `.mdx`), keyword-rich
- `date` — `YYYY-MM-DD` format
- `description` — under 160 chars, includes primary keyword, action-oriented (e.g. "Learn how…", "Discover…")
- `tags` — 3–6 lowercase tags, mix of specific (`nl2sql`) and broad (`analytics`, `ai`)
- `readTime` — estimate at ~200 words/min (1000 words = "5 min read")
- `authorImage` — GitHub avatar URL: `https://github.com/{username}.png`

---

## SEO Best Practices

### Title formula
```
Primary Keyword: What/How/Why + Benefit | OmniQuery
```
Examples:
- `"NL2SQL Explained: How AI Turns Questions into SQL in Milliseconds | OmniQuery"`
- `"Connecting PostgreSQL to OmniQuery: Step-by-Step Guide | OmniQuery"`
- `"OmniQuery vs Dashboards: Why Natural Language Wins for Ad-hoc Analytics | OmniQuery"`

### Description formula
```
[Action verb] + [primary keyword] + [benefit/outcome]. [Supporting detail].
```
Examples:
- `"Discover how NL2SQL converts plain English to SQL instantly—no analyst needed. See benchmarks, real examples, and how OmniQuery does it."`
- `"Step-by-step guide to connecting PostgreSQL to OmniQuery. Enable natural language queries on your Postgres data in under 5 minutes."`

### In-content SEO checklist
- [ ] Primary keyword in H1 title
- [ ] Primary keyword in first 100 words of body
- [ ] 3–5 H2 headings that match search intent phrases
- [ ] At least one H3 per H2 section
- [ ] Internal links: link to `/contact?type=demo` and relevant `/blog` posts
- [ ] External links: link to official docs of mentioned technologies (PostgreSQL, etc.)
- [ ] Alt text on all images = descriptive keyword phrase, not just "image"
- [ ] At least one table or comparison for featured snippet targeting

---

## SVG Diagrams — Generating with create-pixel-art Skill

**Every technical blog post should have at least one custom SVG diagram.** Use the `create-pixel-art` skill to generate it.

### When to generate SVGs

| Post type | Suggested SVG |
|-----------|--------------|
| Architecture / how-it-works | Flow diagram showing data path |
| Integration guide | Connection diagram (source → OmniQuery → output) |
| Comparison post | Side-by-side comparison canvas |
| Tutorial | Step diagram showing the process |
| Benchmark / metrics | Bar chart pixel canvas |

### Workflow for generating and embedding an SVG

**Step 1 — Generate the SVG using create-pixel-art:**
Invoke the `create-pixel-art` skill with a description of the diagram needed. Example prompt:
> "Create a pixel art flow diagram showing: PostgreSQL → OmniQuery Agent → Trino → SQL Result, with animated flow dots and OmniQuery watermark"

**Step 2 — Save the SVG to the assets mirror folder:**
```
assets/{category}/{descriptive-name}.svg
```
Example: `assets/nl2sql/nl2sql-architecture-flow.svg`

**Step 3 — Get the raw GitHub URL:**

GitHub blob URL (what you see in browser):
```
https://github.com/lalit2001/omniquery-blogs/blob/main/assets/nl2sql/nl2sql-architecture-flow.svg
```

Raw content URL (what to use in MDX — replace `github.com` path):
```
https://raw.githubusercontent.com/lalit2001/omniquery-blogs/main/assets/nl2sql/nl2sql-architecture-flow.svg
```

**Conversion rule:**
```
github.com/{user}/{repo}/blob/{branch}/{path}
        ↓
raw.githubusercontent.com/{user}/{repo}/{branch}/{path}
```

**Step 4 — Embed in MDX:**

Option A — Raw URL (SVG hosted in assets/ folder):
```md
![NL2SQL Architecture: How OmniQuery converts natural language to SQL](https://raw.githubusercontent.com/lalit2001/omniquery-blogs/main/assets/nl2sql/nl2sql-architecture-flow.svg)
```

Option B — Inline SVG (paste SVG code directly into MDX):
```mdx
<svg width="960" height="540" viewBox="0 0 960 540" xmlns="http://www.w3.org/2000/svg">
  <!-- SVG content here — animations work, no hosting needed -->
</svg>
```

### When to use each option

| Option | Use when | Pros | Cons |
|--------|----------|------|------|
| Raw URL | SVG committed to repo | Clean MDX, easy to update SVG separately | Needs file committed first |
| Inline SVG | Quick/one-off diagrams | No separate file needed, instant | Makes MDX file large |

> **Always use the raw URL approach** for reusable diagrams. Inline SVG for quick one-off visuals only.

### Alt text for SVGs (SEO)
Alt text on SVG images is used as a caption AND for SEO. Make it descriptive:
```md
<!-- Bad -->
![diagram](https://raw.githubusercontent.com/...)

<!-- Good -->
![NL2SQL flow: natural language query → OmniQuery agent → Trino SQL → result table](https://raw.githubusercontent.com/...)
```

---

## Content Structure

```
# H1 Title (matches frontmatter title, includes primary keyword)

Opening hook — bold claim, striking stat, or vivid problem statement.
Include primary keyword naturally within first 100 words.

## H2: Section matching a search intent phrase
Brief intro sentence.

### H3: Subsection
Content...

## H2: Another Section

![Descriptive alt text for SEO](https://raw.githubusercontent.com/lalit2001/omniquery-blogs/main/assets/{category}/{name}.svg)

## H2: Comparison or Data Section

| Column A | Column B | Column C |
|----------|----------|----------|
| ...      | ...      | ...      |

## Conclusion
3–5 key takeaways as bullet points, then CTA.
```

### CTA (always include at the end)
```md
---

**Ready to experience OmniQuery?** [Book a free demo](/contact?type=demo) or [start building](/contact?type=demo) — turn every business question into an instant SQL insight.
```

---

## Supported MDX Features

### Regular images
```md
![Descriptive alt text](https://publicly-accessible-image-url.jpg)
```

### SVG from GitHub assets
```md
![Flow description for SEO](https://raw.githubusercontent.com/lalit2001/omniquery-blogs/main/assets/{category}/{name}.svg)
```

### Inline SVG (animations work)
```mdx
<svg width="800" height="400" viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
  <!-- paste SVG code directly -->
</svg>
```

### Tables (featured snippet targeting)
```md
| Aspect | Traditional BI | OmniQuery NL2SQL |
|--------|---------------|------------------|
| Setup time | Days | Minutes |
| Ad-hoc queries | Limited | Unlimited |
```

### Code blocks
````md
```sql
SELECT region, SUM(revenue) AS total
FROM sales WHERE quarter = 'Q4'
GROUP BY region ORDER BY total DESC;
```
````
Supported: `sql`, `python`, `bash`, `typescript`, `javascript`, `yaml`, `json`

### Callouts
```md
> **Pro tip:** OmniQuery self-heals SQL — if the generated query fails validation, it retries with the error context up to 3 times automatically.
```

---

## Writing Guidelines

### Tone
- **Authoritative but approachable** — expert insights, no unnecessary jargon
- **Practical** — always answer "so what?" and "how do I use this today?"
- **OmniQuery-first** — tie every concept back to OmniQuery naturally

### Content quality checklist
- [ ] H1 includes primary keyword
- [ ] Primary keyword in first 100 words
- [ ] At least 1 custom SVG diagram (generated via `create-pixel-art`)
- [ ] At least 1 table for comparison or data
- [ ] At least 1 code example for technical posts
- [ ] Each H2 delivers one clear idea
- [ ] Real numbers and specifics — no vague claims
- [ ] CTA at the end linking to `/contact?type=demo`
- [ ] Alt text on all images is descriptive (not generic)

---

## Step-by-Step Workflow

1. **Clarify the topic** — get topic, target audience, primary keyword, and any specific angle
2. **Choose the category folder** — pick from the table or create a new lowercase hyphenated folder
3. **Generate the slug** — lowercase, hyphen-separated, keyword-rich, matches filename
4. **Plan SVG diagrams** — decide which diagrams would help (flow, comparison, architecture)
5. **Generate SVGs** — invoke `create-pixel-art` skill for each diagram; save to `assets/{category}/{name}.svg`
6. **Write the full post** — frontmatter + body with H1/H2/H3 structure, embedded SVGs via raw URLs, table, code block, CTA
7. **Save the MDX** — write to `{category}/{slug}.mdx`
8. **Confirm** — report: file path, SVG asset paths, published URL, and live time

---

## Example Output

**Files to commit:**
```
nl2sql/what-is-nl2sql.mdx
assets/nl2sql/nl2sql-flow.svg
```

**Published URL:** `https://omniquery.ai/blog/nl2sql/what-is-nl2sql`
**Live:** within 1 hour of push to `main`

```mdx
---
title: "NL2SQL Explained: How AI Turns Plain English into SQL in Milliseconds | OmniQuery"
date: "2026-03-03"
slug: "what-is-nl2sql"
description: "Discover how NL2SQL converts natural language questions into SQL instantly—no analyst needed. See how OmniQuery does it with real examples."
tags: ["nl2sql", "ai", "sql", "analytics", "business-intelligence"]
author: "Lalit Moharana"
authorImage: "https://github.com/lalit2001.png"
readTime: "6 min read"
---

# NL2SQL Explained: How AI Turns Plain English into SQL in Milliseconds

Every business decision depends on data — but most employees can't write SQL...

## What is NL2SQL?

NL2SQL (Natural Language to SQL) is AI technology that translates plain English questions...

## How NL2SQL Works: Step by Step

![NL2SQL architecture: natural language → OmniQuery agent → Trino SQL → result](https://raw.githubusercontent.com/lalit2001/omniquery-blogs/main/assets/nl2sql/nl2sql-flow.svg)

### 1. Natural Language Understanding
...

## NL2SQL vs Traditional Dashboards

| Feature | Traditional Dashboards | NL2SQL (OmniQuery) |
|---------|----------------------|-------------------|
| Time to insight | Days | Seconds |
| Ad-hoc queries | Pre-built only | Unlimited |
| User skill needed | BI tool training | Plain English |

## Getting Started with OmniQuery

```sql
-- OmniQuery translates this question:
-- "Show me top 5 products by revenue last quarter"
SELECT product_name, SUM(revenue) as total_revenue
FROM sales
WHERE quarter = 'Q4' AND year = 2025
GROUP BY product_name
ORDER BY total_revenue DESC
LIMIT 5;
```

## Conclusion

- NL2SQL removes the technical barrier between employees and data
- OmniQuery generates, validates, and self-heals SQL automatically
- Time-to-insight drops from days to seconds

---

**Ready to experience OmniQuery?** [Book a free demo](/contact?type=demo) and see NL2SQL on your own data.
```
