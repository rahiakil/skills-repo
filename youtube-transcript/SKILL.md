---
name: youtube-transcript
description: >
  Fetches and cleans transcripts from YouTube videos. Ideal for ingesting conference
  talks, lecture series, webinars, and technical tutorials on photonics, optics, and
  physics. Falls back to Whisper local transcription if no captions available. Produces
  clean plain-text summaries and key-points extraction after transcription.
  Trigger: "transcribe this video", "get transcript", "YouTube transcript", "summarize
  this talk", "extract captions from".
source: https://github.com/michalparkola/tapestry-skills-for-claude-code
version: "1.0"
added: 2026-04-07
domain: research, productivity
---

# YouTube Transcript Skill

Download and process transcripts from YouTube videos for research ingestion.

## Install (run once)

```bash
pip install yt-dlp --break-system-packages
# For Whisper fallback:
pip install openai-whisper --break-system-packages
```

## Workflow

1. Check subtitle availability: `yt-dlp --list-subs "URL"`
2. Try manual subtitles first (highest quality)
3. Fall back to auto-generated captions
4. Last resort: Whisper transcription (confirm with user — slow)
5. Convert VTT to clean plain text (deduplicate overlapping captions)

## Commands

```bash
# List available subtitles
yt-dlp --list-subs "VIDEO_URL"

# Download manual subtitles
yt-dlp --write-sub --skip-download --output "%(title)s" "VIDEO_URL"

# Download auto-generated (English)
yt-dlp --write-auto-sub --sub-lang en --skip-download --output "%(title)s" "VIDEO_URL"

# Whisper (only with user confirmation)
yt-dlp -x --audio-format mp3 --output "audio.%(ext)s" "VIDEO_URL"
whisper audio.mp3 --model base --output_format vtt
```

## Post-Processing

After downloading, always:
1. Convert VTT → clean plain text (remove timestamps, deduplicate)
2. Show video title, channel, duration, word count
3. Offer: full transcript save OR summary extraction
4. For long talks (>30 min): auto-extract key sections by topic

## After Transcription

Offer to:
- Pass to `deep-reading-analyst` for analysis
- Pass to `knowledge-network` for indexing
- Extract action items or key claims
- Generate a blog-friendly summary
