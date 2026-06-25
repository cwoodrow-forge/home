---
categories:
  - "[[Permanent Notes]]"
subjects:
  - "[[Technology]]"
  - "[[Productivity]]"
type: concept
status: seedling
description: "Andrej Karpathy's LLM Wiki pattern — flat Markdown files fed directly into an LLM, bypassing RAG for personal knowledge bases."
resource: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
tags:
  - llm
  - knowledge-management
  - karpathy
  - rag
created: 2026-06-21
---

Created by Andrej Karpathy, former Head of AI at Tesla and Open AI Co-Founder. 

# The concept
The core idea is simple. You maintain a collection of plain text or Markdown files — your “wiki” — organized around topics, concepts, projects, or anything you care about. When you want to query that knowledge, you feed the files directly into an LLM like Claude and ask your question.

That’s it. No database. No indexing. No retrieval pipeline to maintain.

A personal wiki, in Karpathy’s usage, isn’t a Notion database or a Roam Research graph. It’s deliberately flat and portable:

- Plain `.txt` or `.md` files
- Human-readable without any app
- No proprietary format or lock-in
- Easy to version with Git
- Trivial to concatenate and pass to an LLM

The goal is durability and portability. Your knowledge base should work with any LLM that exists today or will exist in ten years.

### How is this different from RAG (Retrieval-Augmented Generation)?

RAG splits your documents into chunks, embeds them as vectors, and retrieves relevant chunks at query time. The LLM Wiki pattern skips all of that — it loads the full knowledge base directly into the model’s context window. RAG is better for large enterprise document stores. Direct context loading is simpler and often more accurate for personal knowledge bases that fit within a model’s context limit. LLM WiKi leverages the large and efficient context window of most of the foundation model, especially Claude.

In short:
- Better for personal knowledge (50,000 - 100,000 words) 
- Unsuitable for enterprise scaled repositories (millions of words)

## Use cases

### Personal Research Database

If you read academic papers, newsletters, or books and take notes, your LLM wiki becomes a queryable research database. “What did I write about transformer attention mechanisms?” becomes a valid query instead of a search through disorganized files.

### Project Memory

Software teams or solo developers can maintain a wiki of architectural decisions, debugging notes, and lessons learned. Querying it with Claude surfaces relevant context before starting a new feature.

### Writing and Thinking Assistant

Feed your wiki to Claude and ask it to help you write something new. “Based on my notes on Warhammer Hobby, help me outline an argument about painting techniques” leverages your accumulated thinking rather than starting from scratch.

### Second Brain

Knowledge workers — consultants, researchers, analysts — accumulate domain-specific knowledge over years. A personal wiki plus Claude turns that accumulated knowledge into an interactive resource.

# External References:
https://community.obsidian.md/plugins/karpathywiki
https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing
https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
