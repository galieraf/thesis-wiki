# Thesis LLM Wiki

This repository is a knowledge base for a Master's thesis about
text-to-image generation, prompt engineering, prompt modifiers,
image quality, diversity, and prompt alignment evaluation.

## Structure

raw/
  papers/       Research papers
  notes/        Personal notes

wiki/
  index.md      Main table of contents
  log.md        Change log
  papers/       One page per paper
  concepts/     Concepts and terminology
  methods/      Evaluation methods and metrics

## Ingest workflow

When asked to ingest a paper:

1. Read the source carefully.
2. Identify:
   - research question
   - motivation
   - methodology
   - datasets
   - models
   - metrics
   - main results
   - limitations
   - relevance to the thesis
3. Create or update a paper page in `wiki/papers/`.
4. Create or update relevant concept pages in `wiki/concepts/`.
5. Create or update relevant method pages in `wiki/methods/`.
6. Cross-link related pages using [[wikilinks]].
7. Update `wiki/index.md`.
8. Append the operation to `wiki/log.md`.

Never modify files inside `raw/`.

Before creating a new concept or method page, inspect the existing wiki
and update an existing page when appropriate.

## Paper page format

# Paper title

**Authors:**
**Year:**
**Source:**
**Last updated:**

## Research question

## Motivation

## Method

## Datasets

## Models

## Metrics

## Main findings

## Limitations

## Relevance to my thesis

## Related pages

## Query workflow

When asked a question:

1. Read `wiki/index.md`.
2. Locate relevant wiki pages.
3. Read those pages.
4. Answer primarily from the wiki.
5. Mention which pages or papers support the answer.
6. If the answer is not supported by the wiki, say so clearly.

## Lint workflow

When asked to lint the wiki:

- find broken wikilinks
- find duplicate concept pages
- find orphan pages
- find papers without source attribution
- find missing entries in index.md
- find concepts mentioned repeatedly but lacking their own page

@AGENTS.md
