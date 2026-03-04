---
name: create-omniquery-blog
description: Use this skill when the user asks to "write a blog post", "create a blog", "write an article", "draft a post" about any OmniQuery-related topic — NL2SQL, data federation, AI analytics, integrations, product features, tutorials, or comparisons. Writes a complete MDX file ready to commit to the omniquery-blogs GitHub repo.
---

# Create OmniQuery Blog Post

Write a complete, publication-ready MDX blog post for OmniQuery and save it to the correct location in the `omniquery-blogs` GitHub repository structure.

## Repository & Publishing Info

- **GitHub repo**: `https://github.com/lalit2001/omniquery-blogs`
- **Local clone path** (if working locally): anywhere — the file just needs to be committed to the repo
- **Published at**: `https://omniquery.ai/blog/{category}/{slug}`
- **Cache refresh**: Posts appear on the site within 1 hour of being pushed (ISR revalidate)

## Folder Structure (Categories)

Each top-level folder is a category shown as a filter tab on `/blog`. Put the MDX file inside the matching category folder:

| Folder | Use for |
|--------|---------|
| `nl2sql/` | What is NL2SQL, how it works, benchmarks, accuracy |
| `product/` | OmniQuery features, releases, changelogs, roadmap |
| `tutorials/` | Step-by-step guides, how-tos, getting started |
| `integrations/` | PostgreSQL, MySQL, MongoDB, Trino, Snowflake, S3, BigQuery |
| `ai-analytics/` | AI/LLM in data analytics, trends, comparisons |
| `case-studies/` | Customer stories, ROI, use cases by industry |
| `engineering/` | Architecture deep dives, technical decisions, internals |

If the topic doesn't fit any existing folder, create a new sensibly named folder (lowercase, hyphen-separated).

## Required Frontmatter

Every MDX file MUST start with this frontmatter block:

```yaml
---
title: "Your Post Title Here"
date: "YYYY-MM-DD"
slug: "url-friendly-slug-matching-filename"
description: "One or two sentences. Used for SEO meta description and card preview. Keep under 160 chars."
tags: ["tag1", "tag2", "tag3"]
author: "Author Full Name"
authorImage: "https://publicly-accessible-avatar-url.jpg"
readTime: "X min read"
---
```

### Frontmatter rules
- `slug` must exactly match the filename (without `.mdx`)
- `date` must be `YYYY-MM-DD` format
- `tags` — 3 to 6 lowercase tags relevant to the content
- `readTime` — estimate based on ~200 words/min (e.g. 1000 words = "5 min read")
- `authorImage` — use a publicly accessible URL. GitHub avatar: `https://github.com/{username}.png`

## File Naming

- Filename = slug + `.mdx`
- All lowercase, words separated by hyphens
- Descriptive and URL-friendly
- Example: `what-is-nl2sql.mdx`, `connecting-postgresql-omniquery.mdx`

## Content Structure

Structure every post with these sections (adapt as needed):

```
# Post Title (H1 — only one per post)

Opening paragraph — hook the reader, state the problem or question.

## Section 1 (H2)
...

### Subsection (H3 if needed)
...

## Section 2 (H2)
...

## Conclusion
Summarise key takeaways. End with a CTA pointing to OmniQuery.
```

### CTA at the end (always include)
```md
---

**Ready to try OmniQuery?** [Book a demo](/contact?type=demo) or [start building](/contact?type=demo) — turn every employee into a data analyst.
```

## Markdown Features Supported

All GitHub Flavored Markdown (GFM) is supported:

### Images
```md
![Alt text / caption](https://publicly-accessible-image-url.jpg)
```
- Use public URLs only (Unsplash, your CDN, GitHub raw, etc.)
- Alt text is shown as a caption below the image
- Recommended width: 800px+

### Tables
```md
| Column A | Column B | Column C |
|----------|----------|----------|
| Value    | Value    | Value    |
```

### Code blocks
````md
```sql
SELECT region, SUM(revenue) AS total
FROM sales
WHERE quarter = 'Q4'
GROUP BY region
ORDER BY total DESC;
```
````

Supported languages: `sql`, `python`, `bash`, `typescript`, `javascript`, `yaml`, `json`

### Callouts (blockquotes)
```md
> **Pro tip:** OmniQuery automatically retries failed SQL with self-healing logic up to 3 times.
```

## Writing Guidelines

### Tone & Voice
- **Authoritative but approachable** — expert insights without jargon overload
- **Practical** — always answer "so what?" and "how do I use this?"
- **OmniQuery-first** — tie concepts back to OmniQuery capabilities naturally, not forcefully

### Content Quality Checklist
- [ ] Opening paragraph hooks the reader with a problem or bold claim
- [ ] Each H2 section delivers one clear idea
- [ ] At least one code example, table, or image per technical post
- [ ] Real numbers and specifics (avoid vague claims like "much faster")
- [ ] Comparisons are fair — acknowledge trade-offs
- [ ] Conclusion summarises 3-5 key takeaways
- [ ] Ends with a CTA

### SEO
- Title should include the primary keyword naturally
- Description should be compelling and under 160 characters
- Use the primary keyword in the first 100 words of body content
- Use H2/H3 headings that people would search for

## Topic Ideas by Category

### nl2sql/
- What is NL2SQL and how does it work
- NL2SQL accuracy benchmarks: OmniQuery vs competitors
- How OmniQuery validates and self-heals SQL
- NL2SQL for non-technical users: a guide
- Complex queries with NL2SQL: joins, aggregations, subqueries

