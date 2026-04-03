# Companion — Ambient Desktop Bot

A voice-first AI companion with expressive animated eyes, ambient particles, and a human-like personality. Built as a single `index.html` file — no dependencies, no build step.

---

## Quick Start

1. Open `index.html` in a browser (or serve it locally)
2. Select a mood on the mood picker
3. Open settings (gear icon, top-right) and enter your API key
4. Tap the mic button (bottom-right) to start talking

---

## Features

### Voice Interaction (Mic Button)
- Small mic button at **bottom-right** — tap to toggle on/off
- **Continuous listening** — stays on between sentences, no need to tap repeatedly
- Speak naturally and the bot responds via voice (TTS)
- During TTS playback, mic **auto-pauses** to avoid feedback, then **auto-resumes**
- Interim transcript shown faintly while you speak

### Soft Female Voice (TTS)
- Auto-selects the best soft female voice available on your system
- Tries: Samantha, Karen, Moira, Tessa, Zoe (macOS/iOS), Google Female (Chrome), Microsoft Zira (Windows)
- Tuned for comfort: slower rate (0.92), slightly higher pitch (1.08), moderate volume (0.85)

### Human-Like Persona
- Talks like a close friend, not an assistant
- Casual, warm, honest — like a late-night conversation
- Short responses (1-2 sentences usually)
- Matches your energy — playful when you're playful, gentle when you're heavy
- Has opinions, disagrees gently sometimes
- If you're venting, it just listens instead of trying to fix everything
- Never breaks character, never says "As an AI"

### Animated Eyes (SVG)
- Fully procedural SVG eyes with iris, pupil, highlights, and lids
- **Idle behaviors** — blink, roam, saccade, lid twitch, eye roll, suspicious squint, cross-eyed, wink, surprised, dizzy, sleepy droop, happy squint, look-around, startle, dash, peek, bounce, slow creep
- **Eye states**: idle, thinking (looking around), speaking (looking at user), listening (widened, dilated)
- **Volume-reactive** when mic is on — pupils and eyes scale with voice volume

### Tap Reactions
- **Single tap** on an eye — squish + elastic bounce back + ripple effect
- **Double tap** — surprised reaction (eyes widen, pupils shrink, quick look around)
- **Long press (hold)** — slow affectionate blink

### Ambient Particles
- 40 soft glowing dots floating on a canvas behind the eyes
- Sine-wave drift motion, brighter near center, fading at edges
- Color matches the current mood
- Dims during emotion overlays

### Emotion Detection
Detects emotions from keywords in conversation and triggers visual reactions:

| Emotion | Visual Effect |
|---------|--------------|
| Sad | Droopy eyes, blue glow, falling tears |
| Happy | Squint eyes, dilated pupils, sparkles |
| Love | Heart-shaped pupils, floating hearts, pink glow |
| Angry | Narrow eyes, small pupils, shake, red glow |
| Scared | Wide eyes, tiny pupils, tremble |
| Confused | Asymmetric eyes, cross-eyed, floating "?" |

### Moods (8 Presets)
Tap the **mood dot** (top-center) to open the mood picker:

| Mood | Color | Eye Style | Personality |
|------|-------|-----------|-------------|
| Calm | Cyan | Soft oval | Perceptive, enigmatic |
| Cyberpunk | Pink | Hexagonal | Edgy netrunner |
| Cat | Green | Wide slit | Curious, sly, aloof |
| Demon | Red | Fiery | Intense, dramatic |
| Cute | Purple | Large round | Cheerful, warm |
| Sleepy | Orange | Narrow | Drowsy, trailing off |
| Robot | Blue | Rectangular | Precise, analytical |
| Panther | Gold | Tilted slit | Predatory, watchful |

Each mood changes: eye shape, iris colors, glow color, particle color, and personality.

### Idle Song Playback
- Upload songs via **settings** (gear icon) — supports multiple files
- After **30 seconds** of no interaction, a **random song** plays for 30 seconds
- Eyes go half-closed/dreamy during playback
- Fades out smoothly at the end
- Tapping the screen stops playback immediately
- Songs stored in IndexedDB (persists across sessions)
- Manage songs: add more anytime, remove individually, or clear all

### Time-of-Day Awareness
The companion adapts to the time of day:

| Time | Phase | Behavior |
|------|-------|----------|
| 5-7am | Dawn | Warm orange tint |
| 7am-12pm | Morning | Faint golden glow |
| 12-5pm | Day | Neutral |
| 5-8pm | Evening | Subtle purple tint |
| 8-11pm | Night | Deep blue tint, occasional yawns/droopy eyes |
| 11pm-5am | Late Night | Darker tint, more frequent drowsy behavior |

### Lock Mode
- **Lock button** (top-left) — hides all UI elements
- Only the eyes and particles remain — pure zen/ambient mode
- Tap lock again to restore all buttons
- Great for keeping it as a desk companion without distractions

---

## Settings (Gear Icon)

| Setting | Description |
|---------|-------------|
| Provider | Anthropic, OpenAI, or Groq (Free) |
| API Key | Your API key (stored in localStorage only) |
| Model | Available models for your chosen provider |
| Idle Songs | Upload audio files for idle playback |

### Supported Providers & Models

**Anthropic**: claude-opus-4-6, claude-sonnet-4-6, claude-haiku-4-5
**OpenAI**: gpt-4o, gpt-4o-mini, gpt-4.1, gpt-4.1-mini, gpt-4.1-nano
**Groq (Free)**: llama-3.3-70b-versatile, llama-4-scout-17b-16e-instruct, mixtral-8x7b-32768, deepseek-r1-distill-llama-70b

---

## Controls Summary

| Element | Location | Action |
|---------|----------|--------|
| Mic button | Bottom-right | Tap to toggle voice on/off |
| Lock button | Top-left | Tap to hide/show all UI |
| Mood dot | Top-center | Tap to open mood picker |
| Gear icon | Top-right | Tap to open settings |
| Eyes | Center | Tap, double-tap, or hold for reactions |

---

## Technical Details

- **Single file**: Everything in one `index.html` — no dependencies
- **APIs**: Web Speech API (recognition + synthesis), Web Audio API (volume analysis), IndexedDB (song storage)
- **Rendering**: SVG eyes, Canvas particles, CSS animations
- **Streaming**: Server-Sent Events for real-time token streaming from LLM
- **Mobile-ready**: PWA meta tags, safe area insets, touch optimized, viewport-fit=cover
- **Storage**: localStorage (settings, mood, API keys), IndexedDB (song files)

---

## Browser Compatibility

- **Best**: Chrome/Edge (desktop + mobile) — best voice support
- **Good**: Safari (macOS/iOS) — good TTS voices, speech recognition requires HTTPS
- **Note**: Mic requires HTTPS or localhost. Song autoplay requires at least one screen tap first (browser policy).
