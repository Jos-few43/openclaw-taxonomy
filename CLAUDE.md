# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Taxonomic knowledge base organizing development tools and project management using Linnaean (biological) nomenclature. Acts as a reference library for tools, frameworks, and system components across the OpenClaw ecosystem.

## Tech Stack

| Component | Technology |
|---|---|
| Format | Markdown documentation |
| Scripts | Python (utilities) |

## Project Structure

```
openclaw-taxonomy/
├── automator/          # Script execution framework (scriptarum)
├── blueprints/         # Architecture designs (deep-research-v1)
├── capsula/            # Container systems (podmanica=Podman, distributa=Distrobox)
├── cortex/             # Session management (sessionis_curator)
├── monitor/            # Monitoring (usus)
├── vector/             # ML components
├── gestor/             # Model management
└── visuallizator/      # Visualization
```

## Cross-Repo Relationships

- **openclaw-workspace** — References this as the formal taxonomy system
- Provides naming conventions and organizational principles for the ecosystem

## Things to Avoid

- Don't break the Linnaean naming convention when adding new entries
