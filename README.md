# wikis

An Obsidian vault that acts as a unified shell for multiple LLM-maintained knowledge wikis.

## Concept

Inspired by [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — instead of querying raw documents every time (RAG), an LLM **compiles** sources into a structured, interlinked markdown wiki. Knowledge is built up incrementally, not rediscovered at each question.

This repo only tracks the **shared configuration** (Obsidian vault settings, Claude Code template). Each project wiki lives in its own git repository and is cloned into this directory.

## Structure

```
wikis/                        ← Obsidian vault (this repo)
├── .obsidian/                ← Vault config
├── .claude/                  ← Claude Code template (copy into each project)
│   ├── CLAUDE.md             ← Wiki librarian instructions
│   └── commands/
│       ├── ingest.md         ← /ingest <file> — process a source into wiki pages
│       └── lint.md           ← /lint — check for broken links, contradictions, orphans
├── project-a/                ← Wiki project (separate git repo)
├── project-b/                ← Wiki project (separate git repo)
└── ...
```

## Usage

### Setting up a new project wiki

```bash
cd wikis/
git clone <project-wiki-repo>
cp -r .claude/ <project>/
```

Each project wiki follows this internal structure:

```
project/
├── raw/       ← Source documents (never modified by the LLM)
├── wiki/      ← Generated markdown pages, interlinked with [[wikilinks]]
│   ├── index.md
│   └── log.md
└── CLAUDE.md
```

### Maintaining a wiki

- **`/ingest <file>`** — Feed a new source document. The LLM reads it, creates or updates wiki pages, and refreshes the index.
- **`/lint`** — Run a health check: broken links, orphan pages, missing sources, contradictions.

## Why this setup

- **One vault, many wikis** — Obsidian's graph view and search work across all projects at once
- **Config-only repo** — Clone this repo to recreate the environment anywhere, then clone your project wikis into it
- **Each wiki is independent** — Separate git history, can be shared or kept private individually
