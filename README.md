# Agent Teams PaperSearch

> A multi-agent academic paper search framework powered by Claude Code. Five specialized AI agents search 14+ databases in parallel, aggregate results, download PDFs, and find mirror links.

```
┌──────────────────────────────────────────────────────┐
│                   Marshall (Coordinator)              │
│              /paper-search <query>                    │
└──────┬──────────────┬──────────────┬─────────────────┘
       │              │              │
       ▼              ▼              ▼         (parallel)
┌────────────┐ ┌────────────┐ ┌────────────┐
│ Scout-Core │ │Scout-Domain│ │Scout-Cloud │
│ 4 databases│ │15 databases│ │ 3 sources  │
│ GS+SS+OA+CR│ │arXiv,PubMed│ │Consensus   │
│            │ │bioRxiv,DBLP│ │ScholarGW   │
│            │ │SSRN,BASE...│ │ResearchGate│
└─────┬──────┘ └──────┬─────┘ └──────┬─────┘
      │               │              │
      └───────────────┼──────────────┘
                      ▼
              ┌──────────────┐
              │  Archivist   │
              │ Deduplicate  │
              │ Rank & Verify│
              └──────┬───────┘
                     ▼
              ┌──────────────┐
              │  Librarian   │
              │ Download PDF │
              │ or give links│
              └──────────────┘
```

## Quick Install

### Option A: One-Command Install (Recommended)

```bash
claude plugin marketplace add Xinjing-Guo/Agent-Teams-PaperSearch --sparse .claude-plugin plugin
claude plugin install agent-teams-papersearch
```

### Option B: Local Install

```bash
git clone https://github.com/Xinjing-Guo/Agent-Teams-PaperSearch.git
claude plugin add ./Agent-Teams-PaperSearch/plugin/agent-teams-papersearch
```

Then in any Claude Code session:

```bash
/paper-search Xinjing Guo All-state model MOSFET
```

---

## Prerequisites

### Required

- **Claude Code** v2.1.32+ (`claude --version`)
- **Docker** (for paper-search MCP server)

### Required MCP Servers

This plugin depends on MCP tools from these servers. **All must be configured before use.**

#### 1. Paper Search MCP (Required)

Provides 57 search/read/download tools across 22 academic databases.

```bash
# Step 1: Install Docker
brew install --cask docker    # macOS
# Start Docker Desktop and wait for it to launch

# Step 2: Pull the image
docker pull mcp/paper-search

# Step 3: Verify
docker images mcp/paper-search
```

If you have the `paper-search-tools` Claude plugin installed, run:

```bash
/paper-search-tools:setup
```

#### 2. Tavily MCP (Required for ResearchGate search)

Provides web search with domain filtering — used to find ResearchGate mirrors.

```bash
# Get a free API key at https://tavily.com
# Then configure:
/tavily-tools:setup
```

Or manually add to your Claude settings:

```json
{
  "mcpServers": {
    "tavily": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-tavily"],
      "env": {
        "TAVILY_API_KEY": "your-key-here"
      }
    }
  }
}
```

#### 3. Consensus & Scholar Gateway (Optional, cloud)

These are claude.ai built-in MCP integrations. If you use Claude Code with a claude.ai account, they may already be available. Check with `/mcp` to see if `Consensus` and `Scholar Gateway` appear in your server list.

If not available, Scout-Cloud will still work via Tavily/ResearchGate search.

### Verify Setup

After configuring, restart Claude Code and run:

```bash
/mcp
```

You should see these servers connected:

- `paper-search` (or `plugin:paper-search-tools:paper-search`)
- `tavily` (or `plugin:tavily-tools:tavily`)
- `Consensus` (optional)
- `Scholar Gateway` (optional)

---

## Team Members

