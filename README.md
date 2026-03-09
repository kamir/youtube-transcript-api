# YT Tools

A growing toolkit for capturing knowledge from YouTube videos -- fetch transcripts, record your thoughts about them, and push everything into your personal knowledge base (ER1).

Built on top of [youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api) by [@jdepoix](https://github.com/jdepoix).

## What's in the box

| Tool | Status | Description |
|------|--------|-------------|
| **Menu Bar App** | available | macOS menu bar app -- fetch transcripts with one click |
| **History Inspector** | available | Web app -- sync your YouTube watch history, browse transcripts, word clouds |
| **Impression Capture** | planned | Record a voice note about a video, bundle both transcripts, push to ER1 |
| **ER1 Integration** | planned | Export video transcripts and impressions to your personal knowledge base |

See the [full documentation](https://kamir.github.io/youtube-transcript-api/) and [ER1 integration requirements](https://kamir.github.io/youtube-transcript-api/requirements-er1-integration).

## Install

**One-liner** (downloads the latest release and installs to `/Applications`):

```bash
curl -fsSL 'https://api.github.com/repos/kamir/youtube-transcript-api/contents/tools/install.sh?ref=kamir/yt-tools' -H 'Accept: application/vnd.github.raw' | bash
```

**From source:**

```bash
git clone https://github.com/kamir/youtube-transcript-api.git
cd youtube-transcript-api
git checkout kamir/yt-tools
tools/build.sh
tools/deploy.sh
```

## Menu Bar App

Fetch transcripts from the macOS menu bar -- no terminal needed.

1. Click the YouTube icon in your menu bar
2. Paste a video URL or ID
3. The transcript is fetched, copied to your clipboard, and stored in history

Features: language fallback with selection dialog, language flags, last 20 transcripts in history, logging to `~/Library/Logs/YTTranscript.log`.

## History Inspector

A web app that syncs your YouTube watch history and fetches transcripts for analysis. Requires [Google OAuth credentials](https://kamir.github.io/youtube-transcript-api/authentication).

```bash
docker compose up        # open http://localhost:8080
```

Features: OAuth login, history sync, timeline view, transcript fetching, word clouds, Google Takeout import.

## Impression Capture (planned)

The idea: you watch a video, then **speak your thoughts** about it. The tool:

1. Fetches the video transcript
2. Records your voice note and transcribes it (Whisper)
3. Bundles both into a composite document:
   - **Video transcript** -- what was said in the video
   - **Your impression** -- what you thought about it
4. Pushes the combined payload into ER1 as a memory entry

This follows the same pattern as [audio-checklist-checker-py](https://github.com/kamir/my-ai-X) -- local MEMORY folder, tagged transcript, ER1 API upload -- but applied to YouTube content instead of raw voice recordings.

## Lifecycle scripts

All scripts live in `tools/`. Run from the repo root.

| Script | What it does |
|--------|-------------|
| `tools/status.sh` | Show install, running, build, log, and history status |
| `tools/pull.sh` | Pull latest changes from remote |
| `tools/build.sh` | Clean build the .app bundle |
| `tools/deploy.sh` | Stop running instance, install to /Applications, launch |
| `tools/update.sh` | **Pull + build + deploy** (one command) |
| `tools/start.sh` | Launch the installed app |
| `tools/stop.sh` | Stop the running app |
| `tools/uninstall.sh` | Remove app, data, and logs |
| `tools/release.sh` | Build + package zip for a GitHub release |
| `tools/install.sh` | Remote install from latest GitHub release |

**Daily workflow** -- pull the latest and redeploy:

```bash
tools/update.sh
```

## Credits

- **[youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api)** -- the Python library that powers transcript fetching
- **[rumps](https://github.com/jaredks/rumps)** -- Ridiculously Uncomplicated macOS Python Statusbar apps
