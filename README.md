# 🥭 Black Mango — Browser-Based IPTV Player

A portable, single-file IPTV player that runs entirely in your browser. No installs, no servers, no dependencies. Open the HTML file and start watching.

![Black Mango](https://img.shields.io/badge/version-6.9-orange) ![License](https://img.shields.io/badge/license-MIT-green) ![Single File](https://img.shields.io/badge/single%20file-HTML-blue)

## What It Does

Black Mango connects to your IPTV provider and gives you live TV, movies, and TV shows in a clean browser-based interface. It works from a thumb drive, a local folder, or any static hosting — no backend required.

## Features

**Connections**
- Xtream Codes API (full: live, movies, series with episodes)
- Stalker / MAG portal support
- Xtream M3U fallback (auto or manual)
- M3U playlist import (file upload, URL, or paste)
- Manual channel add
- Multi-account support with per-account filtering

**Playback**
- Direct .ts stream playback (no CORS proxy needed for live TV)
- HLS.js for .m3u8 streams with automatic proxy fallback
- .ts → .m3u8 auto-fallback when direct playback fails
- Movie format fallback (.mp4 → .m3u8 via HLS.js)
- Picture-in-Picture with auto-PiP on navigation
- Custom live TV controls (play/pause, mute, volume, speed, PiP, cast, fullscreen, retry)
- Cast to any device via Remote Playback API

**Storage**
- IndexedDB for unlimited local storage (handles 30K+ channels)
- Granular saves prevent data races
- Account recovery for orphaned channels
- Export/import full backup as JSON

**Interface**
- Dark theme with orange/green accents
- Mobile responsive
- Live TV EPG-style channel list with search and category filters
- Movie and series list views with search and category filters
- Account filter dropdown (filter content by provider)
- Favorites system across all content types
- Recent plays on home screen
- Account badge in topbar showing connected providers

## Quick Start

1. Download `black-mango-iptv.html`
2. Open it in Chrome, Edge, or any Chromium browser
3. Click **+ Account** and enter your IPTV provider credentials
4. Start watching

That's it. No install, no setup, no server.

## How It Works

Black Mango runs entirely client-side. It uses free CORS proxies to reach your IPTV provider's API (since browsers block cross-origin requests). The proxy is only used for API calls — actual video streams play directly from your provider's server with no middleman.

**Proxy auto-detection:** Black Mango cycles through multiple CORS proxies automatically. If one is down or rate-limited, it tries the next. The last working proxy is remembered for faster reconnection.

**Stream playback:** Live TV uses .ts format which Chrome plays natively via `video.src` — no proxy needed for playback. Movies and shows play directly from the provider. HLS.js handles .m3u8 streams with proxy support when needed.

## Supported Providers

Any IPTV provider that supports one of these:
- Xtream Codes API (most common)
- Stalker/MAG portal
- M3U playlist (URL or file)

## Browser Support

- **Chrome / Edge / Brave** (recommended) — full feature support
- **Firefox** — works, some controls may differ
- **Safari** — native HLS support, some features limited

## Known Limitations

- **CORS proxies:** Free proxies have rate limits. If adding an account fails, wait 30 seconds and retry. Heavy usage may temporarily exhaust proxies.
- **Codec support:** Some streams use HEVC/H.265 which Chrome can't decode. These show "Format not supported" — this is a browser limitation, not a bug.
- **Cast:** Requires a castable device on your network. The Remote Playback API works best over HTTPS; running from `file://` may limit cast availability. Right-click → Cast always works.
- **No EPG guide data:** Channel categories come from the provider, but full EPG program guides are not yet implemented.

## File Structure

```
black-mango-iptv.html    ← The entire app. That's it.
```

Single file. ~100KB. Contains all HTML, CSS, JavaScript, and the embedded logo. HLS.js is loaded from CDN on first use.

## Privacy

- No analytics, no tracking, no telemetry
- All data stored locally in your browser's IndexedDB
- IPTV credentials never leave your machine (only sent to your provider's server via proxy)
- No cookies

## License

MIT — do whatever you want with it.

---

Built with stubbornness and too many proxy retries.