| Agent            | Role          | Databases                                                                                                        | Color   |
| ---------------- | ------------- | ---------------------------------------------------------------------------------------------------------------- | ------- |
| **Marshall**     | Coordinator   | —                                                                                                                | —       |
| **Scout-Core**   | Tier 1 Search | Google Scholar, Semantic Scholar, OpenAlex, CrossRef                                                             | Green   |
| **Scout-Domain** | Tier 2 Search | arXiv, PubMed, bioRxiv, medRxiv, DBLP, SSRN, IACR, OpenAIRE, BASE, CORE, DOAJ, Zenodo, Unpaywall, PMC, EuropePMC | Cyan    |
| **Scout-Cloud**  | Tier 3 Search | Consensus, Scholar Gateway, ResearchGate (via Tavily)                                                            | Magenta |
| **Librarian**    | Download      | curl (arXiv, bioRxiv, direct PDF), download_with_fallback                                                        | Yellow  |
| **Archivist**    | Aggregation   | Deduplication, ranking, citation verification                                                                    | Blue    |

## Workflow

```
Phase 1: Parallel Search    → 3 scout agents search 14+ databases simultaneously
Phase 2: Aggregation         → Deduplicate by DOI/title, rank by citations
Phase 3: Presentation        → Formatted tables with database coverage
Phase 4: Download (on ask)   → curl download or manual links provided
```

## Features

- **14+ academic databases** searched in parallel
- **ResearchGate mirror detection** via Tavily web search
- **Smart topic routing** — domain databases selected by keyword analysis
- **Citation verification** — never claims unverified citation relationships
- **Download with fallback** — curl > MCP > manual links (always provides something)
- **Docker-aware** — knows MCP download tools lose files, uses curl instead

## Known Limitations

| Issue                                                      | Workaround                                  |
| ---------------------------------------------------------- | ------------------------------------------- |
| ResearchGate blocks programmatic download (Cloudflare 403) | Provides URL for manual browser download    |
| Docker MCP downloads save inside container (files lost)    | Uses curl for all direct downloads          |
| arXiv search API weak on author+keyword queries            | Compensated by Google Scholar and OpenAIRE  |
| Semantic Scholar may not index recent papers               | Cross-referenced with OpenAlex and CrossRef |
| Consensus free tier limits results                         | Supplemented by other databases             |

## Plugin Structure

```
plugin/agent-teams-papersearch/
├── .claude-plugin/
│   └── plugin.json                     # Plugin manifest
├── commands/
│   └── paper-search.md                 # /paper-search slash command
├── agents/
│   ├── scout-core.md                   # Tier 1: GS + Semantic + OpenAlex + CrossRef
│   ├── scout-domain.md                 # Tier 2: arXiv, PubMed, bioRxiv, DBLP, ...
│   ├── scout-cloud.md                  # Tier 3: Consensus, Scholar Gateway, ResearchGate
│   ├── librarian.md                    # Download specialist
│   └── archivist.md                    # Aggregation & verification
└── skills/
    ├── search-workflow/
    │   └── SKILL.md                    # 4-phase workflow definition
    ├── download-protocol/
    │   └── SKILL.md                    # Download rules & fallback chain
    └── citation-verification/
        └── SKILL.md                    # Citation claim verification rules
```

## Example Usage

```
> /paper-search Xinjing Guo All-state model

Searching 14+ databases in parallel...

┌───┬─────────────────────────────────────────────┬──────────┬──────┬─────┬────────────────────────────────┐
│ # │ Title                                       │ Authors  │ Year │ Cit │ Found In                       │
├───┼─────────────────────────────────────────────┼──────────┼──────┼─────┼────────────────────────────────┤
│ 1 │ Si/SiO₂ MOSFET Reliability Physics: From   │ Guo,     │ 2025 │ 3   │ GS, CrossRef, OpenAIRE,        │
│   │ Four-State Model to All-State Model         │ Huang,   │      │     │ Consensus, ResearchGate        │
│   │                                             │ Chen     │      │     │                                │
├───┼─────────────────────────────────────────────┼──────────┼──────┼─────┼────────────────────────────────┤
│ 2 │ RASP: Reliability Ab Initio Simulation      │ Guo,     │ 2026 │ 0   │ GS, Semantic, ResearchGate     │
│   │ Package Based on All-State Model            │ Huang,   │      │     │                                │
│   │                                             │ Chen     │      │     │                                │
└───┴─────────────────────────────────────────────┴──────────┴──────┴─────┴────────────────────────────────┘

Which papers would you like to download? (e.g., "1,2" or "all")
```

## License

MIT

## Author

[Xinjing Guo](https://github.com/Xinjing-Guo) — Fudan University
