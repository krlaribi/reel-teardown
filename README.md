# reel-teardown

A Claude Code skill that takes any short video (a reel, a TikTok, a YouTube Short, an ad) and tells you **why it works**:
the hook, every cut, the pacing, the on-screen text, the script and the ending. Everything is measured from the frames
and the transcript, with timecodes, not guessed.

Paste a competitor's reel and ask *"why does this perform?"* You get a breakdown you can act on, ending in
**3–5 moves to steal tomorrow**.

<p align="center"><img src="examples/quartz/sheet-00-13s.jpg" width="640" alt="Contact sheet: the first 13 seconds of a reel, one frame every 0.33 s with timecodes"></p>
<p align="center"><sub>What Claude reads: a frame every 0.33 s, time printed on each. Example: <a href="examples/quartz/BREAKDOWN.md">full teardown of my reel <i>Quartz</i></a>.</sub></p>

## What you get
For each video, a study folder with:
- `sheets/`: contact sheets, a frame every 0.33 s, so no cut is missed
- `transcript.txt`: every word with its timestamp
- `stats.txt`: duration, shot count, average and longest shot, words per second, what happens in the first 3 s
- `BREAKDOWN.md`: Claude's teardown, covering the hook (0–3 s), beat by beat, what keeps people watching, the script, the ending, **steal this**, don't copy

See [examples/quartz/BREAKDOWN.md](examples/quartz/BREAKDOWN.md) for a real one.

## What you need
- **[Claude Code](https://claude.com/claude-code)**, to run the skill.
- **[uv](https://docs.astral.sh/uv/)**, a free installer. One line in the Terminal:
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
  uv fetches everything else by itself the first time you run a teardown: ffmpeg to read the video,
  Whisper for the transcript, yt-dlp to download links. There's nothing else to install.

You don't need Remotion, After Effects or any editing app. The skill reads any video file, whatever made it.

**Getting the video**
- **YouTube, TikTok and most sites:** paste the link. Claude downloads it.
- **Instagram:** paste the link and try. If Instagram asks for a login, save the reel yourself: screen-record it on your phone
  (iPhone: Control Centre → Screen Recording; Android: Quick Settings → Screen record), trim it, AirDrop or send it to your computer,
  and give Claude the file. For your own reels, the original files are in Instagram → Settings → Accounts Center → Your information and permissions → Download your information.

## Install
```bash
git clone https://github.com/krlaribi/reel-teardown
cp -r reel-teardown/skills/reel-teardown ~/.claude/skills/
```
Never used git? Click the green **Code** button on this page → **Download ZIP**, unzip it, and copy the
`skills/reel-teardown` folder into `.claude/skills/` in your home folder (create it if it isn't there).
Or ask Claude Code: *"Install the skill from github.com/krlaribi/reel-teardown."*

## Use
In Claude Code:

> Tear down this reel: https://www.youtube.com/shorts/…

> Why does this ad work? ~/Downloads/competitor-ad.mp4

> Compare my reel out/v3.mp4 with this one and tell me the three biggest differences.

If a link won't download, see [Getting the video](#what-you-need) above.

Prefer no Claude? The measuring script runs on its own:
```bash
uv run --with pillow --with imageio-ffmpeg --with faster-whisper python skills/reel-teardown/scripts/teardown.py study/ video.mp4
```

## Fair use
Study videos to learn from them. Don't republish other people's videos or frames.

## Why I built it
I'm a marketer. About a third of my Claude Code sessions started with "study this reel." This skill is that habit, made repeatable.
More tools: [reel-kit](https://github.com/krlaribi/reel-kit). Reels: [@anatomyofideass](https://www.instagram.com/anatomyofideass/).

## Licence
MIT. See [LICENSE](LICENSE).
