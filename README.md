# WE SKIN

Landing page for **WE SKIN** — a curated skin & beauty studio inside i-Beauty, Chatswood, Sydney.

🔗 **Live:** https://www.we-skin.com  
(also deployed at https://we-skin.vercel.app)

## Overview

A single-page, mobile-first landing site with a bilingual (English / Mongolian) toggle and online booking through Square. No build step — plain HTML/CSS/JS.

- **Hosting:** Vercel (auto-deploys from this repository)
- **Domain / DNS:** Cloudflare
- **Booking:** Square Appointments

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire landing page — HTML, CSS, and JS inline |
| `hero-ring.png` | Gold ring logo used as the hero backdrop |

## Features

- Sticky navigation (About · Services · Contact · Book Now) with smooth scroll
- Hero section with ring-logo backdrop and tagline
- About section + treatment menu with per-service Square booking links
- Client reviews, studio info, and a floating WhatsApp button
- EN / MN language toggle that auto-detects the browser's preferred language

## Editing & deploying

1. Edit `index.html` locally.
2. Commit and push:
   ```bash
   git add index.html
   git commit -m "Describe your change"
   git push
   ```
3. Vercel detects the push and redeploys automatically (~1–2 min).

> When adding new image files (e.g. a logo), remember to `git add` them too, or they won't be deployed.

## To-do

- [ ] Replace the sample reviews with real client feedback (`I18N.en` / `I18N.mn` in `index.html`)
- [ ] Add hero / studio photos
- [ ] Set the Instagram URL (`INSTAGRAM_URL` in the script config)

---

© 2026 WE SKIN · Chatswood, NSW
