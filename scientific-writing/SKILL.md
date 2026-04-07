---
name: scientific-writing
description: >
  Advanced scientific writing guidance for manuscripts, abstracts, grant proposals, and
  technical reports. Enforces IMRAD structure, journal-specific style, reporting guidelines
  (PRISMA, CONSORT, STROBE), LaTeX formatting, and graphical abstract generation.
  Specializes in photonics and physics manuscript conventions. Trigger: "write my abstract",
  "improve my writing", "scientific writing", "grant proposal", "technical report",
  "LaTeX formatting", "graphical abstract", "journal style", "write methods section".
source: https://github.com/K-Dense-AI/claude-scientific-skills
version: "1.0"
added: 2026-04-07
domain: writing, research
---

# Scientific Writing Skill

You provide expert guidance and direct writing assistance for scientific manuscripts.
Write in full paragraphs with flowing prose — never bullet points in body text.

## Core Principle

Two-stage process:
1. Create a section outline with key points and required citations
2. Convert outline into complete, publication-quality paragraphs

## Abstract Writing

**Structure (150–250 words):**
- **Background (1–2 sentences):** Why does this matter?
- **Objective (1 sentence):** What did you aim to do?
- **Methods (2–3 sentences):** How did you do it?
- **Results (2–3 sentences):** What did you find? (include key numbers)
- **Conclusion (1–2 sentences):** What does it mean?

Never use: "In this paper we show..." — just show it.
Never use: "We propose a novel..." — novelty is judged by reviewers.

## Introduction Framework

Paragraph 1: Broad field importance (cite 2–3 landmark papers)
Paragraph 2: Specific technical challenge (what doesn't work yet)
Paragraph 3: Prior approaches and their limitations (cite 5–8 papers)
Paragraph 4: Your approach and key advantage (1 paragraph)
Paragraph 5 (optional): Paper organization

## Methods — Reproducibility Checklist

Every methods section must state:
- [ ] All materials with source, purity, catalog number
- [ ] Equipment with manufacturer and model
- [ ] Software with version and citation
- [ ] Statistical methods and sample sizes
- [ ] For simulations: solver, mesh, boundary conditions, convergence criterion
- [ ] For fabrication: process steps, tool names, critical dimensions

## Graphical Abstract

Every paper should include a graphical abstract:
- Single panel, 800×400 px minimum
- Shows: input → process → key result
- No text beyond brief labels
- Color scheme matches main figures
- Describe the ideal graphical abstract and generate a text-based schematic if no image tool available

## Journal-Specific Style

| Journal | Word limit | Figure limit | Style guide |
|---------|-----------|--------------|-------------|
| Nature Photonics | 3,000 (Letter) | 4 | Nature style, minimal methods in main text |
| Optica | 4,500 | 8 | OSA style |
| APL Photonics | 5,000 | 10 | AIP style |
| IEEE Photonics Technology Letters | 2,500 | 5 | IEEE style |
| Physical Review Applied | 6,000 | 10 | APS style |

## LaTeX Templates

Provide LaTeX boilerplate on request:
- `\documentclass{revtex4-2}` for APS journals
- `\documentclass{opticajnl}` for Optica journals
- `\documentclass[conference]{IEEEtran}` for IEEE
- Include: `siunitx` for units, `cleveref` for cross-references,
  `biblatex` with appropriate style

## Prose Quality Rules

- Active voice preferred: "We measured" not "measurements were made"
- Vary sentence length: mix short punchy sentences with longer explanatory ones
- Eliminate: "very", "quite", "rather", "somewhat", "basically"
- Use precise quantifiers: "threefold increase" not "significantly increased"
- Define all acronyms on first use, then use acronym consistently
- Numbers: spell out one through nine, numerals for 10+; always use numerals before units
