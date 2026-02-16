# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

EventHub is a client-side event management web application. The entire app is a **single `index.html` file** (~5800 lines) containing all HTML, CSS, and JavaScript inline. There is no build system, no package manager, and no server-side code.

## Architecture

- **Single-file app**: All markup, styles, and logic live in `index.html`
- **No build step**: Open `index.html` directly in a browser or serve with any static file server
- **State management**: Global variables (`currentUser`, `events`, `notifications`, etc.) with localStorage for persistence
- **Data storage**: All user data, events, and settings are stored in `localStorage` (keys prefixed with `eventhub-`)
- **Authentication**: Client-side only — user credentials stored in localStorage with a simple hash. Demo account: `demo@eventhub.com` / `Demo123!`

### File Structure (within index.html)

1. **Lines 1–3225**: `<head>` (external dependencies, inline `<style>`) and `<body>` HTML markup
2. **Lines 3226–5804**: `<script>` block containing all application JavaScript

### Key Sections in the JavaScript

- **App state & initialization** (~line 3227): Global state variables and `DOMContentLoaded` setup
- **Auth system** (~line 3337): Login, registration, password validation, Google Sign-In stub
- **Event CRUD** (~line 3851): Create, edit, delete events with modal-based UI
- **Calendar rendering** (~line 4069): Custom calendar grid with month navigation
- **Analytics/Charts** (~line 4201): Chart.js-based dashboard (events, categories, trends, attendance)
- **Notifications** (~line 4399): In-app notification system
- **Settings/Profile** (~line 3780): User profile updates, theme toggle (light/dark)

### External Dependencies (loaded via CDN)

- **Chart.js** — analytics charts
- **EmailJS** — email functionality (requires API key configuration)
- **Google Sign-In** — OAuth stub (requires client ID configuration)
- **Font Awesome 6.4** — icons
- **Google Fonts (Inter)** — typography

## Development

No build commands. To develop:

```bash
# Serve locally (any static server works)
python3 -m http.server 8000
# or
npx serve .
```

Then open `http://localhost:8000` in a browser.

## Deployment

This is a static site suitable for GitHub Pages. Push `index.html` to the repository root and enable GitHub Pages from the repo settings (serve from main branch).
