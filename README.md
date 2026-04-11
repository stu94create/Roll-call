# Roll-Call

A lightweight, offline-friendly web app for taking attendance. Create groups
(classes, teams, clubs), add members, tick who's present, and send the
attendance list by email in one tap.

It's a single-file static site — no build step, no backend — and installs as a
PWA on mobile and desktop.

## Features

- Multiple groups with custom name, organisation, icon, and colour
- Add members one at a time or paste a list
- Fast member search and Select All / Clear All shortcuts
- One-tap "Send Email" that pre-fills a mailto: with the present-members list
- Five colour themes (amber, green, blue, white, red)
- JSON backup and restore
- Works offline via a service worker
- Keyboard accessible and screen-reader friendly

## Running locally

This is a static app — any HTTP server works. A couple of options:

```sh
# Python 3
python3 -m http.server 8000

# Node
npx serve .
```

Then open <http://localhost:8000>.

Opening `index.html` directly via `file://` will *mostly* work but the service
worker will not register, so offline mode won't be exercised. Use a local
server to test PWA behaviour.

## Deployment

The app is a single `index.html` plus `sw.js`. Drop both files on any static
host (GitHub Pages, Netlify, Cloudflare Pages, S3, etc.) at the same path and
it's live. Service-worker paths in `sw.js` are relative, so the app can be
hosted at the domain root or in a sub-path without changes.

## Data & privacy

- All data lives in `localStorage` in your browser. Nothing is sent to a
  server.
- Use **Settings → Backup** to export a JSON file you can archive or move to
  another device, and **Restore** to import one.
- Attendance ticks are intentionally **per-session** — they reset on page
  reload. Groups and members persist.

## Known limitations

- `localStorage` is bounded (typically 5–10 MB). If it fills up the app will
  surface a toast rather than silently dropping data, but you should back up
  regularly.
- Attendance history is not retained; send the email before closing the tab.
