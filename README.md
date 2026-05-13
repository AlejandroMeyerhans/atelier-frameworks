# atelier-frameworks

> Part of [The Atelier](https://alejandromeyerhans.com/atelier/) by Alejandro Meyerhans

Strategic frameworks for understanding your audience, building brand foundations, capturing voice identity, and making better decisions.

## Voice Pipeline

Three skills that work together as a sequential pipeline to capture and replicate someone's authentic voice:

| Stage | Skill | Description |
|---|---|---|
| 1 | [Sourcing Voice Material](./sourcing-voice-material/) | Discovery-driven curation engine — interviews the user, maps their publishing platforms, and assembles a performance-filtered corpus |
| 2 | [Extracting Voice Profile](./extracting-voice-profile/) | Analyzes the corpus across 14 dimensions to produce a structured voice profile |
| 3 | [Adjusting Voice](./adjusting-voice/) | Two-pass engine that transforms any content to match the voice profile, with progressive calibration. Works best when paired with an avatar from Defining Avatars |

> **Companion skill**: [Defining Avatars](./defining-avatars/) produces audience persona files that Stage 3 uses to calibrate voice output for specific target audiences. The voice stays the same — the calibration gets smarter.

### How They Work Together

```
Defining Avatars (companion)
        │
        ▼
Stage 1: Source → Stage 2: Extract → Stage 3: Adjust
   corpus.md         profile.md          output + wins
```

- **Stage 1 → Stage 2**: The source corpus feeds directly into the extraction engine. Stage 2 can also accept content directly (pasted or via URLs) if you skip Stage 1.
- **Stage 2 → Stage 3**: The voice profile is copied to `adjusting-voice/resources/voice-profile.md`. Stage 3 reads it from there.
- **Defining Avatars → Stage 3**: Avatar dossiers are placed in `adjusting-voice/resources/avatars/`. Stage 3 detects them automatically and offers audience calibration.

### Setup Requirements

**Stage 1** requires Python 3.x with the `youtube-transcript-api` package for programmatic YouTube transcript extraction:

```bash
pip install youtube-transcript-api
```

No other external APIs or tools are required. The entire pipeline runs locally using your AI agent as the execution layer.

## Standalone Skills

| Skill | Description |
|---|---|
| [Defining Avatars](./defining-avatars/) | Builds deep psychographic avatar dossiers through progressive discovery. Standalone for any use, and integrates with the Voice Pipeline (Stage 3) for audience-calibrated voice output |

## Quick Start

1. Download or clone this repository
2. Place the skill folders in your AI agent's skills directory
3. Install the YouTube transcript library: `pip install youtube-transcript-api`

## Requirements

- An AI coding agent (Claude Code, Google Antigravity, Cursor, Windsurf, or similar)
- Python 3.x (for YouTube transcript extraction in Stage 1)

## License

[MIT](./LICENSE)
