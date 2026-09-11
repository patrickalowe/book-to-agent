# Book to Agent

Turn a shelf of books into a Claude agent that makes decisions the way those books would.

Most AI advice is generic because it isn't anchored to anything. This repo anchors it: pick the books that define how a job should be done, summarize each one into its core values and principles, then compile those summaries into an agent that cites them every time it recommends something.

## How it works

```
 books & articles ──▶ book-summarizer ──▶ summaries/*.md ──▶ compiled agent
                      (skill)             core values,       applies the principles,
                                          key principles,    names its source,
                                          key takeaways      flags where books disagree
```

1. **Summarize.** Run the `book-summarizer` skill on each book or article. Every summary has the same shape: Overview, Core Values, Key Principles, Key Takeaways. Because they all match, an agent can read any number of them the same way.
2. **Curate.** Choose which summaries belong to the agent. This is the actual design decision: the agent is only as good as the library you give it.
3. **Compile.** Write a `SKILL.md` that tells the agent to load the library before answering, which book governs which kind of question, how to resolve conflicts between sources, and what a good deliverable looks like.

## What's here

```
book-to-agent/
├── book-summarizer/
│   └── SKILL.md                         step 1: the summarizer
└── agents/
    └── ultimate-sales-manager/          a compiled agent
        ├── SKILL.md
        ├── fanatical-prospecting.md     Jeb Blount
        ├── sales-management-simplified.md  Mike Weinberg
        └── the-coaching-habit.md        Michael Bungay Stanier
```

### book-summarizer

Give it a book title and author, or an article URL, and it writes a 400–800 word Markdown summary to `summaries/<slug>.md`. It verifies the source exists before summarizing, keeps what a source *believes* (values) separate from what it tells you to *do* (principles), and won't invent contents for anything it can't verify.

### ultimate-sales-manager

A sales leadership advisor for a website design company, built from three books:

| Book | Governs |
|---|---|
| *Sales Management. Simplified.* (Weinberg) | The manager's calendar, culture, standards, and hard calls |
| *Fanatical Prospecting* (Blount) | The seller's daily behavior: pipeline, channels, call reluctance |
| *The Coaching Habit* (Bungay Stanier) | The shape of the conversation itself |

It diagnoses the upstream cause before prescribing a fix, cites the book behind each recommendation, names the tension when sources pull against each other, and ends with the single cheapest next step.

## Install

Skills go in your Claude Code skills directory:

```bash
git clone https://github.com/patrickalowe/book-to-agent.git
cp -R book-to-agent/book-summarizer ~/.claude/skills/book-summarizer
cp -R book-to-agent/agents/ultimate-sales-manager ~/.claude/skills/ultimate-sales-manager
```

Start a new Claude Code session, then:

```
summarize: "The Challenger Sale" by Matthew Dixon and Brent Adamson
```

```
My best rep has missed quota two months running and says the leads are bad. What do I do?
```

## Build your own agent

1. Summarize 3–5 books that define the role, using `book-summarizer`.
2. Make a folder under `agents/` and put the summaries in it.
3. Write its `SKILL.md`. Use `ultimate-sales-manager/SKILL.md` as a template, and be specific about:
   - **Loading:** read every summary in the folder first, so adding a book later changes the advice automatically.
   - **Jurisdiction:** which source answers which kind of question.
   - **Conflicts:** where the books disagree, and how to decide.
   - **Output:** what a finished answer looks like.
