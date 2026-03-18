---
name: Download Protocol
description: Paper download rules — priority chain, Docker container warning, manual link requirements. Use when downloading or providing paper access links.
version: 1.0.0
---

# Download Protocol

## Critical Warning

Docker-based MCP download tools (`download_arxiv`, `download_biorxiv`, etc.) save files INSIDE the container. The container has NO volume mapping to the host filesystem. **Downloaded files will be LOST.**

**Always use `curl` for direct downloads.**

## Download Priority Chain

| Priority | Source          | Method                                                           | Reliability  |
| -------- | --------------- | ---------------------------------------------------------------- | ------------ |
| 1        | arXiv           | `curl -L -o ~/Downloads/<name>.pdf "https://arxiv.org/pdf/<id>"` | High         |
| 2        | bioRxiv/medRxiv | `curl` from PDF URL                                              | High         |
| 3        | Direct PDF URL  | `curl -L`                                                        | Medium       |
| 4        | DOI fallback    | `download_with_fallback` MCP (tries OA + Sci-Hub)                | Low          |
| 5        | Manual links    | Provide URLs to user                                             | Always works |

## File Naming Convention

`<identifier>_<short-title>.pdf`

Examples:

- `2411.04823_All-State-Model.pdf`
- `10.1038_s41586-024-07386-0_Nature-Paper.pdf`

## Mandatory Post-Download Verification

After every download attempt:

```bash
ls -la ~/Downloads/<filename>.pdf
```

## When Download Fails — Required Output

NEVER just say "download failed." Always provide:

1. arXiv PDF link (if arXiv ID exists)
2. ResearchGate URL (if found by Scout-Cloud)
3. Publisher URL via DOI: `https://doi.org/<DOI>`
4. Sci-Hub mirror: `https://sci-hub.se/<DOI>`

Format as actionable links the user can click in their browser.
