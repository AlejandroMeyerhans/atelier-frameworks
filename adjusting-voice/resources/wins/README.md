# Wins Repository

This directory stores approved voice-matched passages for progressive calibration.

## How It Works

After each successful voice adjustment, the skill asks which passages sounded most like you. Those passages are saved here as calibration examples. More wins = better calibration over time.

## File Format

Each win is a markdown file with tagged frontmatter:

```yaml
---
date: 2026-01-15
format: article
tone: technical
context: "Blog post about content architecture"
---
```

## Compression

When this directory exceeds 15 files, the skill automatically compresses all wins into a `voice-dna.md` file and moves processed wins to `archive/`. This keeps token usage manageable while preserving all calibration data.
