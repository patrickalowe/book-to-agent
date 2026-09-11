---
name: book-summarizer
description: >-
  Summarize books and linked articles into Markdown files focused on their core
  values, actionable principles, and key takeaways. Use when the user provides
  a book title and author or an article URL and asks to summarize, extract core
  ideas, values, principles, lessons, or takeaways. Save book summaries to
  summaries/<book-slug>.md and article summaries to summaries/<article-slug>.md.
---

# Book and Article Summarizer

Turn a book title plus author or a linked article into one durable Markdown summary. Focus on what the source believes, what it advises the reader to do, and what matters most—not a section-by-section recap.

## Process

1. **Identify and verify the source.** For a book, confirm that the title and author match a real book. For an article URL, open the page and identify its title, author or publisher, publication date when available, and canonical URL. If the source cannot be accessed or verified, tell the user instead of inventing its contents.
2. **Gather the substance.** Ground every claim in the source. Identify its central thesis, core values, actionable principles, and most important lessons. Use web search only to verify or fill necessary context; do not substitute outside commentary for the source's argument.
3. **Write the file.** Save books to `summaries/<book-title-slug>.md` and articles to `summaries/<article-title-slug>.md` in the user's working folder. Use kebab-case. Create `summaries/` if needed. Overwrite an existing same-source file when refreshing it.
4. **Report the saved path** briefly.

## Book template

Use this exact structure for books:

```markdown
# <Title>
**Author:** <Author> · **Summarized:** <today's date>

## Overview
2–3 paragraphs: what the book argues, who wrote it and why they're credible, and why the book matters.

## Core Values
3–6 bullets. Bold each value name, then explain it in 1–2 sentences.

## Key Principles
5–10 bullets. Bold each principle, then explain what it means in practice in 1–2 sentences.

## Key Takeaways
3–5 bullets distilling the most important lessons.
```

## Article template

Use this exact structure for linked articles:

```markdown
# <Article title>
**Author/Publisher:** <name> · **Published:** <date or “Not stated”> · **Summarized:** <today's date>
**Source:** <canonical URL>

## Overview
2–3 paragraphs explaining the article's central argument, intended audience, context, and why it matters.

## Core Values
3–6 bullets. Bold each value name, then explain the belief or priority the article champions in 1–2 sentences.

## Key Principles
5–10 bullets. Bold each principle, then explain the article's practical recommendation in 1–2 sentences.

## Key Takeaways
3–5 bullets distilling the most important lessons.
```

## Quality bar

- Keep the summary 400–800 words: dense, useful, and non-exhaustive.
- Distinguish values—what the source believes in—from principles—what it tells the reader to do.
- Prefer the source's own framing and terminology over generic language, without inventing quotes.
- Preserve important qualifications, tradeoffs, and uncertainty. Do not turn the source's opinions or predictions into established facts.
- For commercial or promotional articles, summarize the useful argument while clearly attributing self-reported claims and avoiding uncritical endorsement.
- Do not merely restate headings. Synthesize the source into a coherent mental model the reader can apply.

## Examples

- `summarize: "Inspired" by Marty Cagan` → `summaries/inspired.md`
- `summarize: https://example.com/how-to-build-better-products` → `summaries/how-to-build-better-products.md`
