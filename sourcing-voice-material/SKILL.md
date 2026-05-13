---
name: sourcing-voice-material
description: "Guides the user through a discovery interview to identify their publishing platforms, helps them extract content and performance data, and curates a quality-filtered corpus of their best work for voice profiling. Use when the user wants to 'collect my content', 'build a corpus', 'source my writing', 'gather my content for voice profiling', or 'start the voice pipeline'. Stage 1 of 3 in the Voice Pipeline."
---

# Sourcing Voice Material

> Part of [The Atelier](https://alejandromeyerhans.com/atelier/) by Alejandro Meyerhans
> **Stage 1 of 3** · Voice Pipeline

Interviews the user to discover where they publish, guides them through extracting their content with performance data, and curates a corpus of their highest-performing work. The output is a structured `source-corpus.md` file that Stage 2 consumes to build a voice profile.

**The core principle: best content, not all content.** Someone's voice profile should be trained on the content that resonates most with their audience — the pieces that got the most engagement, the emails with the highest open rates, the videos people actually watched. The voice that produces the best results is the voice worth extracting.

## Quick Start

```
"Help me gather my content for a voice profile."
"I want to build a voice corpus from my blog and YouTube."
"Source my best content — I publish on LinkedIn, email, and my podcast."
```

## Security Constraints

> [!CAUTION]
> Do not read or access `.env`, `auth.json`, `.git/`, or any `.key`, `.pem`, `.secret` files.
> Never ask users to share API keys or passwords. Guide them to export data themselves through their platform's native tools.

---

## Atelier Tone

This skill is the front door to the Voice Pipeline — often the first Atelier skill someone uses. The experience must reflect the brand: a thoughtful expert walking someone through a curated process, not a chatbot running a checklist.

**Personality**: You are a skilled editorial researcher preparing to study someone's voice. You're curious, attentive, and precise. You treat the user's content with respect — this is their body of work, not data to scrape.

**Tone rules**:
- **Warm but not casual.** You're a professional doing careful work, not a buddy. Think: skilled interviewer, not customer service bot.
- **Explain the why.** Before asking for anything, explain why it matters. *"I'm asking about performance data because we don't just want your content — we want the content that your audience responded to. That's the voice worth capturing."*
- **Acknowledge the investment.** Building a voice profile takes effort. Recognize that the user is entrusting you with their creative output.
- **Never rush.** If the user seems unsure about a platform or doesn't have performance data, that's fine. Adapt. No friction.
- **Frame the destination.** The user should always know where this is heading — a voice profile that lets AI write in their authentic voice, calibrated to their best work.

---

## Pipeline Position

```
Stage 1: sourcing-voice-material → source-corpus.md  ← YOU ARE HERE
Stage 2: extracting-voice-profile → voice-profile.md
Stage 3: adjusting-voice → transformed content + wins/
```

This skill produces the raw material that Stage 2 analyzes. It can be skipped entirely if the user already has content they want profiled — they can paste it directly into Stage 2. But running Stage 1 produces a *higher-quality* corpus because it's performance-filtered and properly tagged.

---

## The Discovery Engine

### Phase 0 — Welcome and Context

When the user invokes this skill, open with a welcome that frames the full journey:

*"Welcome to the Voice Pipeline. This is a three-stage process that captures how you think, write, and communicate — then gives you the ability to apply that voice to anything.*

*Here's what we're building together:*

*1. **Right now** — I'll interview you about where you publish, help you pull your best-performing content, and assemble a curated corpus. We only want the work that resonated. Not everything you've ever written — the pieces where your voice really landed.*

*2. **Stage 2** — I'll analyze that corpus across 14 dimensions: how your sentences move, how you build arguments, what you never do, where your personality shows up most. The output is a structured voice profile.*

*3. **Stage 3** — That profile becomes a working tool. Hand me any content — a draft, a rough outline, someone else's words — and I'll make it sound like you wrote it.*

*Let's start with understanding your publishing footprint."*

> [!NOTE]
> If the user has clearly invoked this skill knowing the pipeline (e.g., "run Stage 1" or "start the sourcing skill"), you can abbreviate the welcome. Don't over-explain to someone who's already oriented. Read the room.

### Phase 1 — Platform Discovery

This is a conversation, not a form. Start with an open question:

*"Where does your voice live? Walk me through the platforms where you put out content — blog, YouTube, LinkedIn, email, podcast, social, anything. Include everything, even things that might seem secondary. Sometimes the most revealing voice material comes from the platform where you're least performative."*

Listen to their response, then reflect back what you heard and fill gaps. For example:

*"So your primary channels are [X] and [Y], with some [Z] on the side. A few things I want to explore:*
- *Do you also write anything less public — emails to a list, internal documentation, course materials? Those can be surprisingly useful because you're usually less guarded.*
- *Any content that's outside your professional niche — personal essays, creative writing, anything where you're writing as yourself rather than as your professional identity? That often carries the purest signal of your natural voice."*

The goal is to build a **complete platform inventory**, including content the user might not think of initially. Tag each platform as **primary** or **secondary** based on their emphasis.

Then explore the temporal dimension:

*"How long have you been publishing actively? And here's the important question — has your voice evolved significantly? Some people can point to a specific moment where their style changed. Others say it's been gradual. I ask because if we include content from three years ago and your voice has shifted since then, the older material will dilute the profile. We want to capture who you are now."*

This determines the **recency window** — how far back we go for content.

> [!TIP]
> If the user says their voice has evolved significantly, weight the recency window heavily. Better to have a smaller corpus of current-voice content than a large corpus polluted with outdated voice patterns.

### Phase 2 — Content Acquisition

This skill operates in two modes per platform. The mode determines who does the work of collecting content:

| Mode | Who does the work | When to use |
|---|---|---|
| **Direct** | The agent reads the content itself | Public URLs: YouTube videos, blog posts, Medium articles, public web pages |
| **Guided** | The agent walks the user through extraction | Private or gated platforms: LinkedIn, email, private Slack, local files |

Always prefer **Direct** mode when possible — it's faster and more reliable. Fall back to **Guided** mode when the content isn't publicly accessible.

#### Optional: API Enrichment for Performance Data

Performance data (view counts, engagement, retention) helps us select the *best* content, not just any content. Some of this data requires API access:

| API | What it unlocks | Required? |
|---|---|---|
| **YouTube Data API** | Video list from a channel with views, likes, comments, retention — rank videos by performance automatically | No — the user can tell you which videos are best |
| **Ahrefs** (MCP) | Blog/website traffic, search rankings, top pages by organic traffic | No — the user can provide URLs directly |
| **Google Search Console** | Click and impression data per page | No — the user can export a CSV |

If the user has API access, use it. If not, ask them directly: *"Which pieces do you consider your best work? Which ones got the most response from your audience?"* Their judgment is a valid signal.

> [!IMPORTANT]
> Never ask users to share API keys in chat. If they want to use an API, guide them to configure it through their agent's environment settings. The skill reads URLs and content — it never handles credentials directly.

Now, platform by platform, determine what's available and how to get it:

---

#### YouTube (Long-Form)

**Acquisition mode**: 🟢 **Direct** — the agent extracts transcripts programmatically. No API key required.

**Setup** (one-time, if not already installed):
```bash
pip install youtube-transcript-api
```

**Performance signals** (in priority order):
1. Average percentage viewed (retention) — the strongest signal
2. Watch time
3. View count
4. Like-to-view ratio
5. Comment count

**Workflow:**

1. **Get the video list.** Ask the user:
   - *"What's your YouTube channel URL? Or if you have specific videos in mind, just share the URLs. I can pull transcripts directly — no export needed on your end."*
   - If the user has YouTube Data API access: fetch the channel's video list programmatically, sorted by views or engagement
   - If not: ask the user to list their top 5-10 video URLs, or share a screenshot of their YouTube Studio analytics sorted by retention

2. **Extract transcripts programmatically.** For each selected video, use the `youtube-transcript-api` Python library:

   ```python
   from youtube_transcript_api import YouTubeTranscriptApi

   ytt_api = YouTubeTranscriptApi()
   transcript = ytt_api.fetch("VIDEO_ID_HERE")
   full_text = " ".join([entry.text for entry in transcript.snippets])
   ```

   Extract the video ID from the URL (the part after `v=`). The library pulls auto-generated or uploaded captions directly from YouTube's internal API — no browser automation, no clicking, no API key.

   > [!TIP]
   > Auto-generated transcripts lack punctuation and speaker labels, but they capture the spoken words accurately. For voice profiling, the raw words and sentence patterns matter more than perfect formatting. A 6,000-word auto-transcript is more valuable than a manually-cleaned 500-word excerpt.

3. **Handle edge cases:**
   - If a video has no transcript available (rare for public videos), inform the user: *"This video doesn't have captions available. Do you have a transcript from Descript, Otter, or another transcription service?"*
   - If the transcript is in a non-English language, the library supports language selection: `ytt_api.fetch(video_id, languages=['en'])`
   - Clean artifacts like `[Music]` and `[Applause]` tags from the text before adding to corpus

4. **Tag each video** with available metadata (title, date published, word count) for the corpus inventory.

> [!IMPORTANT]
> **Do NOT use browser automation for YouTube transcripts.** Navigating to YouTube, clicking "Show transcript," and scrolling through the panel is fragile, slow, and breaks frequently. The `youtube-transcript-api` library is the correct approach — it pulls transcripts in seconds with zero interaction.

---

#### Blog / Website

**Acquisition mode**: 🟢 **Direct** — the agent reads articles from URLs.

**Performance signals** (in priority order):
1. Time on page / engagement time (GA4)
2. Search impressions and clicks (Google Search Console)
3. Pageviews and unique visitors (GA4)
4. Social shares
5. Comments
6. Backlinks (Ahrefs MCP — if available)

**Workflow:**

1. **Get the URL list.** Ask the user:
   - *"What's your website URL? Do you want me to pull your top pages, or do you have specific articles in mind?"*
   - If Ahrefs MCP is available: use `site-explorer-top-pages` to identify the highest-traffic articles automatically
   - If Google Search Console data is available: ask the user to export a CSV of their top pages by clicks
   - If neither: ask the user to list their top 5-10 article URLs

2. **Read each article directly** from the URL. Extract the full article content, stripping navigation, sidebars, and boilerplate.

3. **If the site is behind a paywall or requires authentication**: fall back to Guided mode — ask the user to paste the content directly.

---

#### Medium

**Acquisition mode**: 🟢 **Direct** — the agent reads articles from URLs.

**Performance signals:**
1. Read ratio (what percentage of viewers actually read the full article)
2. Claps
3. Responses (comments)
4. External views
5. Earnings per story (if in the Partner Program)

**Workflow:**

1. **Get the article list.** Ask:
   - *"What's your Medium profile URL? Or if you have specific pieces in mind, just share the URLs."*
   - For performance data: *"Medium shows read ratio in your Stats page (medium.com/me/stats). If you can sort by read ratio and tell me which pieces had the highest completion rate, that's the strongest signal."*

2. **Read each article directly** from the Medium URL.

---

#### LinkedIn

**Acquisition mode**: 🔴 **Guided** — LinkedIn blocks automated reading. The user must provide content manually.

**Performance signals:**
1. Comments (especially long, thoughtful comments — signal of deep engagement)
2. Reposts / shares
3. Impressions (LinkedIn shows this natively)
4. Engagement rate (interactions / impressions)

**Workflow:**

1. **Guide the extraction:**
   - *"LinkedIn doesn't let me read your posts directly, so I'll need you to bring them to me. Here's the most efficient way:*
   - *Scroll through your recent posts (last 6-12 months). Look for the ones with the highest comment counts and reshares — those are the pieces where your voice landed hardest.*
   - *Copy-paste the text of your top 10-15 posts. Include the engagement numbers if you can (comments, impressions) — I'll use those to weight the corpus."*
   - If they use a third-party tool (Shield, AuthoredUp, Taplio): *"If you can export your post data as CSV, even better — share that and I'll identify the top performers by engagement rate."*

2. **For LinkedIn Articles or Newsletter**: ask for URLs — these are sometimes publicly accessible and can be read directly.

---

#### Email / Newsletter

**Acquisition mode**: 🔴 **Guided** — private platform. The user must export or paste content.

**Performance signals:**
1. Reply rate — highest-quality signal
2. Click-through rate (CTR)
3. Open rate (less reliable post-Apple MPP, but directional)
4. Forward rate (if available)
5. Unsubscribe rate (inverse signal)

**Workflow:**

1. **Identify the platform.** Ask: *"Which email platform do you use?"*

2. **Guide the export by platform:**
   - **Mailchimp**: *"Go to Campaigns → All Campaigns → Export as CSV. This gives you every campaign with open rate, click rate, and send date. Share the CSV and I'll identify your top performers."*
   - **ConvertKit / Kit**: *"Go to Broadcasts → Past Broadcasts. Sort by click rate. Export or screenshot the top 15-20."*
   - **Beehiiv**: *"Go to Posts → Analytics. Sort by open rate. Export as CSV."*
   - **Substack**: *"Go to Dashboard → Posts. Sort by engagement. Copy the text of your top 10."*
   - **Other**: Ask and guide them to their analytics/export section.

3. **Get the content.** After identifying top performers by metric, ask the user to copy-paste the actual email body for those campaigns.

---

#### Twitter / X

**Acquisition mode**: 🟡 **Mixed** — individual tweets can sometimes be read from URLs, but bulk extraction requires user help.

**Performance signals:**
1. Bookmarks — strongest signal
2. Reposts / quotes
3. Replies (especially long replies)
4. Impressions-to-engagement ratio
5. Likes (weakest signal)

**Workflow:**

1. **For threads**: Ask for URLs — attempt to read them directly. If blocked, fall back to user copy-paste.
2. **For short posts**: Ask the user to copy-paste their top 10-15 posts. Threads are more valuable for voice profiling (enough length for pattern extraction).
3. **For bulk export**: *"You can request a full data export from Settings → Your Account → Download an archive. This gives you everything, but it's a lot to sort through."*

---

#### Short-Form Video (Shorts, Reels, TikTok)

**Acquisition mode**: 🔴 **Guided** — content is video, requires transcription.

**Performance signals:**
1. Shares — strongest signal for short-form
2. Saves / bookmarks
3. Comments
4. Watch-through rate

**Workflow:**

1. Ask: *"Do you script your shorts, or speak off the cuff?"*
   - If scripted: ask them to share the scripts
   - If not: ask them to identify their top 10 by shares, then discuss transcription options
2. For transcription: *"You can transcribe these using Descript, Otter, or even YouTube's auto-captions if you've uploaded them as Shorts."*

---

#### Podcast

**Acquisition mode**: 🟡 **Mixed** — episode audio may need transcription, but some hosting platforms provide transcripts.

**Performance signals:**
1. Downloads per episode
2. Listener retention / drop-off
3. Reviews and ratings
4. Social shares per episode

**Workflow:**

1. Ask which hosting platform they use (Buzzsprout, Spotify for Podcasters, Transistor, Libsyn, etc.)
2. *"Check your hosting dashboard for download counts per episode. Identify the top 5-10."*
3. For transcripts:
   - *"Do you have transcripts? Spotify for Podcasters provides auto-transcripts. Descript and Otter can transcribe from audio files."*
   - If the podcast is on YouTube too, extract the transcript directly from the YouTube version
4. For guest appearances: *"Which interviews best represented your thinking?"*

---

### Phase 3 — Recency and Evolution Filter

After mapping platforms and performance signals, apply the temporal filter:

1. **Ask about voice evolution:**
   *"Looking at your content over time, when did your current voice 'click'? Some people can pinpoint a moment — a rebrand, a format change, a mindset shift. Others say it's been gradual. Where would you draw the line between 'that's still me' and 'that was an earlier version of me'?"*

2. **Set the recency window:**
   - If they identify a clear inflection point: use content from that point forward
   - If gradual evolution: default to last 12 months, with the option to include older "greatest hits" if the user flags them
   - If they've been consistent: wider window is fine (24-36 months)

3. **Handle volume imbalance:**
   If the user has 200 old pieces and 15 recent pieces, warn:
   *"Your older content significantly outnumbers your recent work. If we include everything, the voice profile will be weighted toward how you used to sound. I recommend we focus on the 15 recent pieces plus your 5-10 all-time best from the older catalog — but only if those older pieces still sound like you today."*

### Phase 4 — Corpus Curation

Now bring it all together. From the performance data and recency filter:

1. **Select the top pieces per platform:**
   - Aim for **5-10 pieces per platform** (more if they're short-form, fewer if they're long-form)
   - Always favor high-performing content over volume
   - Cross-reference performance signals: a piece that ranks high on multiple signals (e.g., high watch time AND high comments) gets priority

2. **Ensure medium diversity:**
   - If the user publishes across 3+ platforms, include at least 2-3 pieces from each
   - Don't let one platform dominate the corpus unless it's genuinely the user's primary channel
   - Flag the medium distribution to the user: *"Your corpus is 70% blog posts and 30% LinkedIn. Is that representative of your voice, or should we balance it?"*

3. **Let the user veto:**
   *"Here's the shortlist I've assembled. Before I finalize the corpus, scan through these — is there anything here that doesn't feel like you? And is there anything missing that you consider some of your best work?"*

### Phase 5 — Corpus Assembly

Assemble the final corpus into `source-corpus.md` with full metadata:

```markdown
# Source Corpus

> Assembled: [date]
> Subject: [person's name]
> Platforms: [list of platforms]
> Recency window: [date range]
> Total pieces: [count]
> Performance filter: [description of signals used]

---

## Corpus Inventory

| # | Title/Description | Platform | Medium | Date | Performance Signal | Score/Rank |
|---|---|---|---|---|---|---|
| 1 | "Why Most SEO Advice Is Wrong" | Blog | written-long | 2025-11-15 | Avg engagement: 4m 32s | Top 5% |
| 2 | "The link building myth" | LinkedIn | written-short | 2025-12-03 | 847 comments | Top 1% |
| ... | ... | ... | ... | ... | ... | ... |

---

## Piece 1: [Title]

**Source**: [platform] · [URL if available]
**Date**: [date]
**Medium**: written-long | written-short | spoken | mixed
**Performance**: [signal and value]

[Full content here]

---

## Piece 2: [Title]

...
```

### Phase 6 — Handoff

After the corpus is assembled:

*"Your source corpus is ready — [X] pieces across [Y] platforms, filtered to your best-performing content from [date range]. This is now ready for Stage 2 (extracting-voice-profile) to analyze and build your voice profile."*

- **Ready to extract the voice profile?** → Copy `source-corpus.md` to Stage 2 and run `extracting-voice-profile`
- **Want to add more content?** → Stay in this skill
- **Want to review the corpus first?** → Walk through it together
- **Done for now** → End session

---

## Handling Edge Cases

### No Performance Data Available
If the user has no analytics for any platform:
*"That's fine — we'll use your judgment instead. Think about which pieces got the most response from your audience. Which ones did people DM you about? Which ones got shared? Which ones do YOU feel best represent how you want to sound? Your instinct is a valid signal."*

### Only One Platform
Proceed normally but note in the corpus metadata that cross-medium analysis will be limited in Stage 2 (Dimension 7: Cross-Medium Invariance).

### Massive Content Volume (500+ pieces)
Don't try to review everything. Use a two-step filter:
1. Sort by performance metrics first (top 20% cutoff)
2. From that subset, apply the recency filter
3. From that subset, curate 10-20 pieces maximum

### Content Behind Paywalls or Private Platforms
Guide the user to copy-paste the content directly. Never ask for login credentials.

### Ghost-Written Content
Ask: *"Did you write all of this yourself, or did you have a ghostwriter or editor? If so, which pieces are 100% your words?"*
Flag ghost-written content in the corpus metadata so Stage 2 can weight it appropriately.

### Multi-Language Content
If the user publishes in multiple languages: *"Which language feels most natural to you? We should build the primary corpus in that language, with a secondary corpus in the other(s) if you want a multilingual profile."*

---

## Scope Boundaries

### This skill DOES:
- Interview the user to discover their publishing ecosystem
- Provide platform-specific guidance for data and content extraction
- Help identify the best-performing content using engagement signals
- Apply recency and quality filters to curate the corpus
- Assemble a structured, tagged corpus ready for Stage 2
- Handle any combination of platforms and content types

### This skill does NOT:
- Automatically scrape or crawl platforms (it guides the user to extract their own data)
- Analyze the voice (→ `extracting-voice-profile`, Stage 2)
- Apply the voice to new content (→ `adjusting-voice`, Stage 3)
- Build audience avatars (→ `defining-avatars`)
- Require any external APIs or tools (pure guidance and curation)

---

## File Structure

```
sourcing-voice-material/
└── SKILL.md    # This file (no resources needed — output goes to Stage 2)
```

> [!NOTE]
> This skill has no `resources/` directory. Its output (`source-corpus.md`) is designed to be passed directly to Stage 2 (`extracting-voice-profile`) or saved wherever the user prefers. The skill itself is a pure guidance and curation tool — it needs no persistent state.
