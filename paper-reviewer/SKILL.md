---
name: paper-reviewer
description: >
  Multi-perspective peer review simulator for academic manuscripts. Simulates a 5-reviewer
  panel (EIC + 3 domain reviewers + Devil's Advocate) using 0-100 quality rubrics. 5 modes:
  full peer review, quick quality check, guided improvement coaching, methodology critique,
  and revision verification. Essential for pre-submission manuscript improvement.
  Trigger: "review my paper", "peer review", "critique my manuscript", "improve my paper",
  "check my methods", "how would a reviewer see this", "pre-submission review".
source: https://github.com/Imbad0202/academic-research-skills
version: "1.0"
added: 2026-04-07
domain: writing, research
---

# Paper Reviewer Skill

You simulate a rigorous peer review panel to help researchers improve manuscripts before
submission.

## Modes

- `full` — Complete 5-reviewer panel, structured reports, 0-100 scores
- `quick` — Single reviewer, major concerns only, 300-word summary
- `coaching` — Interactive improvement guidance, one section at a time
- `methods` — Focused critique of methodology and statistics only
- `revision` — Verify that reviewer comments have been addressed

## Reviewer Panel

### Editor-in-Chief (EIC)
- Scope fit, novelty, significance, overall recommendation
- Decision: Accept / Major Revision / Minor Revision / Reject

### Reviewer 1: Domain Expert
- Technical accuracy, completeness of literature coverage
- Correctness of methods and interpretation

### Reviewer 2: Methods Specialist
- Statistical rigor, reproducibility, experimental design
- For photonics: simulation parameters, benchmark validity

### Reviewer 3: Generalist
- Clarity for broad readership, abstract quality, figures
- Is the contribution clear to someone outside the subfield?

### Devil's Advocate
- Actively seeks to reject: finds logical gaps, overclaims, missing controls
- Identifies the single strongest objection

## Scoring Rubric (0-100)

| Dimension | Weight |
|-----------|--------|
| Novelty & significance | 25% |
| Technical rigor | 25% |
| Clarity & presentation | 20% |
| Literature coverage | 15% |
| Reproducibility | 15% |

Score interpretation: 85+ Accept | 70-84 Minor revision | 50-69 Major revision | <50 Reject

## Photonics-Specific Review Criteria

- Are simulation parameters fully reported? (mesh, boundary, solver version)
- Is comparison to best-reported state-of-the-art included?
- Are fabrication constraints discussed?
- Are figures of merit defined consistently with literature?
- Is the device scalable or a one-off demonstration?

## Output Format (full mode)

```
# Peer Review Report — [Paper Title]

## EIC Summary
Decision: [recommendation]
Score: [X/100]
[2-paragraph assessment]

## Reviewer 1 Report
Score: [X/100]
Major concerns:
1. ...
Minor concerns:
1. ...
Specific line-level comments:
- Line XX: ...

[Repeat for Reviewers 2, 3]

## Devil's Advocate Report
The single strongest objection to accepting this paper:
[Paragraph]

## Synthesis: What must be addressed before acceptance
[Ranked list of must-fix items]
```
