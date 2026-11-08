# RMIX

RMIX is a web project designed to bridge Nightbot song requests with a browser-based player for a Lightstream stream setup.

## Current status

The first commit contains a responsive frontend prototype:
- Dark purple/red RMIX interface
- Local demo request queue
- Demo play/pause/next/previous controls
- Volume UI
- Nightbot and Lightstream connection placeholders

**This is a UI demo only.** It does not connect to Nightbot or Lightstream, retrieve real requests, or stream audio yet.

## Planned architecture

- **Frontend:** static HTML/CSS/JavaScript hosted with GitHub Pages
- **Backend:** Supabase Edge Functions for OAuth callbacks and private API operations
- **Nightbot:** official OAuth/API integration, subject to confirming queue access and available fields
- **Lightstream:** browser-source player, subject to confirming supported audio playback and autoplay behavior

Never put OAuth client secrets, service-role keys, or other private credentials in GitHub Pages/frontend code. Use official OAuth flows and server-side secret storage.

## Local preview

Open `index.html` in a browser. The queue demo runs locally in the page.

## GitHub Pages

After enabling Pages for the `main` branch and root folder, the site should be published at:

https://echothedcdev.github.io/Rmix/
