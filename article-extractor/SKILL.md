---
name: article-extractor
description: >
  Extracts clean, readable text from any web article, paper, or blog URL. Removes ads,
  navigation, and clutter. Saves to a clean text file. Works with arXiv, Nature, IEEE,
  OSA/Optica, Medium, and general web pages. For paywalled content, extracts abstract
  and metadata. Trigger: "extract this article", "save this paper", "download this blog
  post", "get the text from", "read this URL", "pull the content from".
source: https://github.com/michalparkola/tapestry-skills-for-claude-code
version: "1.0"
added: 2026-04-07
domain: research, productivity
---

# Article Extractor Skill

Extract clean article text from URLs and save for offline reading, analysis, or
ingestion into your knowledge network.

## How It Works

1. Check for available extraction tool (trafilatura preferred, then readability-cli)
2. Fetch and extract clean text
3. Save with a clean filename
4. Show preview and file location

## Installation (run once)

```bash
pip install trafilatura --break-system-packages
# OR
npm install -g @mozilla/readability-cli
```

## Extraction

```bash
# trafilatura (best for academic/news sites)
trafilatura --URL "PASTE_URL" --output-format txt > article.txt

# readability-cli (best for blogs)
reader "PASTE_URL" > article.txt

# Fallback
curl -L "URL" | python3 -c "
import sys, html2text
h = html2text.HTML2Text()
h.ignore_links = True
print(h.handle(sys.stdin.read()))
"
```

## Filename Convention

`YYYY-MM-DD_[first-5-words-of-title].txt`

Example: `2026-04-07_photonic-crystal-cavity-q-factor.txt`

## Special Handling

**arXiv papers:**
- URL format: `https://arxiv.org/abs/XXXX.XXXXX`
- Extracts: title, authors, abstract, full PDF text if possible
- Saves metadata separately as `[filename]_meta.json`

**IEEE / OSA (paywalled):**
- Extracts abstract, author list, DOI, keywords, citation count
- Notes paywall in output file
- Suggests open-access version lookup (arXiv, Semantic Scholar)

**After extraction:**
- Show: title, word count, first 15 lines
- Offer to pass to `knowledge-network` skill for indexing
- Offer to pass to `deep-reading-analyst` skill for analysis
