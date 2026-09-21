# Thesis LLM Wiki

A personal AI-maintained knowledge base for my Master's thesis research on
text-to-image generation, prompt engineering, prompt modifiers, image quality,
diversity, and prompt alignment evaluation.

The project is inspired by Andrej Karpathy's LLM Wiki pattern: instead of
keeping research notes scattered across PDFs, chats, and documents, an LLM agent
continuously turns source material into a structured, cross-linked Markdown wiki.

## Why I built this

While working on my Master's thesis, the number of research papers quickly started
to grow. It became difficult to remember:

- which paper introduced a particular method;
- which datasets and metrics were used;
- what the main findings and limitations were;
- where different papers agreed or disagreed;
- which sources were relevant to a specific thesis section.

This project turns those papers into a persistent knowledge base that can be
queried and updated over time.

## How it works

The repository has three main parts:

```text
raw/
    papers/       Original research papers
    notes/        Personal research notes

wiki/
    papers/       One structured page per paper
    concepts/     Shared concepts and terminology
    methods/      Evaluation methods and metrics
    index.md      Entry point to the knowledge base
    log.md        History of wiki operations

AGENTS.md         Instructions defining how the AI agent maintains the wiki
```

The source files in `raw/` are treated as immutable.

An AI coding agent reads `AGENTS.md` and performs operations such as:

### Ingest

```text
ingest @raw/papers/paper.pdf
```

The agent:

1. reads the paper;
2. extracts the research question, methodology, datasets, models, metrics,
   results and limitations;
3. creates a structured paper page;
4. creates or updates related concept and method pages;
5. adds cross-links between related topics;
6. updates the wiki index and operation log.

For example, several papers may contribute to the same page:

```text
Paper A ──┐
          ├──> concepts/prompt-engineering.md
Paper B ──┤
Paper C ──┘
```

This is the main difference from simply generating an independent summary for
every PDF: knowledge from new sources is integrated into the existing wiki.

### Query

The agent can answer questions using the accumulated knowledge base:

```text
query "Which papers discuss prompt alignment metrics?"
```

or:

```text
query "What are the limitations of FID for evaluating generated images?"
```

The agent first inspects the wiki and then synthesizes an answer from relevant
pages and sources.

### Lint

```text
lint the wiki
```

The agent audits the knowledge base for issues such as:

- broken wiki links;
- duplicate concept pages;
- orphan pages;
- missing source attribution;
- missing index entries;
- repeated concepts that should have their own page.

## Obsidian

The repository can be opened directly as an
[Obsidian](https://obsidian.md/) vault.

Because the knowledge base consists of Markdown files and `[[wikilinks]]`,
Obsidian provides navigation, backlinks and graph visualization without requiring
a custom frontend.

I currently use Obsidian Copilot with an agent backend to maintain the wiki
directly from the vault.

## Reproducing the setup

A similar wiki can be created for any research or study topic.

### 1. Create the repository

```bash
mkdir my-llm-wiki
cd my-llm-wiki

git init

mkdir -p raw/papers raw/notes
mkdir -p wiki/papers wiki/concepts wiki/methods

touch wiki/index.md wiki/log.md
touch AGENTS.md
```

### 2. Define agent instructions

`AGENTS.md` should describe:

- the purpose of the knowledge base;
- directory structure;
- the ingest workflow;
- required page format;
- source and citation rules;
- query behaviour;
- wiki linting rules.

### 3. Add source material

Place PDFs and other source documents into:

```text
raw/papers/
```

### 4. Connect an AI agent

Use an agent with filesystem access, for example:

- Codex;
- Claude Code;
- an agent integrated into Obsidian.

The agent should load `AGENTS.md` as project instructions.

### 5. Ingest sources

Process sources incrementally:

```text
ingest @raw/papers/example.pdf
```

New papers should update existing concept pages whenever appropriate instead of
creating duplicate summaries.

## Git and source files

The original research PDFs are intentionally excluded from version control.

Example `.gitignore`:

```gitignore
raw/
.obsidian/
.copilot/
.agents/
copilot/
```

The repository therefore contains the generated knowledge base and agent
configuration, while the original documents remain local.

## Inspiration

This project is inspired by Andrej Karpathy's LLM Wiki approach: using an LLM
agent to maintain a persistent, structured knowledge artifact rather than losing
useful information inside individual chat sessions.

- Andrej Karpathy: https://karpathy.ai/blog/wiki.html

## Current use case

The wiki currently supports research for a Master's thesis focused on
text-to-image generation and evaluation, including topics such as:

- prompt engineering and prompt modifiers;
- image quality and realism evaluation;
- diversity metrics;
- prompt-image alignment;
- FID;
- CLIP-based metrics;
- aesthetic scoring.
