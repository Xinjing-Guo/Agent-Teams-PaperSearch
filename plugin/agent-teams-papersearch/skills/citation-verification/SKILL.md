---
name: Citation Verification
description: Rules for verifying citation relationships between papers. Prevents false citation claims from search co-occurrence.
version: 1.0.0
---

# Citation Verification Protocol

## The Problem

When searching multiple databases, papers on the same topic often appear together in results. This creates a false impression that they cite each other. **Search co-occurrence does NOT imply citation.**

## Rules

1. **NEVER** claim "Paper A cites Paper B" based solely on:
   - Appearing in the same search results
   - Being by related authors
   - Being on the same topic
   - One being newer than the other

2. **To verify a citation**, you MUST do one of:
   - Use `read_<source>_paper` to access the citing paper's reference list
   - Use Semantic Scholar's citation API to check the citation graph
   - Find explicit mention of the cited paper's DOI/title in the citing paper's text

3. **Acceptable phrasing when unverified:**
   - "Related work by the same group"
   - "Paper on a similar topic"
   - "Potentially citing (not verified)"

4. **Only use these phrases when verified:**
   - "Cites [Paper X]"
   - "Cited by [Paper Y]"
   - "References [Paper Z]"
