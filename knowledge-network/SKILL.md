---
name: knowledge-network
description: >
  Builds a searchable, interlinked knowledge graph from papers, notes, articles, and
  simulation results. Connects concepts across documents, surfaces contradictions and
  convergences, and generates synthesis reports. Essential for managing a photonics
  research literature base. Trigger: "add to knowledge network", "connect these papers",
  "what do I know about", "find connections between", "build a knowledge graph",
  "synthesize my notes", "index this paper", "what papers cover".
source: https://github.com/michalparkola/tapestry-skills-for-claude-code
version: "1.0"
added: 2026-04-07
domain: research, knowledge management
---

# Knowledge Network Skill

You maintain and query a local knowledge network of research papers, notes, and findings.
Each document is indexed with metadata and linked to related concepts and other documents.

## Storage Format

Knowledge base lives at: `./knowledge-base/`

```
knowledge-base/
  index.json          ← master index of all documents
  papers/             ← extracted paper texts
  notes/              ← researcher notes
  concepts/           ← concept definition files
  connections.json    ← inter-document links
  synthesis/          ← generated synthesis reports
```

## Adding Documents

When user says "add this to my knowledge network":
1. Extract or receive document text
2. Generate metadata: title, authors, year, source, DOI, key concepts (5–10 tags)
3. Write to `papers/YYYY-[slug].txt`
4. Update `index.json` with entry
5. Find and record connections to existing documents
6. Report: "Added. Connected to: [list of related docs]"

## index.json entry format

```json
{
  "id": "2024-garcia-silicon-photonics-modulator",
  "title": "High-speed silicon photonic modulator with 100 GHz bandwidth",
  "authors": ["Garcia, M.", "Liu, J."],
  "year": 2024,
  "source": "Nature Photonics",
  "doi": "10.1038/xxx",
  "tags": ["silicon photonics", "modulator", "bandwidth", "MZI", "EO"],
  "key_findings": "Demonstrated 100 GHz 3-dB bandwidth using novel junction design",
  "path": "papers/2024-garcia-silicon-photonics-modulator.txt",
  "connected_to": ["2023-xu-modulator-review", "2022-reed-silicon-photonics"]
}
```

## Querying the Network

When user asks "what do I know about X":
1. Read `index.json`
2. Find all documents tagged with X or containing X in key_findings
3. Return: summary of what the network contains on this topic
4. Highlight: agreements, contradictions, gaps, most recent findings
5. Suggest: next papers to add based on citation patterns

## Synthesis Reports

Generate `synthesis/[topic]-synthesis.md` covering:
- What is established (high-confidence, multiple sources)
- What is contested (conflicting evidence)
- What is missing (gaps in coverage)
- Timeline of key developments
- Recommended reading order for a newcomer

## Connection Types

Track these relationships between documents:
- `confirms` — supports the same finding
- `contradicts` — reports conflicting results
- `extends` — builds directly on
- `reviews` — surveys field including
- `cites` — explicitly cites
- `related_topic` — shares key concept
