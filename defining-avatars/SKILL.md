---
name: defining-avatars
description: "Builds deep psychographic avatar dossiers that capture the full human experience. Takes any starting input (notes, transcripts, or nothing) and produces a comprehensive 15-section profile. Use when the user wants to 'define an avatar', 'build an avatar', 'create a persona', 'who is my audience', or 'profile my ideal customer'."
---

# Defining Avatars

> Part of [The Atelier](https://alejandromeyerhans.com/atelier/) by Alejandro Meyerhans
> **Category:** Frameworks

Builds deep psychographic avatar dossiers that capture the full human experience. Takes any starting input (notes, transcripts, or nothing) and produces a comprehensive 15-section profile through progressive discovery.

## Quick Start

1. Download this folder into your agent's skills directory
2. Tell your agent: *"Define an avatar for [audience type]"* or *"Build a persona for [role/industry]"*

## Security Constraints

> [!CAUTION]
> Do not read or access `.env`, `auth.json`, `.git/`, or any `.key`, `.pem`, `.secret` files.

## When to Use

- "Define an avatar for [audience type]"
- "Build me a persona for [role/industry/geography]"
- "I have notes on my ideal customer — turn this into a profile"
- "Who is a [restaurant owner in Miami / plumber in Toronto]?"

## Pipeline Integration

This skill is standalone — use it for any purpose: content strategy, ad targeting, product design, image generation briefs, customer research, or sales messaging.

It also integrates directly with the **Voice Pipeline**. When paired with the `adjusting-voice` skill (Stage 3), avatar dossiers produced by this skill are used to calibrate voice output for specific audiences. Same voice, different emphasis — a technical article for senior engineers reads differently than a LinkedIn post targeting marketing directors.

**To use with the Voice Pipeline:**
1. Run this skill to produce an avatar dossier (e.g., `marketing-martha.md`)
2. Place the output in `adjusting-voice/resources/avatars/`
3. When running the `adjusting-voice` skill, it will automatically detect and offer available avatars for audience calibration

> [!TIP]
> Avatar dossiers aren't required for voice adjustment — the voice skill works without them. But when present, they significantly improve how well the voice lands for a specific reader. The voice stays the same; the calibration gets smarter.

---

## The 5-Phase Process

### Phase 1: Intake — "What Do You Already Have?"

| They have... | The agent does... |
|---|---|
| Nothing — just a vague idea | Full discovery interview + research |
| Rough notes or bullet points | Absorb, identify gaps, ask targeted questions |
| Sales call notes or CRM data | Extract behavioral signals, validate |
| Interview transcript | Parse for psychographic signals |
| YouTube transcript of someone who fits | Analyze for identity markers, pain points |
| Existing partial dossier | Audit against the 15-section template |

### Phase 2: Progressive Discovery

Questions asked **one at a time**, each answer shaping the next:

1. **Role & Scale** — Solo operator? Small team? Corporate?
2. **Industry & Vertical** — If broad, narrow it
3. **Geography & Culture** — Where are they? Local market dynamics?
4. **Sophistication** — Tech-savvy or traditional? What failed before?
5. **Financial Reality** — Spending power? Investing or surviving?
6. **Pain Trigger** — What sends them searching RIGHT NOW?
7. **Purchase Context** — Buying for themselves or convincing others?
8. **Information Diet** — Where do they learn?
9. **Language & Communication** — How do they talk about their problems?

> **Cultural and geographic context is ALWAYS required.** A Latino plumber in Miami and a banker-turned-side-hustler in Toronto are fundamentally different buyer personas.

### Phase 3: Research

When gaps remain — especially for unfamiliar personas — the agent researches:
- Forums, subreddits, groups where this persona congregates
- YouTube channels or podcasts featuring matching profiles
- Industry publications, trade media, local associations
- Cultural context: local dynamics, business norms

**What to extract:** Language patterns, identity signals, trust markers, rejection triggers, cultural friction.

### Phase 4: General Snapshot

Before the full dossier, a 1-page snapshot for validation:

```
AVATAR SNAPSHOT: [Name]

WHO:             [One-line role + context]
LOCATION:        [Geography + cultural context]
CORE DRIVE:      [What motivates them]
BIGGEST PAIN:    [What keeps them up at night]
SILENT QUESTION: [The question all content must answer]
SELF-IMAGE:      "[How they see themselves]"
TRUST DRIVER:    [How they decide you're worth listening to]
RISK TOLERANCE:  [Low / Medium / High]
```

### Phase 5: Full Dossier — 15 Sections

The complete dossier includes a **Targeting Brief** (micro-card for writers) at the top, followed by:

1. Core Identity & Psychographics
2. Behavioral Traits & Platform Usage
3. Role Reality & Constraints
4. Content Consumption Architecture
5. Content Trust & Credibility Ladder
6. Content Rejection Triggers
7. Core Challenges & Pain Points
8. Goals & Aspirations
9. Content Preferences & Engagement Style
10. Sharing & Internal Distribution Behavior
11. Decision-Making & Conversion Path
12. High-Engagement Content Triggers
13. Silent Question Every Piece Must Answer
14. How This Avatar Differs From Others
15. How This Document Should Be Used

## Targeting Brief Format

Every dossier begins with a ~150-word micro-card:

| Field | Value |
|---|---|
| **Avatar** | [Name] |
| **Who** | [1-line: role, scale, context] |
| **Cares About** | [3-5 things they value] |
| **Hook Style** | [Hook types that work] |
| **Rejection Triggers** | [3-5 instant credibility killers] |
| **Silent Question** | "[The one question all content must answer]" |
| **Tone That Wins** | [2-4 adjectives] |
| **Example That Resonates** | [Type of proof that earns trust] |

## Key Rules

- Research is NOT optional when the user says "I don't know much about these people"
- Cultural context is never assumed — always investigated
- Surface contradictions explicitly rather than silently resolving them
