---
name: Search Workflow
description: The 4-phase paper search workflow from parallel search to download. Use when coordinating the multi-agent paper search pipeline.
version: 1.0.0
---

# 4-Phase Paper Search Workflow

## Phase Overview

| Phase | Name            | Lead                 | Output                          |
| ----- | --------------- | -------------------- | ------------------------------- |
| 1     | Parallel Search | Marshall (3 scouts)  | Raw results from 14+ databases  |
| 2     | Aggregation     | Marshall + Archivist | Deduplicated, ranked paper list |
| 3     | Presentation    | Marshall             | Formatted tables for user       |
| 4     | Download        | Librarian            | PDF files or manual links       |

## Phase Dependencies

```
Phase 1: Scout-Core ──┐
         Scout-Domain ─┤──→ Phase 2 ──→ Phase 3 ──→ Phase 4
         Scout-Cloud ──┘         ▲                      │
                                 │                      │
                           Archivist              Librarian
                         (deduplicate)           (download)
```

- Phase 1 agents run in PARALLEL
- Phase 2 begins only after ALL Phase 1 agents complete
- Phase 4 requires user confirmation

## Database Tiers

| Tier     | Databases                                                                                                        | Agent        |
| -------- | ---------------------------------------------------------------------------------------------------------------- | ------------ |
| 1 Core   | Google Scholar, Semantic Scholar, OpenAlex, CrossRef                                                             | Scout-Core   |
| 2 Domain | arXiv, PubMed, bioRxiv, medRxiv, DBLP, SSRN, IACR, OpenAIRE, BASE, CORE, DOAJ, Zenodo, Unpaywall, PMC, EuropePMC | Scout-Domain |
| 3 Cloud  | Consensus, Scholar Gateway, ResearchGate (Tavily)                                                                | Scout-Cloud  |
