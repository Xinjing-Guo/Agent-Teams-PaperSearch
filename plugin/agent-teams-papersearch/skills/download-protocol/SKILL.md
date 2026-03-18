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

| Priority | Source                     | Method                                                     | Reliability  |
| -------- | -------------------------- | ---------------------------------------------------------- | ------------ |
| 1        | arXiv                      | `curl -L -o <dir>/<name>.pdf "https://arxiv.org/pdf/<id>"` | High         |
| 2        | bioRxiv/medRxiv            | `curl -L` from PDF URL                                     | High         |
| 3        | MDPI / OA repos            | `curl -L -A "Mozilla/5.0"` from direct PDF URL             | Medium       |
| 4        | Paywalled / login-required | **Open all in browser via Playwright**                     | Always works |

**Do NOT use:** Docker MCP download tools (files lost), Sci-Hub curl (unreliable), ResearchGate curl (Cloudflare 403), IEEE iframe PDF extraction (fragile).

## File Naming Convention

`<##>_<Author><Year>_<Short_Title>.pdf`

Examples:

- `01_Perumal2013_SPICE_Level3_IGZO.pdf`
- `02_Ghittorelli2014_Analytical_IGZO_Model.pdf`

## Mandatory Post-Download Verification

After every curl download, verify the file is a real PDF:

```bash
size=$(stat -f%z "$file")
head_bytes=$(head -c 4 "$file")
# Real PDF: size > 5000 AND head_bytes == "%PDF"
# Otherwise: delete the file, mark as failed
```

## When Programmatic Download Fails — Browser Fallback

**Open ALL failed papers in browser tabs at once** using Playwright `browser_run_code`:

```javascript
async (page) => {
  const urls = [
    /* DOI / IEEE / publisher URLs */
  ];
  const context = page.context();
  for (const url of urls) {
    await context.newPage().then((p) => p.goto(url, { waitUntil: "domcontentloaded", timeout: 15000 }).catch(() => {}));
  }
  return `Opened ${urls.length} tabs`;
};
```

Key rules:

- Open ALL failed papers at once — one tab per paper
- Do NOT try to automate clicking PDF buttons on publisher sites
- Tell user: "Opened N tabs. Please click PDF on each page to download."
- User has institutional access (e.g., Fudan → IEEE) so browser downloads will work
