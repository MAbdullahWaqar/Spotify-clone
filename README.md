# Spotify Clone 🎵

## Overview

A browser-based music player that faithfully replicates the core Spotify Web Player experience. Built with vanilla HTML, CSS, and JavaScript, it dynamically loads playlists and tracks from a structured folder system, providing seamless playback controls, seekbar interaction, volume management, and a fully responsive layout — all without any external frameworks or build tools.

## Key Features

- **Dynamic Playlist Loading** — Albums are discovered at runtime by fetching directory listings; each folder exposes a `cover.jpg` and `info.json` for metadata.
- **Full Playback Controls** — Play / Pause, Previous, and Next track buttons with real-time state updates.
- **Interactive Seekbar** — Click-to-seek with a smooth animated progress indicator and a live `MM:SS / MM:SS` timestamp display.
- **Volume Control & Mute Toggle** — Range slider for fine-grained volume adjustment; dedicated mute/unmute button with icon swap.
- **Curated Playlists** — Pre-loaded categories covering mood playlists (Angry, Bright, Chill, Dark, Funky, Love, Uplifting) and artist collections (Diljit, Karan Aujla, NCS, CS covers).
- **Responsive Design** — Adapts from full desktop layout to a mobile-friendly view with a slide-in sidebar triggered by a hamburger menu.
- **Dark Theme** — Spotify-faithful dark color scheme using CSS custom properties and utility classes.

## Tech Stack

| Category    | Technology                          |
|-------------|-------------------------------------|
| Language    | HTML5, CSS3, JavaScript (ES2017+)   |
| APIs        | Fetch API, Web Audio API (`<audio>`) |
| Fonts       | Google Fonts — Roboto, Lato         |
| Icons       | Custom SVG assets                   |
| Tools       | None — zero build toolchain         |
| Deployment  | Any static file server (Apache, Nginx, Live Server) |

## Installation

### Prerequisites

- A local static file server capable of serving directory listings (required for the Fetch-based folder discovery).  
  Apache with `Options +Indexes` or VS Code **Live Server** both work out of the box.

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/MAbdullahWaqar/Spotify-clone.git
cd Spotify-clone

# 2. Serve with Python (quick option)
python -m http.server 8080

# — or — serve with Node.js http-server
npx http-server -p 8080 --cors
```

> ⚠️ **Do not open `index.html` directly** (`file://` protocol). The `fetch()` calls that discover playlists require an HTTP server.

## Usage

1. Navigate to `http://localhost:8080` in your browser.
2. The page loads album cards from the `songs/` directory automatically.
3. Click any album card to load its track list into the sidebar.
4. Click a song row or the green play button on a card to start playback.
5. Use the fixed playbar at the bottom to control playback, seek, or adjust volume.
6. On screens narrower than 1200 px, tap the ☰ hamburger icon to open the sidebar.

## Project Structure

```
Spotify-clone/
├── index.html              # Single-page application entry point
├── favicon.ico
├── css/
│   ├── style.css           # Core layout, components, and responsive breakpoints
│   └── utility.css         # Reusable utility classes (flex, colors, spacing, scrollbar)
├── js/
│   └── script.js           # All application logic — playlist discovery, playback, UI events
├── img/                    # SVG icons and static images
│   ├── logo.svg
│   ├── play.svg / pause.svg
│   ├── prevsong.svg / nextsong.svg
│   ├── volume.svg / mute.svg
│   └── ...
└── songs/
    ├── .htaccess           # Enables Apache directory listing for fetch-based discovery
    ├── ncs/
    │   ├── info.json       # { "title": "...", "description": "..." }
    │   ├── cover.jpg
    │   └── *.mp3
    ├── cs/
    ├── Diljit/
    ├── karan aujla/
    ├── Angry_(mood)/
    ├── Bright_(mood)/
    ├── Chill_(mood)/
    ├── Dark_(mood)/
    ├── Funky_(mood)/
    ├── Love_(mood)/
    └── Uplifting_(mood)/
```

## Configuration

No environment variables are required. The only configuration needed is at the server level:

| Concern | Detail |
|---------|--------|
| **Directory listing** | The server must serve directory listings for `/songs/` and each album sub-folder. The included `.htaccess` enables this for Apache (`Options +Indexes`). For Nginx, add `autoindex on;` to the relevant `location` block. |
| **Adding a playlist** | Create a sub-folder under `songs/`, add an `info.json` (`title` + `description`), a `cover.jpg`, and any number of `.mp3` files. The UI will discover and display it automatically on next load. |

### `info.json` schema

```json
{
  "title": "Playlist Title",
  "description": "Short description shown on the album card"
}
```

## UI Features

- **Album Cards** — Dynamically rendered grid cards with cover art, title, description, and a hover-reveal green play button.
- **Sidebar Library** — Lists all tracks in the currently selected playlist; clicking a track starts playback immediately.
- **Playbar** — Fixed bottom bar containing song title, timestamp, seekbar, playback buttons, and volume controls.
- **Mobile Sidebar** — Off-canvas left panel that slides in on hamburger click and closes via an ✕ button.

## Contributing

1. Fork the repository and create a feature branch: `git checkout -b feature/your-feature`.
2. Keep changes focused — one feature or fix per pull request.
3. Test across at least Chrome and Firefox before opening a PR.
4. Open a pull request with a clear description of what was changed and why.

## License

This project is licensed under the [MIT License](LICENSE).  
Spotify®, its logo, and related assets are trademarks of Spotify AB. This project is an independent educational clone and is not affiliated with or endorsed by Spotify.

## Author

**Muhammad Abdullah Waqar**  
GitHub: [@MAbdullahWaqar](https://github.com/MAbdullahWaqar)