### tutorials/
- Getting started with OmniQuery in 5 minutes
- Connecting your first PostgreSQL database
- Building a sales dashboard with natural language
- Setting up role-based access control
- How to embed OmniQuery in your SaaS product

### integrations/
- Connecting MongoDB to OmniQuery
- Using OmniQuery with Snowflake
- Federated queries across PostgreSQL and S3
- Trino federation with OmniQuery explained

### ai-analytics/
- Why LLMs are better than dashboards for ad-hoc analysis
- Multi-LLM support: choosing between GPT-4, Claude, and Gemini
- The future of business intelligence: conversational data

### engineering/
- How OmniQuery's LangGraph agent works
- ChromaDB and RAG for schema retrieval
- Self-healing SQL: the validate-retry loop
- Multi-arch Docker builds for OmniQuery

## Step-by-Step Workflow

1. **Clarify the topic** — ask the user for topic, target audience, and any specific angle if not provided
2. **Choose the category folder** — pick from the table above or create a new one
3. **Generate the slug** — lowercase, hyphen-separated, keyword-rich
4. **Write the full post** — frontmatter + complete body with all sections
5. **Save the file** — write to the correct path: `{category}/{slug}.mdx`
6. **Confirm** — tell the user the file path and the URL it will be published at

## Example Output

File saved at: `nl2sql/what-is-nl2sql.mdx`
Published URL: `https://omniquery.ai/blog/nl2sql/what-is-nl2sql`
Appears on site: within 1 hour of pushing to `main`

```mdx
---
title: "What is NL2SQL? Plain English Queries for Your Database"
date: "2026-03-03"
slug: "what-is-nl2sql"
description: "NL2SQL turns natural language questions into SQL queries instantly. Learn how it works and why it's replacing traditional dashboards."
tags: ["nl2sql", "ai", "sql", "analytics"]
author: "Lalit Moharana"
authorImage: "https://github.com/lalit2001.png"
readTime: "6 min read"
---

# What is NL2SQL? Plain English Queries for Your Database

Ask your database a question in plain English and get an answer in seconds...

## How NL2SQL Works

...

## NL2SQL vs Traditional Dashboards

| Feature | Dashboards | NL2SQL |
|---------|-----------|--------|
| Setup time | Days | Minutes |
| Ad-hoc queries | Limited | Unlimited |

![NL2SQL query flow](https://...)

## Getting Started with OmniQuery

...

## Conclusion

...

---

**Ready to try OmniQuery?** [Book a demo](/contact?type=demo) and see NL2SQL in action on your own data.
```



# What is OmniQuery? Complete Guide to Features and Capabilities

Organizations today have data spread across numerous databases, data warehouses, and data lakes. Accessing, querying, and distributing that data often requires complex workflows and technical expertise. OmniQuery solves this by providing a unified, AI-driven platform that completely transforms how both technical and non-technical teams interact with their data.

Without diving into the complex technical internals, this guide walks you through what OmniQuery actually is, the core features you can leverage, and everything you can accomplish within the platform.

## A Unified Hub: What Pages and Tools Do I Have?

OmniQuery is designed with a clean, intuitive interface composed of purpose-driven pages and dashboards. Whether you're an administrator setting up database connections or an end-user running natural language queries, the platform offers a streamlined experience tailored to your role.

### Multi-Database Support & Flexible Output Formats

Data lives everywhere, which is why OmniQuery is built with extensive **multi-database support**. You can connect to a wide array of supported databases entirely from the UI, bringing all your disparate data sources into one federated view. 

But querying is only half the battle—sharing results is just as critical. Whenever you run a query, you can export and visualize your results in nearly **all output formats**. Whether you need raw CSV or JSON data for another application, or fully rendered markdown tables and visual charts for a presentation, OmniQuery handles it seamlessly.

## Core Features and Capabilities

### 1. Robust User & Role Management
Security and collaboration go hand-in-hand. OmniQuery provides comprehensive access control pages where administrators can:
- **Add Users:** Quickly invite and onboard new team members to your organization's workspace.
- **Add Roles:** Implement strict Role-Based Access Control (RBAC). You can define user roles and set precise permissions so that everyone has access to the data they need, without compromising sensitive information.

### 2. Customisable AI Settings
One of OmniQuery's standout features is its adaptable AI engine. Instead of a one-size-fits-all approach, you get dedicated settings pages to customize the "brain" powering your analytics:
- **Save Embedding Settings:** Configure and tweak your embedding models to ensure OmniQuery perfectly understands the semantic context of your specific enterprise data.
- **LLM Model Settings:** You're not locked into a single AI provider. Choose, configure, and save your preferred Large Language Model (LLM) settings to balance speed, cost, and analytical reasoning exactly how you want.

### 3. Embeddable Analytics via IFrame
Your data insights shouldn't be trapped inside the OmniQuery dashboard. We make it incredibly easy to share your findings with the rest of the world.
- **Create and Share:** Instantly generate secure, interactive iframe snippets for any query result, chart, or dashboard.
- **Embedded Capabilities:** Drop these iframes directly into your own SaaS applications, internal wikis (like Notion or Confluence), or client-facing portals. It takes just seconds to turn an OmniQuery insight into a native-feeling embedded analytics feature on your own site.

OmniQuery shifts the focus from managing data infrastructure to actually extracting value from it. By combining broad multi-database support with powerful user management, adaptable AI model settings, and a robust embedded analytics engine, OmniQuery gives you a comprehensive toolkit to make your data work for you.
